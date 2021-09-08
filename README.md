# dockerfiles
Source files for building OMNeT++ related docker images

 - omnetpp-base -> ubuntu based image containing all required packages to build and use OMNeT++ on the command line (clang compiler, make etc.)
   - omnetpp -> contains a pre-built OMNeT++ distribution for quickly compiling and running a model in Cmdenv (No IDE or Qtenv support!)
     - inet -> OMNeT++ and INET in the same image (release only) to be used as a base image for INET dependent models
   - omnetpp-gui -> contains a pre-built OMNeT++ with all GUI tools (except OSG and osgEarth), that can be accessed using X from the host
     - inet-gui -> Same as inet, except based on omnetpp-gui, so it has IDE and Qtenv support
 - omnetpp-tf-base -> ubuntu based image derived from floopcz/tensorflow_cc:ubuntu containing TensorFlow and all required packages to build and use OMNeT++ on the command line (clang compiler, make etc.)
   - omnetpp-tf -> contains a pre-built OMNeT++ distribution and TensorFlow for quickly compiling and running a model in Cmdenv (No IDE or Qtenv support!)
   - omnetpp-tf-gui -> contains a pre-built OMNeT++ with all GUI tools (except OSG and osgEarth) and TensorFlow, that can be accessed using X from the host
 - swarm-base -> tools and packages required to run OMNeT++ simulations in a docker swarm (distcc, compiler, OMNeT++ core)
 - travis-base -> an image containing Linux, Windows and macOS compiled versions of OMNeT++ (for continuous integration)
   - travis-inet -> an image used to run continuous integration test for INET (contains NSC, ffmpeg and other optional INET dependnecies)
 - docker-sphinx -> Sphinx docker image for building OMNeT++ and INET documentation projects
