%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
Kurento Tree JavaScript Client
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

The developer of Kurento Tree applications can use this client when implementing
the front-end part of a broadcasting application with Kurento Tree. It is not
necessary to write any server-side logic.

Using this client
=================

The library files needed to use this client are served by Kurento Tree Server in
the path:

 - ``http://server-host:port/js/KurentoTree.js``

There are also several third party libraries that need to be "imported" in the
HTML in order to user this Kurento Tree JavaScript client. This third party
libraries are also served by Kurento Tree Server in the paths:

 - ``http://treeserver:port/bower_components/adapter.js/adapter.js``
 - ``http://treeserver:port/bower_components/eventEmitter/EventEmitter.js``
 - ``http://treeserver:port/js/kurento-utils.js``
 - ``http://treeserver:port/lib/sockjs.js``
 - ``http://treeserver:port/js/websocketwithreconnection.js``
 - ``http://treeserver:port/js/kurento-jsonrpc.js``
 - ``http://treeserver:port/js/jsonRpcClient.js``

For example, all necessary dependencies to create a SPA Kurento Tree application
can be included in the HTML with the elements:

.. code-block:: html 

   <script src="http://treeserver:port/bower_components/adapter.js/adapter.js"></script>
   <script src="http://treeserver:port/bower_components/eventEmitter/EventEmitter.js"></script>
   <script src="http://treeserver:port/js/kurento-utils.js"></script>
   <script src="http://treeserver:port/lib/sockjs.js"></script>
   <script src="http://treeserver:port/js/websocketwithreconnection.js"></script>
   <script src="http://treeserver:port/js/kurento-jsonrpc.js"></script>
   <script src="http://treeserver:port/js/jsonRpcClient.js"></script>
   <script src="http://treeserver:port/js/KurentoTree.js"></script>

When these files are "included" in the HTML, the class ``KurentoTree`` is
available to subsequent JavaScript files included in the page. ``KurentoTree``
class is the entry point of the Kurento Tree JavaScript Client.

KurentoTree usage
=================

To connect to a Kurento Tree Server it is necessary to create an instance of
``KurentoTree`` class indicating the URL of the server:

.. sourcecode:: javascript

   var tree = new KurentoTree('http://treeserver:port/kurento-tree');

In background, a websocket connection is made between browser and Kurento Tree
server.

To broadcast the user webcam it is necessary to execute a code similar to the
following:

.. sourcecode:: javascript

   var treeName = ...

   var mediaOptions = {
      localVideo : video,
      mediaConstraints : {
         audio : true,
         video : {
            mandatory : {
               maxWidth : 640,
               maxFrameRate : 15,
               minFrameRate : 15
            }
         }
      }
   };

   tree.setTreeSource(treeName, mediaOptions);
   
Where ``localVideo`` refers to a HTML div element when local video being to be
broadcasted will be shown. If this option is not specified, no local video will
be shown in the page.

To include a player showing the video that it is broadcasting another user, it
is necessary to include a code similar to:

.. sourcecode:: javascript

   var treeName = ...
   
   var mediaOptions = { 
      remoteVideo : video
   }
   
   tree.addTreeSink(treeName, options);

Where ``remoteVideo`` refers to a HTML div element when remote video will be
shown.

To stop any transmission (from emitter or receiver), ``close()`` method can be
invoked:

.. sourcecode:: javascript

   tree.close();
