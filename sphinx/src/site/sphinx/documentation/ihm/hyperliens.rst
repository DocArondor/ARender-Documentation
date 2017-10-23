----------
Hyperliens
----------

* Key: hyperlinks  

    ==============================================================   ========================  ========
    Description                                                      Clé du paramètre          Type    
    ==============================================================   ========================  ========
    Charger les URLs des hyperliens dans le fenête ARender           hyperlinks.loadInARender  Booléen
    Charger les hyperliens contenus dans les documents               hyperlinks.loadFromPDF    Booléen
    Autoriser les hyperliens ayant des cibles internes au document   hyperlinks.load.internal  Booléen
    Autoriser les hyperliens ayant des cibles externes au document   hyperlinks.load.external  Booléen
    ==============================================================   ========================  ========

Ces paramètres permettent d'influencer sur le comportement associé avec les hyperliens internes, stockés dans les documents source.
Si vous ne voulez pas que les hyperliens soient clickable ou visibles, utilisez le paramètre *hyperlinks.loadFromPDF=false*.
  