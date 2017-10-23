-------------
Manual launch
-------------

**If ARender isn't installed as a service, There are two possibilities to launch ARender Rendition service :**

 * Manual installation of ARender Rendition service on Windows.

 * Manual launch without installation of ARender Rendition service.

Manual installation of ARender Rendition service on Windows
===========================================================

* Go in "bin" folder of ARender installation folder (by default : C:\Program Files\ARender-{**VERSION-NUMBER**}\bin):

.. image:: /_static/images/img11.png
    :align: center

* Double click on InstallService-ARenderServer.bat to make available the rendition server.

* Check the service is well installed and launch the service

.. image:: /_static/images/img12.png
    :align: center

.. _manualStart:

Manual launch without installation of ARender Rendition service
=================================================================

It's possible to launch ARender Rendition service manually via command line :

* On Windows with **ARenderServer.bat** located in folder ARender-Rendition-**{NUMÉRO-VERSION}**\bin : ::

    C:\Program Files\ARender-Rendition-{VERSION-NUMBER}\bin> ARenderServer.bat

* On Linux with **ARenderServer-Console.sh** located in folder ARender-Rendition-**{NUMÉRO-VERSION}**/bin : ::

    ~/ARender-Rendition{VERSION-NUMBER}/bin/ARenderServer-Console.sh

