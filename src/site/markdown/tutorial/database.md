## Set up databases to store and analyze streams content

This tutorial assumes you are using linux or Mac OS X.

### Confirm Docker is healthy

We'll assume you've got docker up and running.

Run from your command line:

    docker ps

If you see a (possibly empty) list of running containers, you are good.

### Run Elasticsearch

Elasticsearch is a great database for storing content from your streams.

    docker run -d --name elasticsearch elasticsearch

### Add Elasticsearch container details to your configuration

    echo $(docker-machine ip)

Put the following into elasticsearch.conf (in the same directory as reference.conf)

    include "reference.conf"
    elasticsearch {
        hosts = [
          # paste the response from echo $(docker-machine ip) on this line
        ]
        protocol = "tcp"
        port = 9300
        index = "streams"
        indexes = [
            "streams"
        ]
        types = [
            "page"
            "post"
        ]
    }  

###### Licensed under Apache License 2.0 - http://www.apache.org/licenses/LICENSE-2.0
