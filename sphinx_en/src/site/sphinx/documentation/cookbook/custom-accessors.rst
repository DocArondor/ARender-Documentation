Create your own document accessor in ARender
============================================

Depending the kind of service you want to use, we might already have something in-house so don't hesitate to come back to us with the decided service that will be used to fetch documents.

If you prefer to directly go and implement your custom integration for fetching documents, there will be two things to do :

An URL parser, that will load the parameters you need from the URL and create the second component needed, what we call a document accessor.

http://arender.fr/rendition-api/com/arondor/viewer/rendition/api/DocumentServiceURLParser.html

The method canParse has to return true if the parameters in the URL of ARender are sufficient to parse the document.

The method parse will parse the parameters contained in the URL and push the documentAccessor to the rendition server. Example:

.. code-block:: java

	List<DocumentIdParameter> parameters = new ArrayList<DocumentIdParameter>();
	parameters.add(new URLDocumentIdParameter(URL_REQUEST_PARAMETER, url));
	DocumentId documentId = DocumentIdFactory.getInstance().generate(parameters);
	DocumentAccessor documentAccessor = new DocumentAccessorURL(url, documentId);
	documentService.loadDocumentAccessor(documentAccessor);
	return documentAccessor.getUUID();

Here, instead of DocumentAcessorURL, you'll put your own custom DocumentAccessor.

http://arender.fr/rendition-api/com/arondor/viewer/rendition/api/document/DocumentAccessor.html

The methods detailed in the documentation are very straightforward and should not cause you any implementation issues.

Once you developed your couple Parser/Accessor you'll be able to add the parser in the file arender.xml contained in WEB-INF/classes


.. code-block:: xml

	<property name="registeredURLParsers">
		<list>
			<bean class="full.class.name.here.YourCustomURLParser" />
			<bean
				class="com.arondor.viewer.server.servlet.urlparser.FallbackURLParser" />
		</list>
	</property>

In the case of creating a custom Accessor/URLParser we recommend you strongly to make a Maven project and use an XSLT processor in order to overlay and modify the XML of the default ARender war properly each version.
