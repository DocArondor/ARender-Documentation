Microsoft Office documents conversion using ARender
===================================================

This tutorial describe an example of usage of ARender to convert a Word document into a PDF. In order to do so, we are going to explore the API used to connect to the rendition server. 

-------------
Configuration
-------------

Maven configuration
```````````````````

Before everything, we need to import the ARender maven dependencies that are needed for this example. In the case of a maven project, it is sufficiant to add this to the pom.xml file:

.. code-block:: xml

	<dependency>
	       <groupId>com.arondor.arender</groupId>
	       <artifactId>arondor-arender-common</artifactId>
	       <version>ARender_version</version>
	       <type>jar</type>
	       <scope>compile</scope>
	</dependency>
	<dependency>
	       <groupId>com.arondor.arender</groupId>
	       <artifactId>arondor-arender-client-javarmi</artifactId>
	       <version>ARender_version</version>
	       <type>jar</type>
	       <scope>compile</scope>
	</dependency>

Document service configuration
``````````````````````````````
  
This first step defines the necessary information for the usage of the API. The object DocumentService encapsulate the communication between the HMI and the rendition server. (that can be remote)

.. code-block:: java
	
	ClientDocumentService clientDocumentService = new ClientDocumentService();
	clientDocumentService.setRemoteTarget("rmi://localhost:1789/JavaRMIDocumentService");
	clientDocumentService.setMaxTries(3);

----------------
Document loading
----------------

In order to load the document on the rendition server, we can call loadDocumentAccessor(DocumentAccessor documentAccessor) of the DocumentService interface. In this exemple, we give a documentAccessor built from an inputStream containing the content of the document.

.. code-block:: java

	String fileToConvertPath = "C:\\ARender_User\\Documents\\myWordDocument.docx";
	FileInputStream fileInputStream = new FileInputStream(fileToConvertPath);
	DocumentAccessor documentAccessor = new DocumentAccessorByteArray(fileInputStream);
	clientDocumentService.loadDocumentAccessor(documentAccessor);

Fetching the converted document
-------------------------------

Au sein d’un serveur de rendition, un document peut se trouver dans différents états. Dans cet exemple, les états qui nous intéressent sont :
Into the rendition server, a document can be stored in different states. In this example, those are the states : 

*Initial* : Corresponds to the document pushed in its initial state, without treatment from the rendition server.
*Rendered* : Correspond to the document once it has been converted/processed by the rendition server, this is the document we want to fetch.
Therefore, different accessors, implementing the interface DocumentAccessor, are stored allowing to access different states of a same document. The enumration DocumentAccessorSelector allows to fetch the appropriate DocuementAccessor.

.. code-block:: java
	
	DocumentAccessor renderedDocumentAccessor = clientDocumentService.getDocumentAccessor(documentAccessor.getUUID(),DocumentAccessorSelector.RENDERED);
	InputStream pdfDocumentInputStream = renderedDocumentAccessor.getInputStream();
