
--------------
JavaScript API
--------------

Configuring a custom JavaScript file
====================================

The JavaScript custom file must contain a function such as: ::

    function arenderjs_init(arenderjs_){ ... }
    
This function is called by ARender at startup, the arenderjs_ argument is the JavaScript object collecting all the API functions, as provided by ARender.

You can configure the Javascript custom file to use within ARender by two different ways :

Using property arenderjs.startupScript
--------------------------------------

The property arenderjs.startupScript, if defined, will be used by ARender to fetch the custom Javascript file and execute it when the interface is ready.

This property can be set in the profile file, ::

    arenderjs.startupScript=scripts/myarenderscript.js
    
Or directly in the URL parameters: ::

    http://arender.arondor.com/ARender/ARender.jsp?url=http://arender.arondor.com/pdf/pdf/PDFReference15_v5.pdf&arenderjs.startupScript=scripts/arenderJSPAPITest.js

See the default profile jsapi-demo.properties (in the WEB-INF/classes folder of the ARender war) for an example profile.
Note that the JavaScript URL can be provided :

* as a relative URL: the URL is relative to the ARender HMI context root, for example http://arender.arondor.com/ARender
* as an absolute URL: in this case, beware that most modern browsers forbid having queries from multiple sources, because of the XSS limitations.

The "`Hollywood Principle <https://en.wikipedia.org/wiki/Hollywood_principle>`_ "
----------------------------------------------------------------------------------

The other option is to define the init function arenderjs_init() in ARender's parent context.
Consider ARender in a IFrame inclusion; the calling application creates an IFrame with an URL pointing to ARender.
In this case, the calling application only has to define the function :

    function arenderjs_init(arenderjs_){ ... }

ARender will look at this function in its parent context, and call it if it exists.

Using the Javascript API
=========================

Opening documents
---------------------

* Object: arender_js

    +-------------------------------------+-----------------------------------------------------------------------------------------+
    | Function                            | Description                                                                             |
    +=====================================+=========================================================================================+
    | loadDocument(url , callback)        | Loads a document providing an URL. It will provide an ARender Id back.                  |
    |                                     | Arguments:                                                                              |
    |                                     |  - the URL to open                                                                      |
    |                                     |  - the callback function to call when the Id is provided by the server.                 |
    |                                     | Note: This is purely a server-side operation, asynchronous at client side.              |
    +-------------------------------------+-----------------------------------------------------------------------------------------+
    | openDocument(id)                    | Opens a document.                                                                       |
    |                                     | Argument:                                                                               |
    |                                     | - id: ARender id                                                                        |
    +-------------------------------------+-----------------------------------------------------------------------------------------+
    | askChangePage(type , index)         | Changes the current page.                                                               |
    |                                     | Arguments:                                                                              |
    |                                     |  - type: 'Relative', 'Index' or 'Absolute'                                              |
    |                                     |  - index: -1 or 1 for relative or absolute; otherwise the page number                   |
    +-------------------------------------+-----------------------------------------------------------------------------------------+
    | enablePDFDocumentHyperlinks(boolean)| Activate/de-activate the internal hyperlinks of a document                              |
    |                                     | Arguments:                                                                              |
    |                                     |  - boolean : Load internal hyperlinks of a document if true, unload them otherwise.     |
    +-------------------------------------+-----------------------------------------------------------------------------------------+
    | disallowClickOnHyperlinks(boolean)  | Allow/disallow clicks on a document hyperlink for ARender                               |
    |                                     | Arguments:                                                                              |
    |                                     |  - boolean : if true, disallow internal hyperlinks of a document, allow them otherwise. |
    +-------------------------------------+-----------------------------------------------------------------------------------------+

* Example ::

    // Loads the PDF reference document
    getARenderJS().loadDocument("http://arender.arondor.com/pdf/pdf/PDFReference15_v5.pdf",
   function(id)
   {
       getARenderJS().openDocument(id);
   });

    // Move to page 24 (note that first page is called 0)
    getARenderJS().askChangePage('Index',23);

    // Move to last page
    getARenderJS().askChangePage('Absolute',1); 

Register to error events while loading documents
------------------------------------------------

* Object: arender_js

    +---------------------------------------------------+-----------------------------------------------------------------------------------------+
    | Function                                          | Description                                                                             |
    +===================================================+=========================================================================================+
    | registerNotifyLoadingErrorEvent(callback)         | Register a callback function that will be called when an error occurs when loading      |
    |                                                   | documents.                                                                              |
    |                                                   |  Arguments:                                                                             |
    |                                                   |  - the callback function to call when an error occur.                                   |
    +---------------------------------------------------+-----------------------------------------------------------------------------------------+

* Example ::

.. code-block:: javascript

    // Subscribe a function to the errors
    getARenderJS().registerNotifyLoadingErrorEvent(function(documentId,message) {console.log("error: "+message)});
    // Loads the PDF reference document
    // If an error occurs I am notified on the function defined before!
    getARenderJS().loadDocument("http://arender.arondor.com/pdf/pdf/PDFReference15_v5.pdf",
   function(id)
   {
       getARenderJS().openDocument(id);
   });
   

Know when ARender finished to load its modules
----------------------------------------------

* Object: arender_js

    +---------------------------------------------------+-----------------------------------------------------------------------------------------+
    | Function                                          | Description                                                                             |
    +===================================================+=========================================================================================+
    | registerAllAsyncModulesStartedEvent(callback)     | Register a callback function that will be called when ARender finishes loading its      |
    |                                                   | modules.                                                                                |
    |                                                   |  Arguments:                                                                             |
    |                                                   |  - the callback function to call when asynchronous modules are loaded.                  |
    +---------------------------------------------------+-----------------------------------------------------------------------------------------+

* Example ::

.. code-block:: javascript
	
	// Subscribe a function to the loading
    getARenderJS().registerAllAsyncModulesStartedEvent(function() {console.log("modules are loaded")});
    // When asynchronous modules are loaded I am notified on the function defined before!


Change zoom
-----------

* Object: getARenderJS().getZoomJSAPI()

    ===================================     =================================================
    Function                                Description          
    ===================================     =================================================
    askZoomIn()                             Zoom
    askZoomOut()                            Zoom out
    askZoomFullWidth()                      Zoom full width
    askZoomFullHeight()                     Zoom full height
    askZoomFullPage()                       Zoom full page: adapted to both width and height
    ===================================     =================================================
        
Change document builder
-----------------------

* Object: getARenderJS().getDocumentBuilder()

    ===================================     ===================================
    Function                                Description          
    ===================================     ===================================
    close()                                 Closes the document builder
    open()                                  Open the document builder
    reset()                                 Resets the document builder content
    ===================================     ===================================
        
Change the document navigator
-----------------------------

* Objet: getARenderJS().getThumbnailsJSAPI()

    ===================================     ===============================================================================
    Function                                Description          
    ===================================     ===============================================================================
    resetNavigator()                        Reset the document navigator size
    hideNavigator()                         Hide the document navigator
    showNavigator()                      	Show the document navigator
    expandNavigator(width)                  Enlarge the document navigator size (if width is superior to the current width)
    reduceNavigator(width)                  Reduce the document navigator size (if width is inferior to the current width)
    ===================================     ===============================================================================
    
    
Switch to Fullscreen
--------------------
    
* Object: getARenderJS().getFullScreenJSAPI()

    ===================================     ==================================
    Function                                Description          
    ===================================     ==================================
    askOpenFullScreen()                     Activate fullscreen mode
    askCloseFullScreen()                    Deactivate fullscreen mode
    ===================================     ==================================

Rotate pages
---------------------    
    
* Object: getARenderJS().getRotateJSAPI()

    ===================================     ==============================================
    Function                                Description          
    ===================================     ==============================================
    askRotateCurrentPageLeft()              Rotate current page left (counter-clockwise)
    askRotateCurrentPageRight()             Rotate current page right (clockwise)
    askRotateAllPageLeft()                  Rotate all pages of the current document left 
    askRotateAllPageRight()                 Rotate all pages of the current document right
    ===================================     ==============================================
    
Search features
---------------
    
* Object: getARenderJS().getSearchJSAPI() 

    ===================================     ======================================
    Function                                Description          
    ===================================     ======================================
    askSearchTextNext(word)                 Searching the next term : "word"

                                            Argument: 

                                              - word: The word to search
    askSearchTextPrevious(word)             Searching the previous term : "word"

                                            Argument: 

                                              - word: The word to search
    clearSearchResults()                    Clear current search results
    ===================================     ======================================

Download documents
------------------
    
* Object: getARenderJS().getDownloadDocumentJSAPI()  

    ===================================     ===============================================
    Function                                Description          
    ===================================     ===============================================
    askDownloadDocumentPDF()                Download the current document in PDF
    askDownloadDocumentSource()             Download the current document in source format
    askDownloadAllDocuments()               Download a single PDF with all opened documents
    ===================================     ===============================================

Intercept Hyperlinks
--------------------

* Object: getARenderJS().getAnnotationJSAPI()

Here is an example of JS code allowing to register a method that will be called each time that an hyperlink is clicked.


.. code-block:: javascript
    
    var arenderjs;
    function followLink(docId, pageNumber, destination, action)
    {
        alert("docId=" + docId + ", pageNumber=" + pageNumber + ", dest=" + destination + ", action=" + action);
        alert(arenderjs.getPropertyFromDestination(destination,"PAGE_TARGET"));
        alert(arenderjs.getPropertyFromAction(action,"GOTO"));
    }

    function arenderjs_init(ajs) 
    {
        ajs.onAnnotationModuleReady(function(annotjs)
                {
                    arenderjs=annotjs;
                    annotjs.registerFollowLinkHandler(followLink); 
                    console.log(arenderjs.getDestinationTypes().b);
                    console.log(arenderjs.getActionTypes().b);
                });
    }

In this example, you can also observe how to visualize all properties existing in hyperlinks.

*arenderjs.getDestinationTypes().b* and *arenderjs.getActionTypes().b* contains the list of properties that can be asked for hyperlinks destinations and actions. 

*arenderjs.getPropertyFromDestination(destination,property)* and *arenderjs.getPropertyFromAction(action,property)* allow to ask for a particular property once the action or destination have been received.

You will find follwing the list of properties for *destinations* and *actions* :

.. code-block:: java

    
    public static enum DestinationTypes
    {
        PAGE_TARGET, NAMED_DESTINATION, GOTO_DESTINATION, URI, BOTTOM_POSITION, TOP_POSITION, LEFT_POSITION, RIGHT_POSITION, INCORRECT_SYNTAX;
    }

    public static enum HyperlinkActionTypes
    {
        REMOTE_GOTO, LAUNCH, GOTO, NAMED, URI, JAVASCRIPT, NONE, FILE_SPECIFICATION, WIN_LAUNCH_PARAMS, INCORRECT_SYNTAX;
    }

Actions indicate which type of fileds you will find in the destination. A *GOTO* will contain a page, and can contain coordinates (coordinates will be equal to -1 if not existing). An *URI* action will mean that the destination will contain an *URI* address to go to.


Setup plugin events and plugin parameters
-----------------------------------------
 
* Object: getARenderJS()

    ========================================     =============================================================================================
    Function                                     Description          
    ========================================     =============================================================================================
    preparePluginEvent(key,value,pluginName)      Insert a (Key,Value) couple in the target URL of the next plugin Event of name pluginName
    clearPluginEvent(pluginName)                  Clear all couple (Key,Value) stored in for the name pluginName
    openPlugin(pluginName,openInMultiView)        Open the plugin pluginName in ARender, in multiView or not with the boolean openInMultiView
    ========================================     =============================================================================================
    
Those functions allow to prepare an event before opening the plugin in order to setup a correct URL for parameterizing the plugin from ARender ahead of time.

.. code-block:: javascript

    function arenderjs_init(ajs) 
    {
    	// this line prepare an URL such as http://plumeURL/?To=toto@tutu.com
        ajs.preparePluginEvent("To","toto@tutu.com","plume");
     	// Here, we clear all stored values for this plugin, can be useful if called from a "clear" button
        ajs.clearPluginEvent("plume");
    }