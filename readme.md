# Static hosting in a Docker container for SPA

This project demonstrates hosting static files in a Docker container, e.g. if you are working on a SPA-type application.

Files in `./site` are served through `nginx`. You can create a suitable build process to deploy your files into that directory. The sample file `site/index.html` can be deleted.

To run the server, from the `./webserver` directory, run the following command.

```shell
docker-compose up -d
```

When you are done running the server, to close it down, from the `./webserver` directory, run the following command.

```shell
docker-compose down
```

## Using HTTPS

If you want to use HTTPS, you need to

* Provide certificates.
* Make them available inside the container.
* Configure nginx to use them.

### Providing certificates

You will need to create and manage your own certificates - see [Certificates for development](#certs).

### Making certificates available

To make your certificates available, place them in the `./webserver/certs` directory and they will be mapped
into the container.

If you want to use certificates from a different location, edit the `volumes` section of the
`docker-compose.yml` file and change the location that is mapped into `/usr/local/nginx/certs`.

### Configuring nginx

To add your certificates, edit the `conf/nginx.conf` file to refer to them. 

### <a name="certs"></a>Certificates for development

Use of SSL certificates is recommended during development.

If you want to create your own certificate chain, check out
[this article](https://jamielinux.com/docs/openssl-certificate-authority/index.html).

Note that, for modern browsers, the instructions in the above article are incomplete, because
the Subject Alternative Names field is required on the certificate. It's quite painful to get
this working, but the following articles helped:

https://stackoverflow.com/a/21494483/260213

http://www.scispike.com/blog/openssl-subjectaltname-one-liner/

https://blog.zencoffee.org/2013/04/creating-and-signing-an-ssl-cert-with-alternative-names/


You can add the root cert (ca.cert.pem) into your System keychain on OS X -
see [here](https://derflounder.wordpress.com/2011/03/13/adding-new-trusted-root-certificates-to-system-keychain/).
