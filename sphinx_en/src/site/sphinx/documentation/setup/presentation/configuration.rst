------------------------
HMI server configuration
------------------------

Files in WEB-INF/classes
========================

*(the folder is located in your Tomcat, websphere, jetty or similar)*


    ================        ====================================================================================================================================================================================================================
    File name               Role and content
    ================        ====================================================================================================================================================================================================================
    arender.xml             Main configuration of ARender HMI application including rendition server access and connector (Cf. `Connectors <file:///C:/Users/A.%20BOUAZZAOUI/Desktop/sphinxHTML/connectors.html>`_.)
    ehcache.xml             Cache configuration of documents opened via the graphical interface
    log4j.properties        Application logs configuration
    Other files             Configuration of user profiles (cf. `Configuration guide <file:///C:/Users/A.%20BOUAZZAOUI/Desktop/sphinxHTML/guide_en.html>`_)
    ================        ====================================================================================================================================================================================================================


Rendition server definition
===========================

In order to define one or several rendition servers, edit the arender.xml configuration file as follow:

.. code-block:: xml

    <bean id="delegate" class="com.arondor.viewer.common.javarmi.ClientDocumentService" scope="singleton">
        <property name="maxTries" value="5" />
        <property name="remoteTargets">
        <list>
            <value>rmi://{rendition_server_1}:1789/JavaRMIDocumentService</value>
            <value>rmi://{rendition_server_2}:1789/JavaRMIDocumentService</value>
        </list>
        </property>
    </bean>



**Nota bene** : The value of the list in bold here has to be changed by the right rendition server address

*(Don't forget to reboot your HMI)*

Style sheet : ARender-default.css
=================================

Most of the ARender graphical components can be configured in the style sheet. Consult the file for more details.

**Nota bene** : This stylesheet is related to default user profile. See the  Configuration guide for more information.
