# prometheus  for jenkins

## how to running

* build export

> i had push one exporter to dockerhub

```code
git clone https://github.com/akawork/Jenkins-exporter.git

cd Jenkins-exporter
docker build -t dalongrong/jenkins_exporter

```

* edit .env file

```code
touch .env

JENKINS_SERVER=http://jenkins:8080
JENKINS_USERNAME=admin
JENKINS_PASSWORD=dalong
```

* running

```code
docker-compose up -d
```

* config grafanna

import file  jenkins-exporter_rev1.json


## some notes

tboerger/jenkins-exporter &&  tolleiv/jenkins_exporter
also is a better choose

* some config

```code
version: "3"
services: 
    jenkins: 
      image: jenkins/jenkins:lts-slim
      ports:
      - "8080:8080"
    jenkins-exporter2:
      image: tboerger/jenkins-exporter
      command: -jenkins.address=http://jenkins:8080 -jenkins.password=dalong -jenkins.username=admin
      ports:
      - "9103:9103"
    jenkins-exporter3:
      image: tolleiv/jenkins_exporter
      command: -j=http://jenkins:8080 --password=dalong --user=admin
      ports:
      - "9119:9118"
    jenkins-exporter:
      image: dalongrong/jenkins_exporter
      env_file:
      - .env
      ports:
      - "9118:9118"
    grafana:
      image: grafana/grafana    
      ports:
      - "3000:3000"
    prometheus:
      image: prom/prometheus
      volumes:
      - "./prometheus.yml:/etc/prometheus/prometheus.yml"
      ports:
      - "9090:9090"  
  
```

