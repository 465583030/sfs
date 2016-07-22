# sfs

A go-based static file web server for serving files from a directory on macOS, Windows, or Linux.

Intended as a lightweight development tool for viewing static sites, e.g. documentation, blogs, diagnostic reports, HTML mockups, and early prototypes.

## Install

- [Download the zero-install binary](https://github.com/schmich/sfs/releases) to a directory on your `PATH`; or
- `go get -u github.com/schmich/sfs/... && go install github.com/schmich/sfs/...`

## Usage

```
Usage: sfs [OPTIONS]

Static file server - https://github.com/schmich/sfs

Options:
  -v, --version                          Show the version and exit
  -p, --port=8080                        Listening port
  -i, --iface, --interface="127.0.0.1"   Listening interface
  -g, --global=false                     Listen on all interfaces (overrides -i)
  -d, --dir, --directory="."             Directory to serve
  -B, --no-browser=false                 Do not launch browser
  -t, --trace=""                         Trace format (%i %t %m %u %s %b %a)
  -c, --cache=false                      Allow cached responses
```

Start a web server for files in the current directory:

```
sfs
```

Specify a port:

```
sfs -p 777
```

Allow external connections:

```
sfs -i 0.0.0.0
sfs -g
```

Serve files from another directory:

```
sfs -d ../bloop
```

## Logging

Trace and log requests with `-t`:

```bash
sfs -t "%i - [%t] %m %u %s %b - %a"
# 127.0.0.1 - [21/Jul/2016:21:07:51 -0500] GET / 200 273 - Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/51.0.2704.103 Safari/537.36 
```

Log format:

- `%i` Remote IP address
- `%t` Request timestamp
- `%m` Request HTTP method
- `%u` Request URL
- `%s` Response status code
- `%b` Response length (bytes)
- `%a` Request user agent (`User-Agent` HTTP header)

## Caching

By default, `sfs` modifies incoming and outgoing cache headers (`Cache-Control`, `If-None-Match`, `If-Modified-Since`) to ensure no caching occurs. To allow caching, this can be disabled with:

```
sfs -c
```

## License

Copyright &copy; 2016 Chris Schmich
<br />
MIT License. See [LICENSE](LICENSE) for details.
