## Install and run Birdsuite for CNV analysis with Docker

The offical install guide of Birdsuite is [Here](https://www.broadinstitute.org/science/programs/medical-and-population-genetics/birdsuite/birdsuite-install).

This birdsuite docker image is based on Ubuntu 14.04 LTS.

## Prerequisites

- [Docker](https://www.docker.com/) (ver >= 1.5)
- Internet connection

## Getting Started - Method 1 (Easy way): Pulling the pre-built image from DockerHub

        docker pull psytky03/birdsuite

## Getting Started - Method 2: Build a local image

-   Git clone this repo:

        git clone https://github.com/psytky03/Birdsuite_with_Docker.git
        cd Birdsuite_with_Docker
        

-   Download the additional annotation files/apt tool/MCR installer
        
        wget https://dl.dropboxusercontent.com/u/964493/additional.tar.gz
        tar zxvf additional.tar.gz


-   Build docker image:

        docker build -t psytky03/birdsuite:latest .




## Run Birdsuite with Docker 

-   Create a container and get inside:

        docker run -ti psytky03/birdsuite /bin/bash

-   Run the test data:

        cd /test_data
        /birdsuite/birdsuite.sh --basename=test --chipType=GenomeWideSNP_6 --outputDir=output --genderFile=test.gender --celFiles=test.cels --noLsf --apt_probeset_summarize.force


    Wait until the Birdsuite finish the run ^_^
