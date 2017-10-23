--------
Menu bar
--------

Logo
====

* Key: topPanel.logo

    ========================     ======================     ==============
    Description                  Parameter Key              Type
    ========================     ======================     ==============
    The URL of the image         url                        String
    The image width              width                      Integer
    The image height             height                     Integer
    The image margin left        margin.left                Integer
    ========================     ======================     ==============
    
* Example ::

    // Change ARender logo for my company's one
    topPanel.logo.url=http://www.mycompany.com/logos/logo.svg
    topPanel.logo.width=100
    topPanel.logo.height=40
     
    // Hide the logo
    topPanel.logo=false

Document menu
=============

* Key: topPanel.documentMenu

    ==================================================================     =============================   ==============
    Description                                                            Parameter Key                   Type
    ==================================================================     =============================   ==============
    Upload a document from local disk                                      upload                          Boolean
    Upload a document from a remote URL                                    url                             Boolean
    Upload XFDF annotations from local                                     xfdfUpload                      Boolean
    Download current document in PDF                                       downloadPDF                     Boolean
    Download current document in native format (only not PDF document)     download                        Boolean
    Download all visualized documents                                      downloadAll                     Boolean
    Download current document with its annotations                         downloadAnnotation              Boolean
    Download annotations in CSV format                                     downloadCSVAnnotation           Boolean
    Download document with  FDF  annotations                               downloadWithFDFAnnotation       Boolean
    Download annotations in XFDF format                                    downloadXFDFAnnotations         Boolean
    ==================================================================     =============================   ==============

* Example ::

    // Prevent any possibility to download a document via the menu bar
    topPanel.documentMenu.download=false
    topPanel.documentMenu.downloadPDF=false
    topPanel.documentMenu.downloadAll=false
    // If the downloadAll mode does not work because of a document blocking the download process (erroneous document) modify the bean delegate of arender.xml
    <property name="ignoreDocumentAccessorsWithExceptions" value="false" />
    // with
    <property name="ignoreDocumentAccessorsWithExceptions" value="true" />
    

Print menu
==========

* Key: topPanel.print

    ============================================================    =========
    Description                                                     Type
    ============================================================    =========
    Display a dialog box allowing to choose the type of printing    Boolean
    ============================================================    =========

* Example :: 

    // Hide the print button
    topPanel.print=false

Annotation menu
===============

* Key: topPanel.annotationMenu

    ====================================  ==================   =========
    Description                           Parameter Key        Type    
    ====================================  ==================   =========
    Create a sticky note                  stikyNote            Boolean 
    Create a rectangle                    highlight            Boolean 
    Create a circle                       circle               Boolean 
    Create an arrow                       arrow                Boolean 
    Create a highlight text               highlightText        Boolean 
    Create an underline text              underlineText        Boolean 
    Create a strikeout text               strikethroughText    Boolean 
    Create a polygon                      polygon              Boolean 
    Create a polyline                     polyline             Boolean 
    Create a freehand                     freehand             Boolean 
    Create a stamp                        stamp                Boolean 
    Display/hide all annotations          hide                 Boolean 
    Display/hide annotations & rotations  hideAll              Boolean 
    ====================================  ==================   =========


* Example ::

    // Display sticky note creation button
    topPanel.annotationMenu.stickyNote=true
    // Hide arrow creation button,
    topPanel.annotationMenu.arrow=false

Navigation
==========

* Key: topPanel.pageNavigation

    ===============================   ================   =========
    Description                       Parameter Key      Type
    ===============================   ================   =========
    Go to first page                  first              Boolean 
    Go to previous page               previous           Boolean 
    Go to next page                   next               Boolean 
    Go to last page                   last               Boolean 
    ===============================   ================   =========

* Example ::

    // Hide buttons to go to first and last pages
    topPanel.pageNavigation.first=false
    topPanel.pageNavigation.last=false
    
Zoom
====

* Key: topPanel.zoom

    =====================================================   ================   ==========
    Description                                             Parameter Key      Type    
    =====================================================   ================   ==========
    Zoom in                                                 in                 Boolean 
    Zoom out                                                out                Boolean 
    Zoom on a selected zone                                 zone               Boolean 
    Adjust the zoom to the window width                     fullWidth          Boolean 
    Adjust the zoom to the window height                    fullHeight         Boolean 
    Adjust the zoom to both the window width and height     fullPage           Boolean 
    Enable zone zoom in external window                     zoneGlass          Boolean
    Zone zoom multiplication                                zoneGlass.value    Integer
    =====================================================   ================   ==========
    
* Example ::

    // Hide the button allowing to enable zonal zoom
    topPanel.zoom.zone=false
    
Rotation
========

* Key: topPanel.rotation

    =========================================   =============   ========
    Description                                 Parameter Key   Type    
    =========================================   =============   ========
    Rotate current page to the right            right           Boolean 
    Rotate current page to the left             left            Boolean 
    Rotate all pages to the left and right      all             Boolean 
    =========================================   =============   ========
    
* Example ::

    // Disable rotation buttons
    topPanel.rotation.right=false
    topPanel.rotation.left=false 
    
Other features
==============

* Key: topPanel

    ======================================   ================   =========
    Description                              Parameter Key      Type    
    ======================================   ================   =========
    Create an obfuscate text                 obfuscate          Boolean 
    Refresh annotations                      refresh            Boolean 
    Full text search                         search             Boolean 
    Fullscreen mode                          fullscreen         Boolean 
    ======================================   ================   =========
    