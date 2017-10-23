
--------------------------------
Développer son propre connecteur
--------------------------------

Définition d'un connecteur
==========================

**Comment définir un connecteur afin qu'il puisse être utilisé ?**

Pour définir un nouveau connecteur afin qu'il puisse être utilisé par ARender, il faut : 

* Que le JAR correspondant au connecteur soit dans le classpath du serveur d'application (par exemple : directement dans le répertoire *WEB-INF\\lib* de l'application web déployée)
* Ajouter la ligne suivante à la propriété *registeredURLParsers* du bean *servletDocumentService* (dans le fichier *arender.xml* situé dans le répertoire *WEB-INF\\classes* de l'application web déployée)::
    
    <ref bean="{nouveau_connecteur}"/>
  

* Exemple ::
 
    <bean id="servletDocumentService" class="com.arondor.viewer.server.servlet.ServletDocumentService"
      lazy-init="true" scope="prototype">
       <property name="disableCheckDocumentAvailability" value="true" />
       <property name="delegate">
          <ref bean="delegate" />
       </property>
       <property name="registeredURLParsers">
          <list>
             <bean class="com.arondor.viewer.server.servlet.urlparser.DefaultURLParser" />
             <ref bean="oracleURLParser" />
          </list>
       </property>
       <property name="defaultAnnotationAccessorBean" value="inMemoryAnnotations" />
    </bean>


Connecteur Oracle
=================

L'objectif de cet exemple de connecteur est de fournir la possibilité de récupérer un document stocké en tant que BLOB dans une base de données Oracle. Cet exemple se base sur les informations suivantes :

* Une URL à appeler du type ::

    http://{serveur_arender}/ARender.jsp?ref={référence_du_document}

* Un schéma Oracle nommé ARender contenant la table T_DOCS ::
    
    | REF (VARCHAR) | DOC (BLOB) |

* Les dépendances fournies par ARender (dans le répertoire *WEB-INF/lib* de l'application web) :


    =====================================       ================================================
    arondor-arender-client-api-2.2.0.jar        arondor-arender-rendition-api-2.2.0.jar
    arondor-arender-common-2.2.0.jar            arondor-common-io-2.0.0.jar
    arondor-common-mime-2.0.11.jar              log4j-1.2.16.jar
    commons-io-1.3.2.jar                        Spring 3.0.5.RELEASE
    commons-logging-1.1.1.jar                   ojdbc5-11.2.0.3.jar (non fournie par ARender)
    =====================================       ================================================

Parseur d'URL
---------------------------    
    
Le parseur d'URL définit le point d'entrée d'un connecteur et doit implémenter l'interface *DocumentServiceURLParser*.

* Variables de classe

.. code-block:: java

    // Le paramètre de l'URL à utiliser pour récupérer la référence d'un document
    private String docRefParameter;
    // La requête SQL permettant l'accès à un document
    private String query;
    private PreparedStatement preparedStatement;
    private DataSource dataSource;
 

* Définition de l'activation du connecteur

.. code-block:: java

    @Override
    public boolean canParse(DocumentService documentService, ServletContext context, HttpServletRequest request)
    {
       // Le connecteur n'est activé/utilisé que si l'URL d'appel possède le paramètre défini
       return request.getParameter(docRefParameter) != null;
    }    
    
* Chargement du document

.. code-block:: java

    @Override
    public DocumentId parse(DocumentService documentService, ServletContext context, HttpServletRequest request)
       throws DocumentNotAvailableException, DocumentFormatNotSupportedException
    {
       String docRef = request.getParameter(docRefParameter);
       DocumentId documentId = DocumentIdGenerator.generate(docRef);
       BlobOracleDocumentAccessor oracleDocumentAccessor = new BlobOracleDocumentAccessor(docRef, documentId,
          getOrCreatePreparedStatement());
       return documentService.loadDocument(oracleDocumentAccessor);
    }

    protected PreparedStatement getOrCreatePreparedStatement()
    {
       if (preparedStatement == null)
       {
          try
          {
             Connection connection = dataSource.getConnection();
             preparedStatement = connection.prepareStatement(getQuery());
          }
          catch (SQLException e)
          {
             LOGGER.error("Could not prepare statement for document fetching", e);
          }
       }
       return preparedStatement;
    }
     

* Les getters et setters permettant la configuration des paramètres

.. code-block:: java

    public DataSource getDataSource()
    {
       return dataSource;
    }

    public void setDataSource(DataSource dataSource)
    {
       this.dataSource = dataSource;
    }

    public String getDocRefParameter()
    {
       return docRefParameter;
    }

    public void setDocRefParameter(String docRefParameter)
    {
       this.docRefParameter = docRefParameter;
    }

    public String getQuery()
    {
       return query;
    }

    public void setQuery(String query)
    {
       this.query = query;
    }
     

* Configuration Spring du connecteur

.. code-block:: java

    <bean id="oracleURLParser" class="com.arondor.viewer.oracle.OracleURLParser">
       <property name="docRefParameter" value="ref" />
       <property name="query" value="SELECT DOC FROM ARender.T_DOCS WHERE REF=?" />
       <property name="dataSource">
          <bean id="dataSource" class="oracle.jdbc.pool.OracleDataSource" destroy-method="close">
             <property name="connectionCachingEnabled" value="true" />
             <property name="URL" value="jdbc:oracle:thin:@{hôte}:{port}:{SID}" />
             <property name="user" value="{utilisateur}" />
             <property name="password" value="{mot_de_passe}" />
          </bean>
       </property>
    </bean>    

Nota : Se référer à la section `Définition d'un connecteur <file:///C:/Users/A.%20BOUAZZAOUI/Desktop/sphinxHTML/connecteurs.html#definition-d-un-connecteur>`_ pour sa prise en compte par ARender

Accès au contenu du document
----------------------------
 
Cette partie détaille la manière dont le document est récupéré à travers le DAO, *BlobOracleDocumentAccessor*,  implémentant l'interface *DocumentAccessor*.

* Récupération du contenu

L'objectif est, ici, de récupérer le flux correspondant au BLOB à visualiser. Pour cela, le *PreparedStatement* fourni au constructeur est utilisé.

.. code-block:: java

    @Override
    public byte[] toByteArray() throws IOException
    {
       try
       {
          preparedStatement.setLong(1, Long.parseLong(docRef));
          ResultSet resultSet = preparedStatement.executeQuery();
          if (!resultSet.next())
          {
             LOGGER.error("No result can be found for F_DocNumber : " + docRef);
             throw new IOException("No result can be found for F_DocNumber : " + docRef);
          }
          else
          {
             Blob blob = (Blob) resultSet.getObject(1);
             return IOUtils.toByteArray(blob.getBinaryStream());
          }
       }
       catch (NumberFormatException e)
       {
          LOGGER.error("Cannot fetch document content : F_DocNumber is not a valid long : " + docRef, e);
          throw (e);
       }
       catch (SQLException e)
       {
          LOGGER.error("Cannot fetch document content : Impossible to update statement with F_DocNumber: " + docRef,e);
          throw new IOException(e);
       }
    }
    @Override
    public InputStream getInputStream() throws IOException
    {
       return new ByteArrayInputStream(this.toByteArray());
    }
    @Override
    public DocumentAccessor asSerializableDocumentAccessor() throws IOException
    {
       return new DocumentAccessorByteArray(getUUID(), getInputStream());
    }
     

Ajout de métadonnées

.. code-block:: java

    @Override
    public DocumentMetadata getDocumentMetadata()
    {
       DocumentMetadata documentMetadata = new DocumentMetadata();
       DocumentProperty docProperty = new DocumentProperty("client", "Client");
       docProperty.setValue("M. Richard Dupond");
       documentMetadata.addDocumentProperty("client", docProperty);
       return documentMetadata;
    }
 
 
`Télécharger les sources du connecteur <http://blogs.arondor.com/administrer/content/download/1859/12592/file/ARender-connector-Oracle-sample.zip>`_. 


Créer un nouvel AnnotationAccessor
==================================

Quand vous créez votre propre connecteur vous devez définir comment récupérer, ajouter, mettre à jour et supprimer des annotations. Pour ce faire ARender offre une API qui définie quatre méthodes principales à implémenter : create,update,get and delete.

Ci-dessous sont décrites les trois principales étapes afin d'initialiser votre AnnotationAccessor: 

1. Implémenter l'interface AnnotationAccessor

2. Créer les constructeurs

3. Implémenter les méthodes

Implémenter l'interface AnnotationAccessor
------------------------------------------

.. code-block:: java

    public class CustomAnnotationAccessor implements AnnotationAccessor {

Créer les constructeurs
-----------------------

La bonne pratique est de définir deux constructeurs.

Un constructeur par défaut, générique, basé uniquement sur le documentId.

.. code-block:: java

    public CustomAnnotationAccessor(DocumentService documentService, DocumentId documentId)
    {
        if (documentId == null)
        {
            throw new IllegalArgumentException("Invalid null documentId provided !");
        }
        this.documentId = documentId;
    }
    
Et un basé sur le documentAccessor

.. code-block:: java

    public CustomAnnotationAccessor(DocumentService documentService, DocumentAccessor documentAccessor)
    {
        this(documentService, documentAccessor.getUUID());
    }
    
Les méthodes à implémenter
--------------------------

**Méthode create**
    
Cette méthode prend dans le paramètre une liste d'Annotation qui a été créée et enregistrée.

Définissez ici où et comment stocker ces nouvelles annotations.

.. code-block:: java

    @Override
    public void create(List<com.arondor.viewer.annotation.api.Annotation> annotations)
            throws AnnotationsNotSupportedException, InvalidAnnotationFormatException, AnnotationCredentialsException,
            AnnotationNotAvailableException
    {
    
**Méthode update**

Cette méthode prend en paramètre une liste d'Annotation qui a été mise à jour et enregistrée.

Définissez ici où et comment enregistrer ces annotations mises à jour.

.. code-block:: java

    @Override
    public void update(List<com.arondor.viewer.annotation.api.Annotation> annotations)
            throws AnnotationsNotSupportedException, InvalidAnnotationFormatException, AnnotationNotAvailableException,
            AnnotationCredentialsException
    {

**Méthode get**

Cette méthode retourne une liste d'annotations à extraire. Définissez ici comment les récupérer.

.. code-block:: java

    @Override
    public synchronized List<Annotation> get() throws AnnotationsNotSupportedException,
            InvalidAnnotationFormatException
    {

**Méthode delete**

Cette méthode prend en paramètre une liste d'annotations qui ont été supprimées. Définissez ici où et comment les supprimer.

.. code-block:: java

    @Override
    public void delete(List<com.arondor.viewer.annotation.api.Annotation> annotations)
            throws AnnotationsNotSupportedException, InvalidAnnotationFormatException, AnnotationNotAvailableException,
            AnnotationCredentialsException
    {

**Méthode getAnnotationCreationPolicy**

Cette méthode retourne un objet AnnotationCreationPolicy qui défini:

* Si l'utilisateur peut créer ou non des annotations
* Le catalogue de tampons utilisateur

.. code-block:: java

    @Override
    public AnnotationCreationPolicy getAnnotationCreationPolicy()
    {
        return annotationCreationPolicy;
    }

Liens utiles : 

* l'API AnnotationAccessor est disponible ici : http://arender.fr/rendition-api/com/arondor/viewer/rendition/api/annotation/AnnotationAccessor.html

Cacher les paramètres de l'URL
==============================

ARender offre le moyen de cacher les paramètres de l'URL.

 * La première étape consiste à générer la même URL mais en pointant sur la JSP openExternalDocument.jsp. Arender va retourner dans la réponse un UUID (ID du document au sens ARender) :

    + http://[HOST_ARENDER]/openExternalDocument.jsp?[PARAMETERS]

 * Avec l'UUID récupéré de la réponse ci-dessus, générer l'URL ci-dessous et visualiser le document !

    + http://[HOST_ARENDER]/?uuid=[UUID_FETCHED_ABOVE]
