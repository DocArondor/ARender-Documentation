--------------
IBM FileNet P8
--------------

Connectors for FileNet P8 4.x and 5.x are provided. However, a unique configuration is required regardless version.

    ===================================    ====================================================================================
    Parameter                              Description          
    ===================================    ====================================================================================
    id                                     Unique id of document version
    vsId                                   VersionSeries id allowing to fetch last version of a document
    objectStoreName                        The name of the ObjectStore used to store the document
    objectType                             Document type: document, folder, containerXML, mixedObjects (optional for documents)
    ===================================    ====================================================================================

* Examples: :: 

    Open a document stored in FileNet P8
    http://{server_arender}/ARender.jsp?id={345A81-KT7SK95747S-5IS8-8SK0}&objectStoreName=OS1
    
Define the connector
====================

As detailed below, the connector is composed of two parts. First one is designed for the access of an ObjectStore and its documents. Second one is responsible to manage metadata fetching.

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

Add following lines to *registeredURLParsers* property of *servletDocumentService* bean:

    <ref bean="fileNetURLParser"/>

Document access
===============

Regarding authentication mode, two provider types can be used to provide document access.

Sharing FileNet session
-----------------------

In the same JVM (or at least in a shared JAAS context) using IIOP protocol:

    ===================================      ==============================================
    Parameter                                Description          
    ===================================      ==============================================
    ceConnectionUri                          URI of Content Engine using the IIOP protocol
    ===================================      ==============================================

* Example ::

    <bean id="objectStoreProvider" class="com.arondor.viewer.filenetce.helper.impl.JaasObjectStoreProvider">
        <property name="ceConnectionUri" value="iiop://localhost:2809/FileNet/Engine"/>
    </bean>
    
*Nota: It implies that a FileNet session has been previously instanciated.*
 
Technical account
-----------------

Otherwise, FileNet web services can be consumed using :

    ===================================     ====================================================================
    Parameter                               Description          
    ===================================     ====================================================================
    ceConnectionUri                         URI of Content Engine based on FileNet WS (MTOM ou DIME)
    login                                   Username of technical account
    password                                Password of technical account
    ===================================     ====================================================================


* Example ::

    <bean id="objectStoreProvider" class="com.arondor.viewer.filenetce.helper.impl.LoginPasswordObjectStoreProvider">
     <property name="login" value="{p8_identifiant}"/>
     <property name="password" value="{p8_password}"/>
     <property name="ceConnectionUri" value="http://{content_engine_server}/wsi/FNCEWS40MTOM/"/>
    </bean>
    

*Nota : This access type implies that user is not authenticated at application loading. So, security constraints must be disabled in web.xml configuration file.*

Metadata fetching
=================

.. code-block:: xml 

    <bean id="documentPropertiesConfiguration" class="com.arondor.viewer.filenetce.config.DocumentPropertiesConfiguration">
    </bean> 

Include system metadata
-----------------------

By default, no system metadata is fetched. In order to force it, you need to add/edit *includedSystemProperties* property.

* Example ::

    <property name="includedSystemProperties">
        <list>
            <value>DateCreated</value>
            <value>DateLastModified</value>
            <value>Creator</value>
            <value>LastModifier</value>
        </list>
    </property>

Exclude custom metadata
-----------------------

By default, all custom metadata are fetched and displayed. In order to force exclusion of some ones, you need to add/edit *excludedCustomProperties* property

Example ::

    <property name="excludedCustomProperties">
        <list>
            <value>FactureRef</value>
        </list>
    </property>

**Nota** : If the following error appears: *No LoginModules configured for FilenetP8WSI*, an additional configuration is required:

 * Save the file :download:`jaas.conf.WebSphere </_static/docs/jaas.conf.WebSphere>` in a folder on the WAS server

 * Add a parameter to ARender's JVM:

    + Navigate to the menu *Server* and select the related server. Then open *Java and Process Management* and click on  *Process Definition*. In *Start command arguments* add the following argument: -Djava.security.auth.login.config=[Chemin_vers_fichier_jaas.conf.WebSphere]

From an user interface
======================

IBM Workplace & Workplace XT
----------------------------

In order to define which document types have to be opened within ARender, you need to edit the configuration file content-redir.properties (for Workplace XT, in folder: C:\Program Files\FileNet\Config\WebClient) as follow: 

    {mimeType}=/../ARender/ARender.jsp?{JSP_QUERY_STRING}

IBM Content Navigator
---------------------

A specific plugin has been implemented to integrate ARender within ICN.
Nota: ICN connector uses mixedObjects syntax.

Connect to Content Navigator.

Go to the 'Administration View' and click on 'Plug-ins'

.. image:: /_static/images/ICN_clickplugin_medium.png
    :align: center

Click on the button "New Plugin-in".

.. image:: /_static/images/ICN_newplugin_large.png
    :align: center

Enter the JAR file path and click on 'Load'.

Example:  *C:\\sources\\ARenderHMI\\arondor-arender-navigator-plugin-2.2.1.jar*

.. image:: /_static/images/ICN_pickjar_backgroundimage.png
    :align: center

Fill 'ARender context root' field with ARender's address (hots + port + context root). Like below:

.. image:: /_static/images/PluginContextRoot_en_backgroundimage.png
    :align: center

Click on the 'Save' button.

Click on Edit and check that the plugin is correctly installed.

.. image:: /_static/images/ICN_editplugin_backgroundimage.png
    :align: center

Map the new viewer.
Go to 'Viewer Maps'

.. image:: /_static/images/ICN_clickmaps_medium.png
    :align: center

The default map is called 'Default viewer map' and is not editable.
Click on it and then click on copy.

.. image:: /_static/images/ICN_copymap_backgroundimage.png
    :align: center

Click on "New Mapping".
Then select 'Filenet Context Manager' for the Repository type.
Then select ARenderPluginViewer in the list of viewer available.

.. image:: /_static/images/ICN_namemap_backgroundimage.png
    :align: center

You can now choose the MIME Types you want to open with ARender, then click on OK.

.. image:: /_static/images/ICN_mapmimes_backgroundimage.png
    :width: 90%
    :align: center

To use this Map, you just need to link it to a Desktop (Desktop tab -> Edit the desktop -> Select the Map in the Viewer Map list)

.. image:: /_static/images/ICN_linkdesktop_backgroundimage.png
    :align: center

Note
---------------------

If a popup login appears in ARender or in IBM Navigator when an ARender page is closed then an additional configuration is required, see below.
Change the name of ARender's cookie in WAS console from JESSIONID to JSESSIONARID (or the cookie name you want):

*Enterprise Applications > ARender [VERSION_NUMBER] for FileNet 5.x > Manage Modules > arondor-arender-hmi-filenet-[VERSION_NUMBER].war > Session management > Cookies*

.. image:: /_static/images/ICN_ARender_cookie_name.png
    :align: center
