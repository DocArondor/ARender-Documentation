-------------
CMIS Alfresco
-------------

ARender for Alfresco
====================

.. image:: /_static/images/ARender-for-Alfresco_imagefull.png
    :align: center

This article details the integration and installation of CMIS connector Arender. This covers the integration part in Alfresco and HMI configuration part. The rendition server configuration is not detailed here.

Alfresco installation section concerns 4.X and 5.0 versions.

It should be mentioned that the connector is based on CMIS protocol, so potentially "integrated" in each CMS supporting the CMIS.

The connector is used to manage records annotations on Alfresco, XML annotation files are stored in a configurable Alfresco space.

The connector does not yet support the metadata and saving the document after a change via DocumentBuilder.
 
    +----------------+-------------------------------------------------------------------------------------------------------------------+
    | Parameter      | Description                                                                                                       |
    +================+===================================================================================================================+
    | nodeRef        | Example : workspace://SpacesStore/6eb252b8-416b-40ad-a704-5fa39641a211                                            |
    |                | Universal Unique Identifier of a document                                                                         |
    +----------------+-------------------------------------------------------------------------------------------------------------------+
    | alf_ticket     | format : TICKET_d6396b6d866f19b5e2f70e36c6e21df551573610                                                          |
    |                | Authentication ticket for Alfresco.                                                                               |
    +----------------+-------------------------------------------------------------------------------------------------------------------+
    | ARenderContext | Name of deployed webapp                                                                                           |
    +----------------+-------------------------------------------------------------------------------------------------------------------+

* Examples : 

With Arender, URL to open a document in Alfresco :

http://{arender_serveur}:{arender_port}/{ARenderContext}/ARender.jsp?nodeRef=workspace://SpacesStore/6eb252b8-416b-40ad-a704-5fa39641a211&alf_ticket=TICKET_XXX

    
Configuration ARender HMI
=========================

Connector configuration
-----------------------
    
As detailed below, a CMIS connector consists of two elements. The first access to the Alfresco repository and documents. The second is responsible for introducing a new URL parser in Arender configuration.

You will find the configuration of the CMIS connector in the file arender.xml located in the folder ARenderHMI.war : WEB-INF/classes.

**Warning :** Check the url of the cmis connector regarding the property « atomPubURL » according to the installed Alfresco version (See the description of the "atomPubURL" property in the Properties section of the CmisConnection bean below).

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
    
**Properties of the CmisConnection bean:**

    ===================================     ================================================================================================================================================================================
    Property                                Description          
    ===================================     ================================================================================================================================================================================
    atomPubURL                              CMIS URL,  : https://wiki.alfresco.com/wiki/CMIS#CMIS_Service_URL

                                            The connector is tested with CMIS Version 1.0 et 1.1
    alfDataAbsolutePath                     Path of storing Alfresco files : This is the contentstore, file system that stores all Alfresco content.
 
                                            this property can be used only if HMI is installed on the same Alfresco server or the HMI server can access to alfresco storage. Otherwise, this property must be commented
    annotationsPath                         CMIS Alfresco storage path for store annotations.
    annotationFolderName                    Annotation folder name.
    ===================================     ================================================================================================================================================================================

*Definition :*

Add the following lines to the property registeredURLParsers bean servletDocumentService

.. code-block:: xml 

    <bean class="com.arondor.viewer.cmis.CMISURLParser">
                 <property name="cmisConnection">
                            <ref bean="cmisConnection" />
                 </property>
    </bean>

Authentication
--------------

Depending on the selected authentication mode, two types of providers can be used to provide access to documents

Ticket authentication
~~~~~~~~~~~~~~~~~~~~~

Ticket authentication no requires additional configuration

Service account authentication
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To use the Arender viewer with a service account, the two properties user and password are required in the configuration bean cmisConnection

.. code-block:: xml 

    <bean id="cmisConnection" class="com.arondor.viewer.cmis.CMISConnection" scope="prototype">
            <!-- Mandatory: Cmis URL  http://wiki.alfresco.com/wiki/CMIS#CMIS_Service_URL -->
            <property name="atomPubURL" value="http://localhost:8080/alfresco/service/cmis" />
            <property name="user" value="admin" />
           <property name="password" value="admin" />
    </bean>

Add CMIS Jars dependencies : apache Chemistry
---------------------------------------------

In the current state, Arender HMI does not carry the jars CMIS, to correct this and to properly use the server CMIS Alfresco, please download the Apache Chemistry jars 0.12 :  :download: `chemistry-opencmis-client-impl-0.12.0-with-dependencies.zip <chemistry-opencmis-client-impl-0.12.0-with-dependencies.zip>`_ and copy the jars in the folder: webapps/ArenderHMI/lib/

    
Alfresco Installation/Configuration
====================================    
    
Arender integration for Alfresco is a Alfresco Jar module.
The following jar assumes the architecture is the following: an ARender war deployed into the alfresco tomcat server, named ARenderHMI.war
Please follow this architecture when making your deployments.
The jar installation requires restarting Alfresco.

    
Alfresco version 4.0.X-4.1.X
----------------------------

Place the jar "arender-for-alfresco-4.2-4.1-plugin-0.1.jar" on tomcat/shared/lib

Restart Alfresco.

Alfresco version 4.2.X-5.0.X
----------------------------

Place the jar "arender-for-alfresco-4.2-5.0-plugin-0.1.jar " on tomcat/shared/lib

Restart Alfresco.


You can check if the plugin is activated at this URL: 
 
<your_alfresco_url>/share/page/modules/deploy

If it's not the case, double check that catalina.properties checks the shared/lib folder for loaded libraries. 