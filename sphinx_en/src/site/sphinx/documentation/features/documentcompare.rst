----------------------
Document comparison
----------------------


Compare two documents
=====================

Manual processing
-----------------

To do a comparison between two documents, right click on a document's thumb in the navigation panel and select \ *Open as new and compare*\ . 

.. image:: /_static/images/documentCompare1.png
    :align: center
    :width: 100%

The chosen document opens next to the current one, then the comparison results are displayed.

.. image:: /_static/images/documentCompare2.png
    :align: center
    :width: 100%

Automatic comparison on start up
--------------------------------

To automatically start the comparison after the application loading, use the following parameter : ::
	
	visualization.multiView.doComparison=true

The comparison will only be triggered if at least two documents are loaded.

The first document of these will be opened on the left and the second one on the right.


Close comparison mode
=====================

* To go back to the simple view mode, click on the red cross in the upper right corner of the document to close.

.. image:: /_static/images/documentCompare3.png
    :align: center
    :width: 100%

* It is also possible to close the comparison mode by right clicking on a document and select \ *Close multiView* \ . 

.. image:: /_static/images/documentCompare4.png
    :align: center
    :width: 100%


Parse comparison results
========================

Each difference type between two documents corresponds to a specific color :

+------------------------+------------------------------------+
|       Color            |   Meaning                          |
+========================+====================================+
|      Green             |  Added line                        |
+------------------------+------------------------------------+
|      Red               |  Removed line                      |
+------------------------+------------------------------------+
|      Grey              |  Modified line                     |
+------------------------+------------------------------------+
|      Orange            |  Modified text on a specific line  |
+------------------------+------------------------------------+

.. image:: /_static/images/documentCompare5.png
    :align: center
    :width: 100%


Browse results
==============

Navigate through results
------------------------

.. image:: /_static/images/documentCompare6.png
    :align: center

Clicking on the \ *Next result*\  or \ *Previous result*\  button will redirect to the closest one, regardless of the document.

.. image:: /_static/images/documentCompare7.png
    :align: center
    :width: 100%

Synchronized scroll between documents
-------------------------------------

The synchronized scroll function is enabled by default when a comparison is done.
It can be disabled using the corresponding button in the top panel.

Result's match
--------------

Clicking on a specific result redirects to the matching line on the other document. 

.. image:: /_static/images/documentCompare8.png
    :align: center
    :width: 100%


Comparison mode's specifications
================================

- The multi-view mode comes with the concept of current document which is defined has the last document hovered.
  
  This document is used for most of functionalities : Annotations, Download, Printing, Text searching, Page rotation, ...

- Document changing using navigation panel's thumbs is disabled.
  
  Only thumbs corresponding to documents currently opened in comparison mode allow to jump to the selected page on it.

How define the focus of document by click
=======================================

To define the focus of the document by click use the parameter : ::

	visualization.multiView.focusOnClick=true 
|