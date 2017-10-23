-----------------------------
Rendition server installation
-----------------------------

Setup
=====

*Bold areas must be modified according to your versions / situations*

To launch installation wizard :

- Double clic on the executable jar file **as admin** : arondor-arender-rendition-service-**{VERSION-NUMBER}**.jar

- Or in console **admin mode** ::

    java –jar arondor-arender-rendition-service{VERSION-NUMBER}.jar

For an installation in console mode, execute below command ::

    java –jar arondor-arender-rendition-service{NUMÉRO-VERSION}.jar -console

For a silent installation, execute below command (link to the property file : :download:`installer.properties </_static/docs/installer.properties>`) ::

    java –jar arondor-arender-rendition-service{NUMÉRO-VERSION}.jar -options installer.properties

- The following window is displayed. Click on "Next":

.. image:: /_static/images/Welcome_highlighted.png
    :align: center

- Choose the installation folder and click on "Next":

.. image:: /_static/images/img2_highlighted.png
    :align: center

- In the window of components to install, click on "Next" to install default components

.. image:: /_static/images/img3_highlighted.png
    :align: center


- Once the rendition server installation is done , click on "Next":

.. image:: /_static/images/img4_highlighted.png
    :align: center

- Enter the configuration parameters corresponding to the environment.
    * Check "Run ARender as service" to launch ARender as a service.
    * When you do not want ARender as service, uncheck "Run as service"

         :ref:`Start the service manually <manualStart>`.


- Then click on "Next"

.. image:: /_static/images/img31_highlighted.png
    :align: center


Once configuration done, click on « Next ». If an error appears, refer to the :ref:`FAQ<FAQ>`.

.. image:: /_static/images/img6_highlighted.png
    :align: center

- Click on "Done" to finish the installation:

.. image:: /_static/images/img7_highlighted.png
    :align: center

