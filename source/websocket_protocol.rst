%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
Kurento Tree WebSocket Protocol
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

The Kurento Tree server exposes a SockJS websocket at
http://treeserver:port/kurento-tree, where the hostname and port depend on the
current setup.

The exchanged messages between server and clients are
`JSON-RPC 2.0 <http://www.jsonrpc.org/specification>`_ requests and responses.
The events are sent from the server to client as notifications (they don't
require a response and they don't include an identifier).

WebSocket messages
==================

1 - Create tree
---------------

Request to create a new tree in Tree server. It is send by clients to server.

- **Method**: createTree

- **Parameters**:

  - **treeId** - new tree Id (optional)

- **Example request**::

    {
       "jsonrpc":"2.0",
       "id": 1,
       "method":"createTree",
       "params": {
           "treeId":"Channel 1"
        }
    }

- **Server response (result)**:

   - **value** - new tree id
   - **sessionId** - id of the WebSocket session between the client and the server

- **Example response**::

     {
        "jsonrpc":"2.0",
        "id": 1,
        "result": {
            "value": "Channel 1",
            "sessionId":"dv41ks9hj761rndhcc8nd8cj8q"
        }
     }

2 - Set tree source
-------------------

Request to configure the emitter (source) in a broadcast session (tree). It is
send by clients to server.

- **Method**: setTreeSource

- **Parameters**:

  - **treeId:** tree id to configure the source

  - **offerSdp:** Offer SDP created in the WebRtc peer that wants to
    broadcast media to viewers

- **Example request**::

    {
       "jsonrpc":"2.0",
       "id": 2,
       "method":"setTreeSource",
       "params": {
           "treeId":"Channel 1",
           "offerSdp":"v=0....apt=100\r\n"
        }
    }

- **Server response (result)**

  - **sdpAnswer:** SDP answer build by the the user's server WebRTC endpoint
  - **sessionId:** id of the WebSocket session

- **Example response**::

     {
        "jsonrpc":"2.0",
        "id": 2,
        "result": {
            "answerSdp": "v=0....apt=100\r\n",
            "sessionId":"dv41ks9hj761rndhcc8nd8cj8q"
        }
     }


3 - Remove tree source
----------------------

Request to remove the current emitter of a tree. It is send by clients to server.

- **Method**: remoteTreeSource

- **Parameters**:

  - **treeId:** tree id to remove the source

- **Example request**::

    {
       "jsonrpc":"2.0",
       "id": 3,
       "method":"remoteTreeSource",
       "params": {
           "treeId":"Channel 1"
        }
    }

- **Server response (result)**

  - **sessionId:** id of the WebSocket session

- **Example response**::

     {
        "jsonrpc":"2.0",
        "id": 3,
        "result": {
            "sessionId":"dv41ks9hj761rndhcc8nd8cj8q"
        }
     }

4 - Add tree sink
-----------------

Request to add a new viewer (sink) to the tree. It is send by clients to server.

- **Method**: addTreeSink

- **Parameters**:

  - **treeId:** tree id to add a new viewer
  - **offerSdp:** Offer SDP created in the WebRtc peer that wants to receive
    media from tree

- **Example request**::

    {
       "jsonrpc":"2.0",
       "id": 4,
       "method":"addTreeSink",
       "params": {
           "treeId":"Channel 1",
           "offerSdp":"v=0....apt=100\r\n"
        }
    }

- **Server response (result)**

  - **sdpAnswer:** SDP answer build by the the user's server WebRTC endpoint
  - **sinkId:** New sink id. This id will be used to remove the sink and to
    exchange ice candidates.
  - **sessionId:** id of the WebSocket session

- **Example response**::

    {
        "jsonrpc":"2.0",
        "id": 4,
        "result": {
            "answerSdp": "v=0....apt=100\r\n",
            "sinkId": "dab37f17-be82-4cd3-af20-edea13548254",
            "sessionId":"dv41ks9hj761rndhcc8nd8cj8q"
        }
     }

5 - Remove tree sink
--------------------

Request to remove a previously connected sink (viewer). It is send by clients to
server.

- **Method**: removeTreeSink

- **Parameters**:

  - **treeId:** tree id to remove the sink
  - **sinkId:** sink id to be removed

- **Example request**::

   {
       "jsonrpc":"2.0",
       "id": 5,
       "method":"removeTreeSink",
       "params": {
           "treeId":"Channel 1",
           "sinkId": "dab37f17-be82-4cd3-af20-edea13548254"
        }
    }

- **Server response (result)**

  - **sessionId:** id of the WebSocket session

- **Example response**::

     {
        "jsonrpc":"2.0",
        "id": 5,
        "result": {
            "sessionId":"dv41ks9hj761rndhcc8nd8cj8q"
        }
     }


6 - Ice candidate
-----------------

Notification sent form server to client when a new Ice candidate is received
from Kurento Media Server. It is send by server to clients.

- **Method**: iceCandidate

- **Parameters**:

  - **treeId** - Tree id to which belongs this candidate

  - **sinkId** - Sink id to which belongs this candidate (if not present,
    this candidate is referred to the tree source)

  - **sdpMid** - Ice candidate sdpMid

  - **sdpMLineIndex** - Ice candidate sdpMLineIndex

  - **candidate** - Ice candidate string

- **Example message**::

     {
        "jsonrpc":"2.0",
        "method":"iceCandidate",
        "params": {
            "treeId":"Channel 1",
            "sdpMid": "audio",
            "sdpMLineIndex": 0,
            "candidate": "candidate:2 2 UDP 2013266430 10.1.34.190 54211 typ host"
        }
     }

7 - Add ice candidate
---------------------

Request used to add a new ice candidate generated in the browser. It is send by
clients to server.

- **Method**: addIceCandidate

- **Parameters**:

   - **treeId**: Tree id to which belongs this candidate
   - **sinkId**: Sink id to which belongs this candidate (if not present,
     this candidate is referred to the tree source)
   - **sdpMid**: Ice candidate sdpMid
   - **sdpMLineIndex** Ice candidate sdpMLineIndex
   - **candidate**: Ice candidate string

- **Example request**::

    {
       "jsonrpc":"2.0",
       "id": 7,
       "method":"addIceCandidate",
       "params": {
          "treeId": "Channel 1",
          "sinkId": "dab37f17-be82-4cd3-af20-edea13548254",
          "sdpMid":"video",
          "sdpMLineIndex": 1,
          "candidate": "candidate:952163293 2 .... port 55404 generation 0",
       }
    }

- **Server response (result)**

      - **sessionId:** id of the WebSocket session

- **Example response**::

    {
       "jsonrpc":"2.0",
       "id": 7,
       "result": {
           "sessionId":"dv41ks9hj761rndhcc8nd8cj8q"
       }
    }


8 - Remove tree
---------------

Request used to remove a tree. It is send by clients to server.

- **Method**: removeTree

- **Parameters**:

   - **treeId**:  Tree id to be removed

- **Example request**::

     {
        "jsonrpc":"2.0",
        "id": 8,
        "method":"removeTree",
        "params": {
           "treeId": "Channel 1"             
        }
     }

- **Server response (result)**

    - **sessionId:** id of the WebSocket session

- **Example response**::

       {
          "jsonrpc":"2.0",
          "id": 8,
          "result": {
              "sessionId":"dv41ks9hj761rndhcc8nd8cj8q"
          }
       }
