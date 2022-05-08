# dockerized-kafka-rest-bigquery-pipeline
In this repo, you can set up a container which has kafka and kafka connect to connect with restful api and bigquey (as sink). Edit json on `config` folder to connect to any restful api you want and specify target dataset in your bigguqery.

kafka connect add-on included in the image:
https://github.com/llofberg/kafka-connect-rest
https://www.confluent.io/hub/wepay/kafka-connect-bigquery

# Initiation
```
docker compose up
```
