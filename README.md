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