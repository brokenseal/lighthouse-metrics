DISCLAIMER: this is a copied (and improved) version of the official
[https://github.com/sigp/lighthouse-metrics](lighthouse-metrics) repo.

# Lighthouse Metrics

Provides a `docker-compose` environment which scrapes metrics from Lighthouse
nodes using Prometheus and presents them in a browser-based Grafana GUI.

## Usage

This guide expects you to be running the official
[https://github.com/sigp/lighthouse-docker](lighthouse) docker-compose
environment.

1. Bring the environment up with `docker-compose up -d`.
2. Ensure that Prometheus can access your Lighthouse nodes by ensuring they are
   in the `UP` state at [http://localhost:9090/targets](http://localhost:9090/targets).
   Both http://beacon_node:5054/metrics and http://validator_client:5064/metrics
   needs to be in the `UP` state
3. Browse to [http://localhost:3000](http://localhost:3000)
   - Username: `admin`
   - Password: `changeme`
4. Import any dashboard from the `dashboards` directory in this repo:
   - In the Grafana UI, go to `Dashboards` -> `Manage` -> `Import` -> `Upload .json file`.
   - The `Summary.json` dashboard is a good place to start.

Grafana and Prometheus will be running on the same network as the official
`lighthouse-docker` containers and will persist any data in the two `grafana`
and `prometheus` folders of this repo.

## Hosting Publicly

By default Prometheus and Grafana will only bind to localhost (127.0.0.1), in
order to protect you from accidentally exposing them to the public internet. If
you would like to change this you must edit the `http_addr` in `grafana.ini`.

## Prometheus

The `scrape-targets.json` file is periodically read by Prometheus and specifies
the targets it should watch.

If you want to add a node to the metrics service, do it there.
