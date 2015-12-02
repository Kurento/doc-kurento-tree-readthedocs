%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
Kurento Tree Server Deployment
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

Currently, there are no binary releases of Kurento Tree Server. In order to
deploy a new Tree Server it is needed to build it from sources.

Software Requirements
=====================

In order to execute Kurento Tree Server it is necessary the following software:

- Ubuntu 14.04
- JDK 7 or 8
- Kurento Media Server or connection with at least a running instance (to
  install follow the official
  `guide <http://www.kurento.org/docs/current/installation_guide.html>`_)

Build from sources
==================

To compile Kurento Tree Server from sources, there are more dependencies:

First of all, to build from sources it is necessary to download the sources from
git repository. For it, you have to install git::

    sudo apt-get install git

Then, you have to install maven::

    sudo apt-get install maven
    
Finally, you need Bower, npm and nodejs::

   curl -sL https://deb.nodesource.com/setup | sudo bash -
   sudo apt-get install -y nodejs
   sudo npm install -g bower
     
When all dependencies are installed, you have to download and build two git
repositories, kurento-java and kurento-tree:: 

    git clone https://github.com/Kurento/kurento-java.git
    cd kurento-java
    mvn install -DskipTests=true
    cd ..
    git clone https://github.com/Kurento/kurento-tree.git
    cd kurento-tree
    mvn install -DskipTests=true
    cd ..
    
To execute Kurento Tree server from the recent build, execute the following
commands::
    
    cd kurento-tree/kurento-tree-server
    mvn exec:java
    
Then a bunch of log messages will appear in the console. When the following
message appears in the console::

    Started KurentoTreeServerApp in 4.058 seconds (JVM running for 8.017)

You can use Kurento Tree Server in the port 8890.
