%%%%%%%%%%%%%%%%%%%%%%%%
Kurento Tree Java Client
%%%%%%%%%%%%%%%%%%%%%%%%

The developer of Kurento Tree applications can use a Java client to control
Kurento Tree Server. This library gives more control to developer and allows to
include authentication and authorization to broadcast applications. To create a
broadcast applications with this Java client, it is necessary to implement a
frond-end logic in JavaScript that communicates with Java web applications
using websockets or another technology. Then, Java back-end will communicate
with Kurento Tree Server using this client.

Using this client
=================

This client can be obtained as a maven dependency with the following coordinates:

.. code-block:: html

   <dependency>
      <groupId>org.kurento</groupId>
      <artifactId>kurento-tree-client</artifactId>
      <version>6.6.1-SNAPSHOT</version>
   </dependency>

With this dependency, the developer can use the class
``org.kurento.tree.client.KurentoTreeClient`` to control Kurento Tree Server.

KurentoTreeClient usage
=======================

To connect to a Kurento Tree Server it is necessary to create an instance of
``KurentoTreeClient`` class indicating the URL of the server:

.. sourcecode:: java

   KurentoTreeClient tree = new KurentoTreeClient("http://treeserver:port/kurento-tree");

In background, a websocket connection is made between Java app and Kurento Tree
server.

To broadcast the user webcam it is necessary to execute a code similar to the
following:

.. sourcecode:: java

   String treeName = ... // Select a unique name for the broadcast

   tree.createTree(treeName);

   String sdpOffer = ... // Create sdp offer in browser

   String sdpAnswer = tree.setTreeSource(treeName, sdpOffer);

   // Send sdpAnswer to browser to complete media negotiation

In this code, ``sdpOffer`` have to be created in the browser and communicated to
Java web app using websocket or other technology. On the other hand,
``sdpAnswer`` have to be send to browser.

.. sourcecode:: java

   String treeName = ... // The broadcast name

   String sdpOffer = ... // Create sdp offer in browser

   TreeEndpoint treeEndpoint = tree.addTreeSink(treeName, sdpOffer);

   String viewerId = treeEndpoint.getId(); // Id of this viewer

   String sdpAnswer = treeEndpoint.getSdp();

   // Send sdpAnswer to browser to complete media negotiation

In same way as before, ``sdpOffer`` and ``sdpAnswer`` have to be interchanged
with JavaScript code in the browser to perform the media negotiation.

Kurento Tree support media negotiation with
`Trickle ICE <https://webrtchacks.com/trickle-ice/>`_ . In this sense, besides
SDP offer and answer interchange between browser and media server, it is
necessary to interchange Ice candidates between peers.

.. sourcecode:: java

   while (true) {

      // Retrieve new ice candidate from server
      IceCandidateInfo cand = tree.getServerCandidate();

      if (candidateInfo == null) {
         // No more ice candidates. Connection closed
         break;
      }

      // Tree to which belongs this candidate
      String treeName = cand.getTreeId();

      // Viewer to which belongs this candidate (if null, it is tree source)
      String viewerId = cand.getSinkId();

      // Ice candidate info
      String candidate = cand.getIceCandidate().getCandidate());
      int sdpMLineIndex = cand.getIceCandidate().getSdpMLineIndex());
      String sdpMid = cand.getIceCandidate().getSdpMid());

      // Send candidate info to browser to complete media negotiation

   }

When a new ice candidate is received from browser it is necessary to process it
properly to achieve a successful media negotiation. This is done using the
following code:

.. sourcecode:: java

   String treeName = ...
   String viewerId = ... // null if is tree source
   
   String candidate = ...
   int sdpMLineIndex = ...
   String sdpMid = ...

   tree.addIceCandidate(treeName, viewerId, 
       new IceCandidate(candidate, sdpMid, sdpMLineIndex));

Reference documentation
=======================


You can take a look to the `JavaDoc <#kurento-tree-client-javadoc>`_ of this
client.
