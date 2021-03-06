## Install and run Birdsuite for CNV analysis with Docker

The offical install guide of Birdsuite is [Here](https://www.broadinstitute.org/science/programs/medical-and-population-genetics/birdsuite/birdsuite-install).

This birdsuite docker image is based on Ubuntu 14.04 LTS.

#### Prerequisites

- [Docker](https://www.docker.com/) (Version >= 1.5)
- Internet connection

#### Getting Started - Method 1 (Easy way): Pull the pre-built image from DockerHub

        docker pull psytky03/birdsuite

#### Getting Started - Method 2: Build a local image

-   Git clone this repo:

        git clone https://github.com/psytky03/Birdsuite_with_Docker.git
        cd Birdsuite_with_Docker

-   Build docker image:

        docker build -t psytky03/birdsuite:latest .
		
#### Getting Started - Method 3: Save a local image and transfer to offline machine		

-	Save the docker image after pull from DockerHub

		docker pull psytky03/birdsuite
		docker save -o birdsuite.docker psytky03/birdsuite
	 
-	Transfer the birdsuite.docker to the offline computer with USB and load the image from the file:
		
		docker load birdsuite.docker

		
#### Run Birdsuite with Docker 

-   Create a container and get inside:

        docker run -ti psytky03/birdsuite /bin/bash

-   Run the test data:

        cd /test_data
        /birdsuite/birdsuite.sh --basename=test --chipType=GenomeWideSNP_6 --outputDir=output --genderFile=test.gender --celFiles=test.cels --noLsf --apt_probeset_summarize.force


    Wait until the Birdsuite finish the run :-)

	
