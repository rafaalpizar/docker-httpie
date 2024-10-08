# docker-httpie with Akamai edgegrid

[If enjoy, please consider buying original author a coffee.](https://www.buymeacoffee.com/ozbillwang)

httpie running in docker alpine (python3+pip3+alpine+httpie+httpie-edgegrid)

### Github Original Repo

https://github.com/alpine-docker/multi-arch-docker-images/tree/master/httpie

### Github This Repo

https://github.com/rafaalpizar/docker-httpie

### Docker Build

1. Download Dockerfile

2. Build. Make sure you are in the folder where you have this Dockerfile and run the following command in the terminal:

```bash
docker build -t httpie-edgegrid .
```

### Usage
Always map your edgerc file:

```bash
$ alias http='docker run -ti --rm -v ~/.edgerc:/root/.edgerc httpie-edgegrid'
$ alias https='docker run -ti --rm -v ~/.edgerc:/root/.edgerc --entrypoint=https httpie-edgegrid'
```

To use and persist a [`.netrc`](https://httpie.org/docs#netrc) file:

```bash
$ alias http='docker run -ti --rm -v ~/.edgerc:/root/.edgerc -v ~/.netrc:/root/.netrc httpie-edgegrid'
$ alias https='docker run -ti --rm -v ~/.edgerc:/root/.edgerc -v ~/.netrc:/root/.netrc --entrypoint=https httpie-edgegrid'
```

A `.netrc` file must exist at `~` on the host.

`/root/.netrc` is used because httpie is run as root in the container, and it
looks to the user's home directory (`/root`) for the `.netrc` file.

To use and persist a [`.httpie`](https://httpie.org/docs#config) configuration
directory:

```bash
$ alias http='docker run -ti --rm -v ~/.edgerc:/root/.edgerc -v ~/.httpie:/root/.httpie httpie-edgegrid'
$ alias https='docker run -ti --rm -v ~/.edgerc:/root/.edgerc -v ~/.httpie:/root/.httpie --entrypoint=https httpie-edgegrid'
```

The `~/.httpie` directory on the host will be created automatically if it does
not exist already. You will notice a `~/.httpie/config.json` is created by
httpie if one did not exist.

This will create a temporary alias. In order to make it persist reboots,
you can append this exact line to your `~/.bashrc` (or similar) like this:

```bash
$ alias http >> ~/.bashrc
$ alias https >> ~/.bashrc
```

Running HTTPie is as simple as invoking it like this:

> _From [the official examples](https://github.com/jakubroztocil/httpie#examples):_

Hello World:

```bash
$ https httpie.io/hello
```

Custom [HTTP method](https://httpie.io/docs#http-method), [HTTP headers](https://httpie.io/docs#http-headers) and [JSON](https://httpie.io/docs#json) data:

```bash
$ http PUT example.org X-API-Token:123 name=John
```

Submitting forms:

```bash
$ http -f POST example.org hello=World
```

Upload a file using redirected input:

```bash
$ http example.org < file.json
```

Download a file and save it via redirected output:

```bash
$ http example.org/file > file
```

You can supply any number of [HTTPie arguments](https://github.com/jakubroztocil/httpie#readme)
that will be passed through unmodified.

### Help

HTTPie has a fairly [extensive documentation](https://github.com/jakubroztocil/httpie#readme) available.
Also, you can use its included help output:

```bash
$ http --help
```
