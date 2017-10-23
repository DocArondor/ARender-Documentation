----------
Hyperlinks
----------

* Key: hyperlinks  

    ==================================================   ========================  ========
    Description                                          Parameter Key             Type    
    ==================================================   ========================  ========
    Load URLs into the ARender frame                     hyperlinks.loadInARender  Boolean
    Load hyperlinks from the source document             hyperlinks.loadFromPDF    Boolean
    Allow internal hyperlinks from the source document   hyperlinks.load.internal  Boolean
    Allow external hyperlinks from the source document   hyperlinks.load.external  Boolean
    ==================================================   ========================  ========

These parameters allow to influence of the behavior associated with internal hyperlinks stored into source documents. 
If you do not wish to have the internal links of a PDF to be displayed or clicked, use the parameter *hyperlinks.loadFromPDF=false*. 