Managing rejected documents causing errors in the rendition server
==================================================================

This guide aims at explaining you the configuration of erroneous document handling by the rendition server. 

XML configuration of the error handling mechanism
-------------------------------------------------


In the arender-rendition.xml file, remove the comments around the following XML block in order to activate the erroneous document handling:

.. code-block:: xml

    <!-- Copy all documents with errors to the rejected path -->
    <property name="rejectedDocumentsPath">
        <value>${rendition.dir.rejected.documents}</value> 
    </property>

This feature places each erroneous document into a specific folder configured by the parameter "rendition.dir.rejected.documents" in your arender-rendition.properties file. 


XML configuration of the remplacement picture
---------------------------------------------

It is also possible to configure a picture that takes place of the erroneous document faulty content. May it be a single page of the document of the entire document, the replacement picture replaces all errors.

The configuration of this picture is also done in the arender-rendition.xml file by uncommenting the following block:

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

The parameter "default.rejected.file" points to the picture that will replace the faulty contents and is defined in arender-rendition.properties. The title that will be displayed for the picture and its dimensions are defined in the xml block directly.