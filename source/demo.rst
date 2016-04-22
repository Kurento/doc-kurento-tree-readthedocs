%%%%%%%%%%%%%%%%%%
Kurento Tree Demos
%%%%%%%%%%%%%%%%%%

We provide two demos in this repository to show how to use the two provided
clients.

Demo using JavaScript client
============================

The demo using Kurento Tree JavaScript client is located in the project
**kurento-tree-demo-spa**. It allows a user to broadcast his webcam and any
other user can see it.

From a technical point of view, this demo is Single Page Application (SPA)
implemented as a bunch of HTML, CSS and JS files. This files are served from a
SpringBoot web server, but can be served with any http server. The JavaScript
code uses Kurento Tree JavaScript client to communicate directly with Kurento
Tree Server.

Demo using Java client
======================

The demo using Kurento Tree Java client is located in the project
**kurento-tree-demo**. It allows a user to broadcast his webcam and any other
user can see it (in the same way as the another demo).

From a technical point of view, this demo is a SpringBoot web application that
serves HTML, CSS and JS files. JavaScript logic communicates with SpringBoot
server by means of websocket protocol. The SpringBoot server handle websocket
messages and uses Java Kurento Tree Client to communicate with Kurento Tree
Server. That is, there is no direct communication between JavaScript code and
Kurento Tree Server. All communications is through SpringBoot server app.

Installation
------------

To start this demo application you first need to download the source code as
specified in :doc:`deployment` section.

First, you have to have a Kurento Media Server available. Please refer to
`official Kurento documentation <http://doc-kurento.readthedocs.org/en/stable/installation_guide.html>`_
for information on how to get it.

Then, you have to start Kurento Tree Server using the following commands::

    mvn install -DskipTests=true
    cd kurento-tree-server
    mvn exec:java
    
These commands will start Kurento Tree Server assuming that Kurento Media Server
is located in the same server. That is, Kurento Tree Server will try to connect
to a KMS in ``ws://localhost:8888/kurento``. If you need Kurento Tree Server
connects to KMS with another URI, you have to exec it using the following
command::

    mvn exec:java -Dkms.url=ws://<kms_host>:8888/kurento

The following step is start the Kurento Tree Demo app that uses Kurento Tree
Server. You have to open another terminal and locate in the root of the source
code repository, then you have to execute the following commands::

    cd kurento-tree-demo 
    mvn install -DskipTests=true
    mvn exec:java

These commands execute Kurento Tree Demo assuming that Kurento Tree Server is
located in localhost. The demo app tries to connect to
``wss://localhost:8890/kurento-tree``. If you want to connect to a Kurento Tree
Server located in another host, you have to start it using the following
command::

    mvn exec:java -Dkts.ws.uri=wss://<kts_host>:8890/kurento-tree
    
To use the demo application you have to open a browser pointing to
``https://localhost:8443``. The main use case of Kurento Tree Demo is broadcast
a webcam to other users. To test this scenario, open two browsers, first
configure one browser as presenter and then configure the other browser as
viewer and you should be the webcam from the presenter in the viewer.


