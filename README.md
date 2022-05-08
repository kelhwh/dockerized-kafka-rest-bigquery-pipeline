# dockerized-kafka-rest-bigquery-pipeline
In this repo, you can set up a set of containers which has kafka and kafka connect to connect with restful api and bigquey (as sink). By default, a kafka pipeline which ingests bitoin and stablcoins price data from the [Coingecko api](https://www.coingecko.com/en/api) and send to a table in bigquery is built. Edit json on `config` folder to connect to any restful api you want and specify target dataset in your bigguqery.

kafka connect add-ons included in the image:
- https://github.com/llofberg/kafka-connect-rest
- https://www.confluent.io/hub/wepay/kafka-connect-bigquery

# Initiation
1. Export you bigquery key and paste it in `config/bigquery-credential.json`.
2. Put in your names of your bigquery project and dataset in `config/sink-bigquery.json`.
3. Start the containers

```
docker compose up
```

4. Start the source connector (Create the kafka topic first if you don't want to apply the default topic settings)
```
docker container exec -it connect_1 bash -c \
"curl -i -X POST -H "Accept:application/json"  -H  "Content-Type:application/json" \
http://localhost:8083/connectors/ -d @config/source-coingecko.json"
```

5. Start the sink connector
```
docker container exec -it connect_1 bash -c \
"curl -i -X POST -H "Accept:application/json"  -H  "Content-Type:application/json" \
http://localhost:8083/connectors/ -d @config/sink-bigquery.json"
```
