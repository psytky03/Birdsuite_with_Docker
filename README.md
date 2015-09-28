## Install and run Birdsuite for CNV analysis with Docker

The homepage of Birdsuite is [Here](https://www.broadinstitute.org/scientific-community/science/programs/medical-and-population-genetics/birdsuite/birdsuite).

## Prerequisites

- Docker 
- Internet connection

## Getting Started

-   Git clone this repo:

        git clone https://github.com/psytky03/



-   Build docker image:

        
        docker build -t psytky03/birdsuite:latest .

-   Create a container and get into:

        docker run -ti psytky03/birdsuite /bin/bash


-   Run test data with Birdsuite:

        cd /test_data
        /birdsuite/birdsuite.sh --basename=test --chipType=GenomeWideSNP_6 --outputDir=output --genderFile=test.gender --celFiles=test.cels --noLsf --apt_probeset_summarize.force


    Wait to see whether the application to finsih
