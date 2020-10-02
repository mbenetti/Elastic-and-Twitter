## Sentiment Analysis using the Twitter API and the Elastic Stack


<img align="center" width="640" height="426" src="https://cdn.pixabay.com/photo/2018/07/26/08/31/woman-3563066_1280.jpg">

### This project was developed between Datagroup and the University Ulm. This was a studen project and is not suitable for pruduction envirments. 
# Guide:

## Requirements:
  - An x86 (or an ARM64) based 64bit CPU
  - Docker aswell as Docker-Compose have to be installed (On Windows, Docker-Compose comes with the Docker Desktop installation)
  - Enough Ram (At least 4GB)
  
## Set-Up:
Clone this repository to the desired location 
```
git clone https://github.com/WIFProjekt1920/sentiment-analysis_elk-stack.git .
```

Afterwards go into the newly created directory (Termina/Bash/Powershell)
```
cd /sentiment-analysis_elk-stack
```

Here you will see Directories named Kibana, Elasticsearch and Logstash. The docker-compose file that we will be using later, binds configuration files located in these directories into the Elastic-Stack Container/s. So you use your own configuration files and/or modify the existing ones in these directories.
You will at least ned to modify the logstash.conf file located in logstash/pipelines/ to fill in your Twitter API Tokens and Keys.

If you're ready, run the following command/s (depending on your need) to create and start the necessarry containers.
The first time might require a longer procesing time, as the needed images need to be downloaded or build up first.
```
docker-compose up --scale sentiment=4 

// if no live output is needed, put -d after the command:

docker-compose up -d --scale sentiment=4

// for the x86 version (For live output, ommit -d):

docker-compose -f dc-x86.yml up -d --scale sentiment=4
```

Currently, the Containers are created on the running System. Later it will be possible to just pull the necessary Images from Dockerhub.

### Do NOT! build the image on Windows, as there WILL be errors! To build the image from the ground up, a Linux OS is needed!

If all Containers started successfully, you can reach Kibana in your brownser with the following URL:
```
http://localhost:5601
```

## Mapped Ports
```
Host    Container   Service

5601    5601        Kibana
9200    9200        Logstash
5044    5044        Elasticsearch
4444    4444        Nginx-Load-Balancer
```

## Sources
Here you will find the Sources that were used to create this project.

Load-Balancing via Nginx:
https://pspdfkit.com/blog/2018/how-to-use-docker-compose-to-run-multiple-instances-of-a-service-in-development/

Elastic-Stack Container Documentation (The ELK Stack is based on sebp/elk)
https://elk-docker.readthedocs.io/

Documentation of the Sentiment Analysis module that is used in this project:
https://github.com/thisandagain/sentiment

