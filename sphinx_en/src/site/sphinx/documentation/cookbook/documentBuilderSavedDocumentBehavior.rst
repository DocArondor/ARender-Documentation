Save new documents with ARender
===============================

---------------------------------------------------
Configure ARender saving policy for built documents
---------------------------------------------------

Prerequisite
------------
Below you will find a configuration with properties modification.

Be sure to read the chapter *HMI configuration guide* before.

Moreover, in order to save new document with ARender you need to activate the documentBuilder functionality as below:

* **documentbuilder.enabled=true**

Tutorial for ARender versions strictly lower than 3.1.4
-------------------------------------------------------
It is possible to define different behaviors at the save of a built document.

Below, the properties to modify:

* **documentbuilder.save.behavior=UPDATE_NO_DOCUMENT**
Role: behavior to adopt at the save.

Possible values:

    CREATE_NEW_FIRST_DOCUMENT: a new document is created in the EDM.

    UPDATE_FIRST_DOCUMENT: a new version of the document is created in the EDM.

    UPDATE_NO_DOCUMENT: no action on the EDM side.

* **documentbuilder.save.download=true**
Role: Activate/deactivate document download on client side.

Possible values: true/false.

Tutorial for ARender versions 3.1.4 and higher
----------------------------------------------
It is possible to show different buttons having specific behavior at document save.

Below, the properties to modify:

* **documentbuilder.button.legacySave.enabled=true**
Role: get back to the legacy behavior of pre 3.1.4 ARender versions (see `Tutorial for ARender versions strictly lower than 3.1.4`_).

Possible values: true/false.

* **documentbuilder.button.download.enabled=true**
Role: Activate/deactivate the download button of a built document on the client side.

Possible values: true/false.

* **documentbuilder.button.createFirst.enabled=true**
Role: Activate/deactivate the button that create a new document in the EDM corresponding to the built document.

Possible values: true/false.

* **documentbuilder.button.updateFirst.enabled=true**
Role: Activate/deactivate the button that create a new version of the document in the EDM corresponding to the built document.

Possible values: true/false.