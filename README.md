# tick+grafana

Run the complete tick stack plus grafana using docker compose.  This uses the latest versions of each individual docker image.

- [telegraf](https://hub.docker.com/_/telegraf/)
- [influxdb](https://hub.docker.com/_/influxdb/)
- [chronograf](https://hub.docker.com/_/chronograf/)
- [kapacitor](https://hub.docker.com/_/kapacitor/)
- [grafana/grafana](https://hub.docker.com/r/grafana/grafana/)

## Usage

Start all the images as follows:

    # cd to desired version
    cd 1.3/
    # Start all images in the background
    docker-compose up -d

### Check that InfluxDB works:

Run this curl command, if no errors occur InfluxDB is running:

    curl http://localhost:8086/ping


#### The `influx` client

Use the built-in influx cli service:

    docker-compose run influxdb-cli

### Check that Telegraf works

By default, the Telegraf creates a `telegraf` database.
Check that InfluxDB has such a database in addition to the `_internal` database.

    docker-compose run influxdb-cli
    > show databases

### Check that Chronograf works

Access the Chronograf inteface, [http://localhost:8888](http://localhost:8888)

### Check Kapacitor works

First, run this curl command, if no errors occur Kapacitor is running:

    curl http://localhost:9092/kapacitor/v1/ping


Use the built-in kapacitor cli service:

    docker-compose run kapacitor-cli
    $ kapacitor list tasks

Confirm Kapacitor is subscribed to all databases in InfluxDB

    docker-compose run influxdb-cli
    > show subscriptions


## References

- https://github.com/influxdata/TICK-docker
- https://github.com/nicolargo/docker-influxdb-grafana