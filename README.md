# LDF Server Deployment
Example files for a default LDF deployment, with an [LDF server](https://github.com/LinkedDataFragments/Server.js), [NGINX cache](https://www.nginx.com/) and [LDF web client](https://github.com/LinkedDataFragments/jQuery-Widget.js) using [Docker Compose](https://docs.docker.com/compose/).

## Run
To start the LDF server, cache and web client, simply run the following command:

```bash
docker-compose up
```
Adding the `-d` parameter will run it as a daemon.

The server will now be running on the default HTTP port, and the web client will be running on port 8080.

## Configure
The required configuration for deploying an LDF server is minimal.

### Server config
`config-server.json` specifies the [server configuration](https://github.com/LinkedDataFragments/Server.js#configure-the-data-sources).

### Client config
`config-client.json` specifies the [web client configuration](https://github.com/LinkedDataFragments/jQuery-Widget.js).
The `queries` folder should contain the SPARQL queries that should be available by default in the web client.

### Cache config
`nginx.conf` and `nginx-default` are the NGINX config files.
By default, this cache is configured to have 4 worker processes, which cache LDF server resources for 7 days.
Logging is enabled by default, resulting log files will appear in the automatically mounted `log/` folder.

### Parameters
No changes are required in the `docker-compose.yml` file, all essential parameters can be changed in the `.env` file.

`DATA_DIR` specifies the data directory in which your datasets are available.
The files in this directory will be mounted to the `/data` directory inside the Docker instance.
The default `config-server.json` expects a `dbpedia2014.hdt` dataset file to be present in this directory.

`LDF_WORKERS` specifies the number of workers the LDF server should have, this will typically be the same as the number of cores of your machine.
The `worker_processes` value in `nginx.conf` should in most cases have the same value.
