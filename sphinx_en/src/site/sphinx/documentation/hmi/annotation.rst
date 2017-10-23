Annotations
===========

* Key: *annotation*

    ===================================================  =======================  =========
    Description                                          Parameter Key            Type
    ===================================================  =======================  =========
    Automatic save mode                                  autosave                 Boolean
    Load existing annotations                            loadExisting             Boolean
    Display loading GIF when saving annotations          loadingGIF               Boolean
    Include annotation textual content when searching    searchTextInAnnotations  Boolean
    ===================================================  =======================  =========

* Example ::

    // Enable autosave mode
    annotation.autosave=true
   
Sticky Note
-----------
  
* Key: *annotation.stickyNote*


    ======================================  ==================  =========
    Description                             Parameter Key       Type
    ======================================  ==================  =========
    Opacity                                 opacity             Boolean
    Minimum width                           minimum.width       Integer
    Minimum height                          minimum.height      Integer
    Background color                        default.color       String
    Font size                               default.fontSize    Integer
    Default font                            default.font        String
    Underlined text                         default.underline   Boolean
    Bold text                               default.bold        Boolean
    Italic text                             default.italic      Boolean
    Hide border                             hide.border         Boolean
    Hide details about sticky note          hide.details        Boolean
    ======================================  ==================  =========

    
Rectangle
---------
  
* Key: *annotation.rectangle*

    ======================================  ====================  =========
    Description                             Parameter Key         Type
    ======================================  ====================  =========
    Opacity                                 opacity               Float
    Minimum width                           minimum.width         Integer
    Minimum height                          minimum.height        Integer
    Background color                        default.color         String
    Border color                            default.border.color  String
    Border width                            default.border.width  Integer
    ======================================  ====================  =========

Circle
------
  
* Key: *annotation.circle*

    ======================================  ====================  =========
    Description                             Parameter Key         Type
    ======================================  ====================  =========
    Opacity                                 opacity               Float
    Minimum width                           minimum.width         Integer
    Minimum height                          minimum.height        Integer
    Background color                        default.color         String
    Border color                            default.border.color  String
    Border width                            default.border.width  Integer
    ======================================  ====================  =========
    
Highlight, strikeout and underline text
---------------------------------------
  
* Key: *annotation.highligthtext*

    ======================================  ==================  =========
    Description                             Parameter Key       Type
    ======================================  ==================  =========
    Opacity                                 opacity             Float
    ======================================  ==================  =========

Obfuscate
---------

     ======================================  ===========================  =========
     Description                             Parameter Key                Type
     ======================================  ===========================  =========
     Allow hiding obfuscate                  annotation.canHideObfuscate  Boolean
     Lock obfuscate                          toolbar.lockedObfuscate      Boolean
     ======================================  ===========================  =========
    
Polygon
-------
  
* Key: *annotation.polygon*

    ======================================  ====================   =========
    Description                             Parameter Key          Type
    ======================================  ====================   =========
    Opacity                                 opacity                Float
    Background color                        backgroundColor        String
    Border width                            width                  Float
    ======================================  ====================   =========

Polyline
--------
  
* Key: *annotation.polyline*

    ======================================  ====================  =========
    Description                             Parameter Key         Type
    ======================================  ====================  =========
    Opacity                                 opacity               Float
    Background color                        backgroundColor        String
    Border width                            width                 Float
    ======================================  ====================  =========

Freehand
--------
  
* Key: *annotation.ink*

    ======================================  ====================  =========
    Description                             Parameter Key         Type
    ======================================  ====================  =========
    Opacity                                 opacity               Float
    Background color                        backgroundColor       String
    Border width                            width                 Float
    ======================================  ====================  =========
            
Arrow
-----
  
* Key: *annotation.arrow*

    ======================================    ==================    ======================================
    Description                               Parameter Key         Type
    ======================================    ==================    ======================================
    Background color                          backgroundColor       String (RGB or hexadecimal format)
    Compute the arrow size                    computeDistance       Boolean
    ======================================    ==================    ======================================
    
Information popup
-----------------

This part concerns the popups which display annotation information on mouse over.
  
* Key: *annotation.info.popup*

    ====================================================  ==================  =========
    Description                                           Parameter Key       Type
    ====================================================  ==================  =========    
    Enable / disable popup                                enabled             Boolean
    Display the popup even if the annotation is editable  evenIfEditable      Boolean
    Display information about last update                 displayUpdate       Boolean
    ====================================================  ==================  =========

---------------------------
Per page annotation loading
---------------------------

If the connector implements the Interface *AnnotationPageAccessor*, annotations can be loaded on a per page basis in ARender version 3.1.0+.

In order to use this feature activate this parameter : 

* annotation.loadPerPage=true


The signature of the interface is the following: 

.. code-block:: java

    List<Annotation> get(int page) throws AnnotationsNotSupportedException, AnnotationCredentialsException, InvalidAnnotationFormatException;

The connector will have to make use of buffers/per page access to the backend annotation storage in order to benefit fully from this feature.

