%%%%%%%%%%%%%%%%%%
Kurento Tree Demos
%%%%%%%%%%%%%%%%%%

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
