Gestion des documents en erreur (rejets)
========================================

Ce guide vise à vous expliquer la configuration de la prise en charge des documents en erreur par la rendition. 


Configuration XML de la gestion des rejets
------------------------------------------


Dans le fichier arender-rendition.xml de votre rendition, retirer les commentaires de ce bloc xml afin d'activer la gestion des rejets : 

.. code-block:: xml

    <!-- Copy all documents with errors to the rejected path -->
    <property name="rejectedDocumentsPath">
        <value>${rendition.dir.rejected.documents}</value> 
    </property>

Ceci a pour effet de placer chaque document en erreur dans le dossier configuré par le paramètre "rendition.dir.rejected.documents" de votre fichier arender-rendition.properties. 

Configuration XML de l'image de remplacement 
--------------------------------------------

Il est également possible de configurer une image de remplacement en cas d'erreur dans le document. Si une page du document ou le document tout entier ne parvenait pas à être chargé, une image viendrait alors prendre place.

La configuration  de cette dernière se fait également depuis le fichier arender-rendition.xml, en retirant les commentaires autour du bloc de code suivant: 

.. code-block:: xml

    <!-- Replace all documents with errors by a static image -->
    <property name="rejectedDocumentReplacement">
        <bean class="com.arondor.viewer.rendition.image.StaticImageDocumentModel"> 
            <property name="title" value="Error"/>
            <property name="imagePath" value="${default.rejected.file}"/>
            <property name="pageDimensions">
                <bean class="com.arondor.viewer.client.api.document.PageDimensions"> 
                    <constructor-arg value="1600"/>
                    <constructor-arg value="1312"/>
                    <constructor-arg value="0"/>
                </bean>
            </property>
        </bean>
    </property>

Le paramètre "default.rejected.file" référence une image de votre choix à définir dans arender-rendition.properties. Le titre et les dimensions de cette dernière sont a remplir directement dans le bloc xml.