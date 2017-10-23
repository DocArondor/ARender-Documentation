--------------
IBM FileNet P8
--------------

Des connecteurs pour les versions 4.x et 5.x de la solution de Gestion Électronique de Documents, FileNet P8, d'IBM. La configuration est cependant identique quelque soit la version concernée.

    ===================================    ==============================================================================================================================
    Paramètre                              Description          
    ===================================    ==============================================================================================================================
    id                                     Identifiant unique d'une version d'un document
    vsId                                   Identifiant d'une VersionSeries permettant de récupérer la dernière version d'un document
    objectStoreName                        Nom de l'ObjectStore dans lequel est stocké le document
    objectType                             Type du document à visualiser : document, folder, contentContainerXML, mixedObjects (facultatif dans le cas d'un document)
    ===================================    ==============================================================================================================================

* Exemples : 

Ouverture d'un document simple stocké dans FileNet P8 ::

    http://{arender_serveur}/ARender.jsp?id={345A81-KT7SK95747S-5IS8-8SK0}&objectStoreName=OS1

Ouverture de deux documents simultanément avec la syntaxe mixedObjects ::

    http://{arender_serveur}/ARender.jsp?ids=doc:{345A81-KT7SK95747S-5IS8-8SK0},doc:{F64A9342-6114-4A5C-A5E1-589A2FFB159F}&objectStoreName=OS1&objectType=mixedObjects

Ouverture de deux documents et d'un folder simultanément ::

    http://{arender_serveur}/ARender.jsp?objectStoreName=OS1&ids=doc:{3DBE573A-1AC9-4B08-8CB1-8F9495619954},doc:{F64A9342-6114-4A5C-A5E1-589A2FFB159F},folder:{55714817-BDAC-4C8A-9EFB-963E4620A4E4}&objectType=mixedObjects
    
La syntaxe mixedObjects est la suivante :

    ids=[ [ "doc" | "folder" ] ":" [ Id du document ou Folder] [ "," ] ]+    
    
Définition du connecteur
========================

Comme détaillé ci-dessous, un connecteur FileNet est composé de deux éléments. Le premier concerne l'accès à un ObjectStore et ses documents. Le deuxième est chargé de gérer la configuration des propriétés d'un document.

.. code-block:: xml 

    <bean id="fileNetUrlParser" class="com.arondor.viewer.filenetce.FileNetURLParser">
        <property name="objectStoreProvider">
            <ref bean="objectStoreProvider" />
        </property>
        <property name="documentPropertiesConfiguration">
            <ref bean="documentPropertiesConfiguration" />
        </property>
    </bean>

* Définition : 

Ajouter la ligne suivante à la propriété registeredURLParsers du bean servletDocumentService ::

    <ref bean="fileNetURLParser"/>

Configuration de l'accès aux documents
======================================

Selon le mode d'authentification choisi, deux types de fournisseur peuvent être utilisés pour fournir un accès aux documents.

Partage de la session FileNet
-----------------------------

Dans la même JVM (ou à minima partage de contexte JAAS) en utilisant le protocole IIOP : 

    ===================================        =================================================
    Paramètre                                  Description          
    ===================================        =================================================
    ceConnectionUri                            URI du Content Engine utilisant le protocol IIOP
    ===================================        =================================================

* Exemple ::

    <bean id="objectStoreProvider" class="com.arondor.viewer.filenetce.helper.impl.JaasObjectStoreProvider">
        <property name="ceConnectionUri" value="iiop://localhost:2809/FileNet/Engine"/>
    </bean>
    
    
Compte de service
-----------------

Dans le contraire, en utilisant les web services exposés :

    ===================================        ======================================================================================
    Paramètre                                Description          
    ===================================        ======================================================================================
    ceConnectionUri                                        URI du Content Engine utilisant les WS exposés par le CE (MTOM ou DIME)
    login                                    Identifiant du compte de service utilisé
    password                            Mot de passe du compte de service utilisé
    ===================================        ======================================================================================


* Exemple en HTTP ::

    <bean id="objectStoreProvider" class="com.arondor.viewer.filenetce.helper.impl.LoginPasswordObjectStoreProvider">
        <property name="login" value="{p8_identifiant}"/>
        <property name="password" value="{p8_password}"/>
        <property name="ceConnectionUri" value="http://{serveur_content_engine}/wsi/FNCEWS40MTOM/"/>
    </bean>    
    
* Exemple en IIOP ::

    <bean id="objectStoreProvider" class="com.arondor.viewer.filenetce.helper.impl.LoginPasswordObjectStoreProvider">
        <property name="login" value="{p8_identifiant}"/>
        <property name="password" value="{p8_password}"/>
        <property name="ceConnectionUri" value="iiop://{serveur_content_engine}/FileNet/Engine"/>
        <property name="jaasStanza" value="FileNetP8" />
    </bean>

*Nota : Ce deuxième type d'accès implique que l'utilisateur n'est pas authentifié au sein du serveur d'application. Une modification de fichier web.xml est donc nécessaire afin de désactiver les contraintes de sécurité définies par défaut.*

Gestion des métadonnées à récupérer
===================================

.. code-block:: xml

    <bean id="documentPropertiesConfiguration" class="com.arondor.viewer.filenetce.config.DocumentPropertiesConfiguration">
    </bean> 

Récupérer des métadonnées système
---------------------------------

Par défaut, aucune métadonnée système n'est récupérée. Pour forcer la récupération d'une ou plusieurs, il faut ajouter/éditer la propriété *includedSystemProperties*.

* Exemple: ::

    <property name="includedSystemProperties">
        <list>
            <value>DateCreated</value>
            <value>DateLastModified</value>
            <value>Creator</value>
            <value>LastModifier</value>
        </list>
    </property>

Exclure des métadonnées personnalisées 
--------------------------------------

Par défaut, l'ensemble des métadonnées personnalisées sont récupérées et affichées. Pour forcer, l'exclusion d'une ou plusieurs, il faut ajouter/éditer la propriété *excludedCustomProperties*.

Exemple: ::

    <property name="excludedCustomProperties">
        <list>
            <value>FactureRef</value>
        </list>
    </property>

**Note** : Si l'erreur suivante apparaît : *No LoginModules configured for FilenetP8WSI*, une configuration WAS est nécessaire :

 * Déposer le fichier :download:`jaas.conf.WebSphere </_static/docs/jaas.conf.WebSphere>` dans un dossier du serveur WAS

 * Ajouter un paramètre à la JVM ARender :

    + Menu Server puis Gestion des Gestion des processus et Java puis définition des processus puis Arguments de commande de démarrage et ajouter la commande ci-dessous : -Djava.security.auth.login.config=[Chemin_vers_fichier_jaas.conf.WebSphere]

Depuis une interface graphique
==============================

IBM Workplace & Workplace XT
----------------------------

Pour définir quels types de documents doivent s'ouvrir avec ARender, il suffit d'éditer le fichier content-redir.properties (Pour la Workplace XT, situé par défaut dans le dossier : *C:\Program Files\FileNet\Config\WebClient*) ::

    {mimeType}=/../ARender/ARender.jsp?{JSP_QUERY_STRING}

IBM Content Navigator
---------------------

Un plugin spécifique a été développé pour permettre l'intégration d'ARender avec ICN. 
Nota : le connecteur ICN est basé sur la syntaxe mixedObjects cité ci-dessus.

Se connecter au Content Navigator.

Aller dans la vue "Administration" et cliquer sur "Plug-ins". 

.. image:: /_static/images/ICN_clickplugin_medium.png
    :align: center 

Cliquer sur "Nouveau Plug-in".

.. image:: /_static/images/ICN_newplugin_large.png
    :align: center 

Entrer le chemin et nom du JAR et cliquer sur "Charger".

Exemple:  *C:\\sources\\ARenderHMI\\arondor-arender-navigator-plugin-2.2.1.jar*

.. image:: /_static/images/ICN_pickjar_backgroundimage.png
    :align: center 

Dans le champ ARender context root entrer l'adresse (host + port + context root) de ARender. Cf. exemple ci-dessous :

.. image:: /_static/images/PluginContextRoot_en_backgroundimage.png
    :align: center 

La liste des propriétés définies dans la classe ARenderPlugin est automatiquement chargée dans l'interface, cliquer sur "Sauvegarder".

Cliquer sur "Éditer" et vérifier que le plug-in a été correctement installé.

.. image:: /_static/images/ICN_editplugin_backgroundimage.png
    :align: center 

Mapping du nouveau viewer.
Aller dans l'onglet "Mappes d'afficheur". 

.. image:: /_static/images/ICN_clickmaps_medium.png
    :align: center 

La mappe par défaut s'appelle "Mappe de l'afficheur par défaut" et n'est pas modifiable, cliquer dessus et cliquer sur "Copier".

.. image:: /_static/images/ICN_copymap_backgroundimage.png
    :align: center 

Cliquer sur "Nouveau mappage" et sélectionner le nouveau viewer qui apparaît dans la liste des afficheurs disponibles. 

.. image:: /_static/images/ICN_namemap_backgroundimage.png
    :align: center 

Vous pouvez alors choisir dans la liste des types mimes supportés.

.. image:: /_static/images/ICN_mapmimes_backgroundimage.png
    :align: center 

Pour utiliser cette mappe d'afficheur, il suffit de l'associer à un bureau (dans l'onglet général de définition du bureau, Mappe d'afficheur).

.. image:: /_static/images/ICN_linkdesktop_backgroundimage.png
    :align: center

Note
---------------------

Si une popup de connexion s'affiche dans ARender ou dans IBM Navigator à la fermeture de ARender, une configuration supplémentaire est à effectuer, voir ci-dessous.
Modifier le nom du cookie associé à l'application ARender (par défaut JSESSIONID)

*Applications d'entreprise > ARender [VERSION ARENDER] for FileNet 5.x > Gestion des modules > arondor-arender-hmi-filenet-[VERSION ARENDER].war > Gestion de session > Cookies*

.. image:: /_static/images/ICN_ARender_cookie_name.png
    :align: center