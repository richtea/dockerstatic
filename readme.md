# Static hosting in a Docker container for SPA

This project demonstrates hosting static files in a Docker container, e.g. if you are working on a SPA-type application.

Files in `./site/` are served through `nginx`. You can create a suitable build process to deploy your files into that directory. The sample file `site/index.html` can be deleted.

To run the server, from the `./webserver` directory, run the following command.

```shell
docker-compose up -d
```

When you are done running the server, to close it down, from the `./webserver` directory, run the following command.

```shell
docker-compose down
```
