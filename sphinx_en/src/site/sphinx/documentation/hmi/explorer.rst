------------------
Document navigator
------------------

* Key: documentnavigator

    =============================   ===============  ========
    Description                     Parameter Key    Type    
    =============================   ===============  ========
    Width of document navigator     width            Pixels  
    =============================   ===============  ========

Thumb explorer
==============

The table below lists the general configuration of the explorer allowing to browse into documents through thumbs.

* Key: thumbexplorer

    =======================================================  ===============  =========
    Description                                              Parameter Key    Type    
    =======================================================  ===============  =========
    Enable/disable the explorer                              enabled          Boolean 
    Indentation between a master document and its children   indentation      Pixels  
    Depth level of documents to load                         maxLevelToLoad   Integer 
    Enable/disable metadata display                          metadata         Boolean 
    =======================================================  ===============  =========

* Example ::

    // Disable the thumb explorer
    thumbexplorer.enabled=false

The table below enumerates specific configuration related to thumbs.

* Key: thumbexplorer.thumb

    ===============================================  ===============  =========
    Description                                      Parameter Key    Type    
    ===============================================  ===============  =========
    Default width of the thumbs                      width            Pixels  
    Margin between each thumb                        margin           Pixels  
    Explorer width from which thumbs are expanded     grow.min         Pixels
    Increment of thumb expanding                     grow.increment   Pixels  
    NA                                               grow.ratio       Integer 
    ===============================================  ===============  =========

* Example ::

    // Define an explorer whose thumbs are expanded when it is maximized by a user
    thumbexplorer.thumb.width=100
    thumbexplorer.thumb.margin=200
    thumbexplorer.thumb.increment=10

Annotation explorer
====================

* Key: annotationexplorer
    
    =====================================================   =====================   ===========
    Description                                             Property key            Type    
    =====================================================   =====================   ===========
    Enable/Disable this explorer                            enabled                 Boolean    
    Display Sticky note answer                              showStickyNoteReplies   Boolean
    Display Sticky note label before content                showStickyNoteLabel     Boolean
    Adapt explorer size to fit to the annotation table      adaptiveWidth.enabled   Boolean
    =====================================================   =====================   ===========

* Example ::

    annotationexplorer.enabled=false
    annotationExplorer.showStickyNoteReplies=false
    annotationExplorer.showStickyNoteLabel=true
    annotationExplorer.adaptativeWidth.enabled=false
    
Bookmark explorer
=================

* Key: bookmarkexplorer
    
    ==============================================   ===============   ========
    Description                                      Parameter Key     Type     
    ==============================================   ===============   ========
    Enable/Disable this explorer                     enabled           Boolean  
    ==============================================   ===============   ========
    
* Example ::

    // Disable the bookmark explorer
    bookmarkexplorer.enabled=false
