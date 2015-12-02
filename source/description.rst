%%%%%%%%%%%%%%%%%%%%%%%%
Kurento Tree Description
%%%%%%%%%%%%%%%%%%%%%%%%

Kurento Tree is a project that allows developers to build video broadcasting web
applications over internet. It is developed using WebRtc technology and Kurento
Media Server.

Kurento Tree project is formed by a server and two clients, a Java client and a
JavaScript client. There are also two demonstration applications are available
that makes use of this project to enable users to see the webcam of other user.

Kurento Tree Server
===================

The Tree Server (**kurento-tree-server**) is a project designed to be deployed
and controlled by clients. We provide a Java client and a JavaScript client
specifically designed to browsers (it uses several browser-only APIs). In any
case, other clients can be implemented if follow the Json-Rpc over websocket
protocol. Tree Server uses a Kurento Media Server to provide WebRtc media
handling to clients. For this reason, a Kurento Media Server have to be
available and configured in Tree Server config file.

Kurento Tree Java Client
========================

The Java Tree Client (**kurento-tree-client**) implements a Tree Client to be
used from Java applications. It is designed to be used in Java web applications
or Android applications. The client only contains an implementation of Json-Rpc
websocket protocol implementated by Tree server. It does not contain any
functionality to control video players or video capturing from webcams.

Kurento Tree JavaScript Client
==============================

The JavaScript Tree Client (**kurento-tree-client-js**) implements a Tree Client
to be used in Single Page Applications (SPA). It contains the main file
``KurentoTree.js`` to connect to Tree Server. Besides the Json-Rpc websocket
protocol, it uses several libraries to control WebRtc and player HTML5 APIs in
the browsers. This allows to developer to focus in app functionality hidding
low level details.

Kurento Tree Demo applications
==============================

We provide two demos in this repository to show how to use the two provided
clients.

Demo using JavaScript client
----------------------------

The demo using Kurento Tree JavaScript client is located in the project
**kurento-tree-demo-spa**. It allows a user to broadcast his webcam and any
other user can see it.

From a technical point of view, this demo is Single Page Application (SPA)
implemented as a bunch of HTML, CSS and JS files. This files are served from a
SpringBoot web server, but can be served with any http server. The JavaScript
code uses Kurento Tree JavaScript client to communicate directly with Kurento
Tree Server.

Demo using Java client
----------------------

The demo using Kurento Tree Java client is located in the project
**kurento-tree-demo**. It allows a user to broadcast his webcam and any other
user can see it (in the same way as the another demo).

From a technical point of view, this demo is a SpringBoot web application that
serves HTML, CSS and JS files. JavaScript logic communicates with SpringBoot
server by means of websocket protocol. The SpringBoot server handle websocket
messages and uses Java Kurento Tree Client to communicate with Kurento Tree
Server. That is, there is no direct communication between JavaScript code and
Kurento Tree Server. All communications is through SpringBoot server app.