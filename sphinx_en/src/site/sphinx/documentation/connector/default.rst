-------
Default
-------

This connector is provided as default. It is used for internal product mechanism. For these purposes, it can be used with following URL parmaters: 

    ===================================      ====================================================
    Parameter                                Description          
    ===================================      ====================================================
    url                                      Allow to supply a URL based on HTTP or FTP protocol
    uuid                                     Used to visualize the id of a ARender document
    bean                                     Specify use of a specific connector (Advanced level)
    ===================================      ====================================================

* Example ::

    Open a WEB document
    http://arender.arondor.com/ARender/ARender.jsp?url=...

    Open a document using a specific connector providing a user id and a security token
    http://{arender_server}/ARender.jsp?bean=myConnector&user=123456&token=9GISU9SG4Z  
