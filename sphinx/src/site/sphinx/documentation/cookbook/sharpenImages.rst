Obtenir des images moins lissées sur ARender
============================================

Par défaut, les navigateurs internet lissent les images afin de rendre les page web plus agréables à la consultation.

Si vous souhaitez retrouver un effet plus proche d'Adobe reader qui lui ne lisse pas les images, il est désormais possible dans ARender de ne pas activer ce lissage.

Le paramètre à changer est le suivant: 

*visualization.images.sharpen* et le placer à *true* dans les profils ARender.

Exemple avant sharpen : 

.. image:: /_static/images/blurry.png

Exemple avec sharpen : 

.. image:: /_static/images/unblurry.png

Comparaison avec le rendu adobe au même niveau de zoom:

.. image:: /_static/images/adobePixel.png

On voit bien que le rendu sharpen est fidèle au rendu Adobe. Si vos utilisateurs sont donc habitués à ce genre de rendus, vous pouvez songer à activer le paramètre. 