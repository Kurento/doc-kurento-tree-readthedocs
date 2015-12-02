%%%%%%%%%%%%%%%%%%%%%%%%
Kurento Tree Source Code
%%%%%%%%%%%%%%%%%%%%%%%%

Kurento Tree is hosted on github:

https://github.com/Kurento/kurento-tree

The git repository contains a Maven project with the following modules:

- **kurento-tree** - Reactor project that contains all modules.
- **kurento-tree/kurento-tree-server** - Server implementation of webcam
  broadcasting service. It provides the a custom protocol based on Json-Rpc
  over WebSockets for the communications between tree clients and the server.
- **kurento-tree/kurento-tree-client** - Java library that uses WebSockets and
  Json-Rpc to interact with the server. Can be used to implement the
  client-side of a tree application in a Java Application Server or in an
  Android device.
- **kurento-tree/kurento-tree-client-js** - Javascript library that uses
  WebSockets and Json-Rpc to interact with the server. It is also a wrapper for
  several JS APIs to make easier to develop a broadcast application from a
  browser.
- **kurento-tree/kurento-tree-demo** - Demonstration project of kurento-tree.
  It is implemented with a Java web application that uses Java client to
  communicate with tree server. The browser communicates with Java web
  application using a custom websocket protocol.
- **kurento-tree/kurento-tree-demo-spa** - Demonstration project of
  kurento-tree. It is implemented as a full Single Page Application. This
  project serves static assets with a SpringBoot server, but can be changed to
  any other server. Tree server is controlled from browser with JavaScript tree
  client.
- **kurento-tree/kurento-tree-test** - Includes integration tests for the tree
  server.

