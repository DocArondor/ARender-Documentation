---------------------
HMI server deployment
---------------------

Jetty deployment
================

* Get "jetty-runner-**{VERSION-NUMBER}**.jar"
* Get "arondor-arender-hmi-**{VERSION-NUMBER}**.war"
* Move those files to a folder (example : "C:\ARender")

Once files have been stored:

* Open the console and type: ::

    cd C:\ARender

By default, the file to modify is:

* arender.xml : if the rendition server is installed on another server than HMI one or if it use another port than default one (1789), and/or if the Content Engine is on another server than the HMI one or if it use another port than the default one (2809).

* To extract and modify these files, in a console, type the following command: ::

    java -jar jetty-runner-{VERSION-NUMBER}.jar arondor-arender-hmi-{VERSION-NUMBER}.war

.. image:: /_static/images/img15_highlighted.png
    :align: center

Webpshere deployment
====================

* Open a WebSphere console (« https://serveur_websphere:9043/ibm/console »)

.. image:: /_static/images/img19_highlighted.png
    :align: center
    :width: 100%

* Go in tab "Applications", then click on "Enterprise applications"

.. image:: /_static/images/img20_highlighted.png
    :align: center
    :width: 100%

* To launch installation, click on "Install"

.. image:: /_static/images/img21_highlighted.png
    :align: center
    :width: 100%

* Choose the EAR path to deploy and click on "Next"

.. image:: /_static/images/img22_highlighted.png
    :align: center
    :width: 100%

* To accept default parameters, click on "Next"

.. image:: /_static/images/img23_highlighted.png
    :align: center
    :width: 100%

* Select webserver(s) and/or server(s) of the Workplace, then click on "Next"

.. image:: /_static/images/img24_highlighted.png
    :align: center
    :width: 100%

* To accept the parameters by default (virtual host : default_host), click on "Next"

.. image:: /_static/images/img25_highlighted.png
    :align: center
    :width: 100%

* In recap window, click on « Finish » to begin the installation with these parameters after checking them

.. image:: /_static/images/img26_highlighted.png
    :align: center
    :width: 100%

* Click on "save" to finish the installation

.. image:: /_static/images/img27_highlighted.png
    :align: center
    :width: 100%

* Start "ARender HMI" selecting it and clicking on "Begin"

.. image:: /_static/images/img28_highlighted.png
    :align: center
    :width: 100%

* To test if the deployment is OK, load the default document in ARender by typing the following address in your browser: http://[ARENDER_HOST]:[ARENDER_PORT]/ARender (for example: http://localhost:8080/ARender).

**Careful with class loading order**

Websphere must be configured in parent-last which means it has to load its libraries after ARender.

How to check this parameter:

Procedure:

For all Websphere versions:

* In the application list click on ARenderHMI
* Click on "Class loading and update detection"
* Select "Classes loaded with local class loader first (parent last)"

.. image:: /_static/images/ChargementClasse_ParentLast_large.png
    :align: center
    :width: 100%

* Click on "OK"

Then, for Websphere version above 8:

* In the application list click on ARenderHMI
* Click on "Manage Modules"
* Click on ARender module
* Select in the drop down list

.. image:: /_static/images/DernierParent_large.png
    :align: center
    :width: 100%

* Click on "OK"

Note:

When deploying ArenderHMI on WebSphere Application Server, do not use the same profile (jvm) for ArenderHMI and IBM Content Navigator.

Thus, you will need to configure LTPA in order to enable session sharing between IBM Content Navigator and ArenderHMI :

I) If LTPA has already been configured, skip to "Importing LTPA keys". Otherwise, export the keys :

1. In WebSphere Administration Console, navigate to **Security** > **Global Security**, under **Authentication**, click **LTPA**



.. image:: /_static/images/Configuration-LTPA_highlighted.png
    :align: center
    :width: 100%

2. Specify a password, a filepath, and click "Export keys"

.. image:: /_static/images/Export-LTPA-key_highlighted.png
    :align: center
    :width: 100%

3. Once successfully exported, import the keys (you just exported) in the current profile
4. Save the modifications
5. Restart the profile

2) Copy the file containing the keys to the ArenderHMI Server

3) Import the keys in the ARenderHMI profile

1. Using the WebSphere Administration Console, navigate to **Security** > **Global Security**, under **Authentification**, click **LTPA**

.. image:: /_static/images/Configuration-LTPA_highlighted.png
    :align: center
    :width: 100%

2. Fill in the same password you entered when exporting the keys
3. Specify the path where you copied the keys
4. Click Import keys
5. Save the modifications
6. Restart the profile

--------------
Using EARMaker
--------------

**Setup for the HMI Server using EARMaker**

**Method :**

* Get the EAR « arondor-arender-hmi-filenet-**{VERSION-NUMBER}**.ear »
* Get the tool « earmaker-X-jar-with-dependencies.jar »
* Move these jar in a folder (example : « C:\ARender »)

.. image:: /_static/images/img16.png
    :align: center

* Open a cmd to open the folder " cd C:\\ARender "
* By default, the file to modify is: **arender.xml**, if the rendition server is installed on another server than HMI one or if it use another port than default one (**1789**), and/or if the Content Engine is on another server than the HMI one or if it use another port than the default one (**2809**).
* Open the console and go in the folder where jar files are.
* To extract and modify these files, in a console, type the following command ::

    java –jar earmaker-X-jar-with-dependencies.jar  –f (arender.xml,WcmApiConfig.properties) –s arondor-arender-hmi-filenet-{VERSION-NUMBER}.ear –t extraction

.. image:: /_static/images/img17.png
    :align: center


* In the extraction folder (« C:\\ARender\\extraction »), modify the concerned files (the ones given in the command).
* To include modified files in final EAR, in the console, type: ::

    java –jar earmaker-X-jar-with-dependencies.jar  –m extraction –s arondor-arender-hmi-filenet-{VERSION-NUMBER}.ear –t arondor-arender-hmi-filenet-{VERSION-NUMBER}-earmaker.ear »

.. image:: /_static/images/img18.png
    :align: center

* The EAR is rebuilt and located in the folder « C:\\ARender ».
