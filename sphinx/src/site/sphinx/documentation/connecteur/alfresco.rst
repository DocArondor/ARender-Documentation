-------------
CMIS Alfresco
-------------

ARender for Alfresco
====================

.. image:: /_static/images/ARender-for-Alfresco_imagefull.png
	:align: center

Cet article détaille l'intégration et l'installation du connecteur CMIS Arender. Ceci couvre la partie intégration dans Alfresco et la partie configuration HMI. La configuration du serveur de rendition n'est pas détaillée ici. 

La partie installation Alfresco concerne les versions 4.X et 5.0

Il est à mentionner que le connecteur se base sur le protocole  CMIS, donc potentiellement "intégrable" dans toutes les GED supportant le CMIS.

Le connecteur permet de gérer les enregistrements des annotations sur Alfresco, les fichiers XML d'annotations sont enregistrés dans un espace Alfresco configurable.

Le connecteur ne gère pas encore les métadonnées à l'enregistrement du document après une modification via documentBuilder. Il va cloner celles du document courant.
 
	+----------------+-------------------------------------------------------------------------------------------------------------------+
	| Paramètre      | Description                                                                                                       |
	+================+===================================================================================================================+
	| nodeRef        | Exemple : workspace://SpacesStore/6eb252b8-416b-40ad-a704-5fa39641a211                                            |
	|                | Identifiant unique d'un document                                                                                  |
	+----------------+-------------------------------------------------------------------------------------------------------------------+
	| alf_ticket     | format : TICKET_d6396b6d866f19b5e2f70e36c6e21df551573610                                                          |
	|                | Ticket d'authentification Alfresco.                                                                               |
	+----------------+-------------------------------------------------------------------------------------------------------------------+
	| ARenderContext | Nom de la webapp déployée                                                                                         |
	+----------------+-------------------------------------------------------------------------------------------------------------------+

* Exemples : 

Ouverture d'un document simple stocké dans Alfresco :

	http://{arender_serveur}:{arender_port}/{ARenderContext}/ARender.jsp?nodeRef=workspace://SpacesStore/6eb252b8-416b-40ad-a704-5fa39641a211&alf_ticket=TICKET_XXX

Installation de l'IHM ARender:
	* Arrêter le service Alfresco
	* Copiez le fichier arondor-arender-hmi-alfresco-<version_arender>.war dans  votre dossier <chemin_alfresco>/tomcat/webapps
	* Renommez le fichier .war en : ARenderHMI.war et ouvrir l'archive.
	
Configuration ARender HMI
=========================

Définition du connecteur
------------------------
	
Comme détaillé ci-dessous, le connecteur CMIS est composé de deux éléments. Le premier concerne l'accès à un l'entrepot Alfresco et ses documents. Le deuxième est chargé d'introduire un nouveau URL parser dans la configuration ARender.

Vous trouverez la configuration du connecteur CMIS dans le fichier arender.xml situé dans le fichier ARenderHMI.war : WEB-INF/classes.

**Attention :** Vérifier l'url du connecteur CMIS de la propriété « atomPubURL » en fonction de la version d'Alfresco installée (voir la description de la propriété « atomPubURL » dans la partie Propriétés du beans CmisConnection située ci-dessous).

.. code-block:: xml 

	<bean id="cmisConnection" class="com.arondor.viewer.cmis.CMISConnection" scope="prototype">
			<!-- Mandatory: Cmis URL  http://wiki.alfresco.com/wiki/CMIS#CMIS_Service_URL -->
			<property name="atomPubURL" value="http://localhost:8080/alfresco/service/cmis" />
			<!-- Optional : if set : connector use disk storage to get document content. if not set, connector use CMIS to get document content -->
			<property name="alfDataAbsolutePath" value="/opt/alfresco/alf_data/contentStore" />
			<!-- Optional : if not set : annotationPath is "/Dictionnaire de données" -->
			<property name="annotationsPath">
				<value>/Dictionnaire de données</value>
			</property>
			<!-- Optional : if not set : annotationFolderName is Annotations -->
			<property name="annotationFolderName">
				<value>Annotations</value>
			</property>
	</bean>	
    
**Propriétés du beans CmisConnection :**

    ===================================     =========================================================================================================================================================================================================================
    Propriété                               Description          
    ===================================     =========================================================================================================================================================================================================================
    atomPubURL                              URL du service CMIS, selon les versions Alfresco voir: https://wiki.alfresco.com/wiki/CMIS#CMIS_Service_URL

                                            Les connecteur est testé avec les version CMIS 1.0 et 1.1
    alfDataAbsolutePath                     Chemin de stockage des fichiers Alfresco  : C'est le contentStore Alfresco, système de fichier où sont stockés tous les contenus Alfresco.

                                            **Ce dernier ne peut être utilisé que dans le cas où le HMI est installé sur le même serveur qu'Alfresco ou que le serveur HMI peut accéder a ce stockage.** Dans le cas contraire, cette propriété doit être commentée.


    annotationsPath                         Chemin sur Alfresco du stockage du dossier d'annotations.
    annotationFolderName                    Nom du dossier d'annotations
    ===================================     =========================================================================================================================================================================================================================

Configuration de l'accès aux documents
--------------------------------------

Selon le mode d'authentification choisi, deux types de fournisseurs peuvent être utilisés pour fournir un accès aux documents.

Authentification avec ticket
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

L'authentification par ticket ne nécessite aucune configuration supplémentaire.

Authentification avec un compte service
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


Afin d'utiliser la visionneuse Arender avec un compte de service, les deux propriétés user et password sont nécessaires dans la configuration de bean cmisConnection (à définir, si souhaité, dans le fichier arender.xml situé dans le dossier WEB-INF/classes du war ARender - Alfresco):

.. code-block:: xml 

	<bean id="cmisConnection" class="com.arondor.viewer.cmis.CMISConnection" scope="prototype">
			<!-- Mandatory: Cmis URL  http://wiki.alfresco.com/wiki/CMIS#CMIS_Service_URL -->
			<property name="atomPubURL" value="http://localhost:8080/alfresco/service/cmis" />
			<property name="user" value="admin" />
		   <property name="password" value="admin" />
	</bean>
	
Installation/Configuration Alfresco
===================================
	
L'intégration d'Arender sur Alfresco se fait via un module de type jar, ce dernier est à copier sur le serveur Alfresco.

Les modules packagés se basent sur l'architecture « HMI » et doivent être sur le même serveur d'application qu'Alfresco. Ils se trouvent dans le dossier webapps de tomcat avec pour nom : ARenderHMI.

L'installation d'un jar nécessite le redémarrage d'Alfresco.	
	
Alfresco version 4.0.X-4.1.X
----------------------------

Déposez le jar "arender-for-alfresco-4.0-4.1-plugin.jar" dans tomcat/shared/lib

Redémarrer Alfresco.

Alfresco version 4.2.X-5.0.X
----------------------------

Déposez le jar "arender-for-alfresco-4.2-5.0-plugin.jar " dans tomcat/shared/lib

Redémarrer Alfresco.

Vous pouvez voir si le plugin est bien activé à cette adresse:
 
<votre_url_alfresco>/share/page/modules/deploy

Si ce n'est pas le cas, vérifiez dans catalina.properties si les jar de shared/lib sont lus. 