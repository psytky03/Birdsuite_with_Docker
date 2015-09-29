## Install and run Birdsuite for CNV analysis with Docker

The homepage of Birdsuite is [Here](https://www.broadinstitute.org/scientific-community/science/programs/medical-and-population-genetics/birdsuite/birdsuite).

## Prerequisites

- Docker 
- Internet connection

## Getting Started Method 1: Pulling the pre-built image from DockerHub

        docker pull psytky03/birdsuite

## Getting Started Method 2: Build a local image

-   Git clone this repo:

        git clone https://github.com/psytky03/Birdsuite_with_Docker.git
        

-   Download the additional annotation files/apt tool/MCR installer
        
        wget https://dl.dropboxusercontent.com/u/964493/additional.tar.gz


-   Build docker image:

        docker build -t psytky03/birdsuite:latest .




## Run Birdsuite with Docker 

-   Create a container and get into:

        docker run -ti psytky03/birdsuite /bin/bash

        cd /test_data
        /birdsuite/birdsuite.sh --basename=test --chipType=GenomeWideSNP_6 --outputDir=output --genderFile=test.gender --celFiles=test.cels --noLsf --apt_probeset_summarize.force


    Wait to see whether the application to finsih
