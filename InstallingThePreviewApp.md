

# Installing the Preview App #

[Our online previewer application](http://fossil.wanderinghorse.net/demos/wikiwym/) can be installed as follows...

## Requirements ##

  * Our [source code](http://code.google.com/p/wikiwym/source/checkout).
  * PHP5 with JSON support and the the so-called `fopen()` wrappers, which allow PHP to open remote URLs using `fopen()`.
  * The web server must be able to open http connections to `XXX.googlecode.com`, where `XXX` is an arbitrary Google Code-hosted project name. On a home server this is not normally a problem, but can be if inside a firewall which restrict's the server's access to the outside world (e.g. an organization where servers cannot resolve external hostnames).
  * It is untested on non-Apache servers and is known to not work on Windows servers (but _why_ is unknown).

# Setting up Apache #

If you run Apache/PHP locally then you will want to an entry to your `/etc/hosts` (or equivalent):

```
127.0.0.1 localhost <any local aliases> wikiwym
```

In your Apache configuration, add something like:

```
<VirtualHost *:80>
    ServerAlias wikiwym
    DocumentRoot /path/to/wikiwym
</VirtualHost>
```

Restart Apache and then point your browser at `http://wikiwym/`.

If all goes well, you'll then have a running copy of the server and client.