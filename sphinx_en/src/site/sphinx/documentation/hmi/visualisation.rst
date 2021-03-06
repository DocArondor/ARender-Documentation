Visualization
=============

* Key: *visualization*

    ==========================================================  ======================  ==================================
    Description                                                 Property key            Type
    ==========================================================  ======================  ==================================
    Visualization mode                                          mode                    Simple, BookMode        
    Fullscreen mode at startup                                  fullscreen              Boolean
    Activate save page rotation                                 rotation.save.enabled   Boolean
    Autoplay videos                                             video.autoplay          Boolean
    ==========================================================  ======================  ==================================

Zoom
------------

* Key: *zoom*

    ==========================================  =======================  ==================================    
    Description                                 Property key             Type
    ==========================================  =======================  ==================================    
    Zoom type                                   type                     FullWidth, FullHeight or FullPage
    Zoom value                                  value                    Integer (%)
    Enable zoom animation                       animation                Boolean                                   
    ==========================================  =======================  ==================================    


Page change
-----------

* Key: *pageChange*

    ==========================================================  ==================  ==================================
    Description                                                 Property key        Type
    ==========================================================  ==================  ==================================    
    Changement de page au *scroll* de la souris                 mouse               Boolean
    Activation de l'animation au changement de page             animation           Boolean
    ==========================================================  ==================  ==================================

* Key: *pageCorner*

    **Only when visualization.bookMode=true**
	
    ==========================================================  ==================  ==================================
    Description                                                 Key parameter       Type
    ==========================================================  ==================  ==================================    
    Activate page corners                                       enabled             Boolean
    Activate page corners animation                             animation           Boolean
    ==========================================================  ==================  ==================================


Guide ruler
-----------

* Key: *guideRuler*

    ==========================================================  ==================  ==================================
    Description                                                 Key parameter       Type
    ==========================================================  ==================  ==================================    
   	Activate guide ruler                                        enabled             Boolean
    Guide ruler height                                          height              Integer
    Guide ruler step                                            increment           Integer
    ==========================================================  ==================  ==================================


Multiview
---------

* Key: *multiview*

    ==========================================================  ==================  ==================================
    Description                                                 Key parameter       Type
    ==========================================================  ==================  ==================================    
   	Activate multiview                                          enabled             Boolean
    Multiview orientation                                       direction           vertical , horizontal
    Activate document compare                                   doComparison        Boolean
    Display multiview on startup                                showOnStart         Boolean
    Synchronized multiview scroll                               synchronized        Boolean
    Activate the focus of the document by click                 focusOnClick        Boolean
    Configure the time to hide the multiview header             header.timeoutMs    Long
    ==========================================================  ==================  ==================================
    