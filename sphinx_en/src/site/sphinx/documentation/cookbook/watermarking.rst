Watermarking documents
======================

This code snippet allows you, using the ARender jar dependency arondor-arender-client-javarest, to communicate with rendition servers in order generate PDFs with annotations.

In this particular example, we will setup a stamp annotation repeated on each page of the document in order to generate a watermarking. 

---------------
Variables setup
---------------

Here you will have to setup the address of the rendition server you are targeting and the binary content of the original document you want to watermark. We assume in this example that the data is stored into the field *data* .

.. code-block:: java

	DocumentServiceRestClient client = new DocumentServiceRestClient();
	client.setAddress("http://localhost:1990");
	// Assuming that this "data" contains your documentContent
	InputStream data;
	DocumentAccessor original = new DocumentAccessorByteArray(data);
    

-------------------------------
Loading of the documentAccessor 
-------------------------------

In this code, we load the documentAccessor and get the *RENDERED* version of it in case it needed a conversion on the rendition side. 

.. code-block:: java
    
    client.loadDocumentAccessor(original);
    DocumentAccessor accessorConverted = client.getDocumentAccessor(original.getUUID(),
            DocumentAccessorSelector.RENDERED);
            
-----------------------------
Obtaining the number of pages
-----------------------------

.. code-block:: java
            
    DocumentLayout layout = client.getDocumentLayout(accessorConverted.getUUID());
    int nbPages = -1;
    if (layout instanceof DocumentPageLayout)
    {
        nbPages = ((DocumentPageLayout) layout).getPageCount();
    }
    else
    {
        // send error 
        throw ...
    }

-------------------------------------
Setup the annotation style for stamps 
-------------------------------------

.. code-block:: java

    // configure here the ARender stamp style
    AnnotationStyle annotationStyle = new AnnotationStyle();

    annotationStyle.setFontSize(80);
    annotationStyle.setFontColor("rgb(0,0,255)");
    annotationStyle.setBackgroundColor("none");
    annotationStyle.setBorderWidth(0);
    Map<String, String> styleMap = new HashMap<String, String>();
    styleMap.put("fontSize", annotationStyle.getFontSize() + "");
    styleMap.put("fontColor", annotationStyle.getFontColor() + "");
    styleMap.put("borderWidth", annotationStyle.getBorderWidth() + "");
    styleMap.put("borderColor", annotationStyle.getBorderColor() + "");
    styleMap.put("backgroundColor", annotationStyle.getBackgroundColor() + "");
    String newAppearance = "";
    for (String key : styleMap.keySet())
    {
        newAppearance += key + ":" + styleMap.get(key) + ";";
    }
    // the appearance for the ARender stamp is now built


--------------------------------
Setup the list of stamps to send 
--------------------------------

.. code-block:: java

    // now we prepare the list of stamps to send the rendition server
    List<Annotation> stamps = new ArrayList<Annotation>();
    for (int i = 0; i < nbPages; i++)
    {
        StampElemType annotation = new StampElemType();
        annotation.setDocumentId(DocumentIdFactory.getInstance().generate());
        annotation.setContents("WATERMARK");
        annotation.setRotation(0);
        annotation.setPosition(new PageRelativePosition(0, 100, 400, 400));

        annotation.setAppearance(newAppearance);

        annotation.setPage(i);
        stamps.add(annotation);
    }


-------------------------------
Creation of the conversion task 
-------------------------------

.. code-block:: java

    AlterContentDescriptionWithAnnotations alterContent = new AlterContentDescriptionWithAnnotations();
    // set annotations
    alterContent.setAnnotations(stamps);
    // set documentId
    List<DocumentId> sourceDocumentIdList = new ArrayList<DocumentId>();
    sourceDocumentIdList.add(accessorConverted.getUUID());
    DocumentId renderedDoc = client.alterDocumentContent(sourceDocumentIdList, alterContent);


-------------------------------
Fetch of the resulting document 
-------------------------------


.. code-block:: java

    DocumentAccessor accessorFinalDocument = client.getDocumentAccessor(renderedDoc,
            DocumentAccessorSelector.RENDERED);
            
            
The binary data of the resulting document is in : 

.. code-block:: java

    accessorFinalDocument.getInputStream();
