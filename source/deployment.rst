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
     
When all dependencies are installed, you can get the code from the official
github repository and move into the code folder:: 

    git clone https://github.com/Kurento/kurento-tree.git
    cd kurento-tree

This will downloadd the latest code into your machine. *That code is normally for
development, and depends on SNAPSHOT versions of artifacts that are not deployed
in Maven Central*. You can either continue working with the nightly build (with caution,
as the development version might be unstable), or get the latest release of the project.
The steps that you have to follow for each one are different.

* Working with development versions: Please read the `official project's documentation <https://doc-kurento.readthedocs.org/en/stable/mastering/kurento_development.html>`__ on how
  to work with development versions, specially `this <https://doc-kurento.readthedocs.org/en/stable/mastering/kurento_development.html#kurento-java-client>`__ part about how to use our internal Archiva repo.

* Using a release version: This is the recommended approach, as release versions are more
  stable. You'll need to download the last release tag::

    git checkout -b release 6.5.1-SNAPSHOT

Once you got the desired version, you just need to execute::

    mvn install -DskipTests=true

And that will install all generated artifacts in your local Maven repository.
    
To execute Kurento Tree server from the recent build, execute the following
commands::
    
    cd kurento-tree-server
    mvn exec:java
    
Then a bunch of log messages will appear in the console. When the following
message appears in the console::

    Started KurentoTreeServerApp in 4.058 seconds (JVM running for 8.017)

You can use Kurento Tree Server in port 8890.
