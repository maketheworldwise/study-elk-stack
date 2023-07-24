# Installation

## ElasticSearch

```shell
docker network create elastic
docker pull elasticsearch:8.1.2
docker run --name es-01 --net elastic -p 9200:9200 -p 9300:9300 -it elasticsearch:8.1.2
```

```shell
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
-> Elasticsearch security features have been automatically configured!
-> Authentication is enabled and cluster connections are encrypted.

->  Password for the elastic user (reset with `bin/elasticsearch-reset-password -u elastic`):
  V=nbaqlJp=+eH-YPPvuY

->  HTTP CA certificate SHA-256 fingerprint:
  acad4bcbc9f28a3c0a13e083c096f442faca6e6ce1eec0721f0b8b744bbbb1d9

->  Configure Kibana to use this cluster:
* Run Kibana and click the configuration link in the terminal when Kibana starts.
* Copy the following enrollment token and paste it into Kibana in your browser (valid for the next 30 minutes):
  eyJ2ZXIiOiI4LjEuMiIsImFkciI6WyIxNzIuMTguMC4yOjkyMDAiXSwiZmdyIjoiYWNhZDRiY2JjOWYyOGEzYzBhMTNlMDgzYzA5NmY0NDJmYWNhNmU2Y2UxZWVjMDcyMWYwYjhiNzQ0YmJiYjFkOSIsImtleSI6IjZmSUppSWtCVUU1Y1BrNGRlcHlJOnJLOWxzRzNuU18tM1Y2MU95alRMZXcifQ==

-> Configure other nodes to join this cluster:
* Copy the following enrollment token and start new Elasticsearch nodes with `bin/elasticsearch --enrollment-token <token>` (valid for the next 30 minutes):
  eyJ2ZXIiOiI4LjEuMiIsImFkciI6WyIxNzIuMTguMC4yOjkyMDAiXSwiZmdyIjoiYWNhZDRiY2JjOWYyOGEzYzBhMTNlMDgzYzA5NmY0NDJmYWNhNmU2Y2UxZWVjMDcyMWYwYjhiNzQ0YmJiYjFkOSIsImtleSI6IjZ2SUppSWtCVUU1Y1BrNGRlcHlJOnJ4NGVDajJxU1dHVXVNdjdDV0xpaHcifQ==

  If you're running in Docker, copy the enrollment token and run:
  `docker run -e "ENROLLMENT_TOKEN=<token>" docker.elastic.co/elasticsearch/elasticsearch:8.1.2`
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
```

![](/docs/images/001-install-elasticsearch.png)

## Kibana

```shell
docker pull kibana:8.1.2
docker run --name kib-01 --net elastic -p 5601:5601 kibana:8.1.2
```

```shell
[2023-07-24T13:20:10.813+00:00][INFO ][plugins-service] Plugin "metricsEntities" is disabled.
[2023-07-24T13:20:10.919+00:00][INFO ][http.server.Preboot] http server running at http://0.0.0.0:5601
[2023-07-24T13:20:10.964+00:00][INFO ][plugins-system.preboot] Setting up [1] plugins: [interactiveSetup]
[2023-07-24T13:20:10.966+00:00][INFO ][preboot] "interactiveSetup" plugin is holding setup: Validating Elasticsearch connection configuration…
[2023-07-24T13:20:11.022+00:00][INFO ][root] Holding setup until preboot stage is completed.


i Kibana has not been configured.

Go to http://0.0.0.0:5601/?code=628662 to get started.
```

![](/docs/images/001-install-kibana-token.png)
![](/docs/images/001-install-kibana-login.png)
![](/docs/images/001-install-kibana-change-password.png)

## Remote server

```yaml
# kibana.yml
server.host: 0.0.0.0

# elasticsearch.yml
http.host: 0.0.0.0
```

- open elasticsearch and kibana in remote address
