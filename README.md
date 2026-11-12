# localhost

A small static file server for your own machine. It binds to `127.0.0.1` and serves one or more folders on one port.

Website: https://megamanics.github.io/localhost/

## Install

```
brew install megamanics/tap/localhost
```

This works on macOS and Linux. The same binaries, with checksums, are on the [releases page](https://github.com/megamanics/localhost/releases).

## Use

```
localhost [DIR] [NAME=DIR ...] [--port N] [--addr A] [--auth] [--quiet]
```

With no arguments it serves the current directory at `http://127.0.0.1:8000/`. Each `NAME=DIR` is served at `/NAME/`.

```
localhost 3d=~/prj/3d docs=~/notes/site
```

That gives you `http://127.0.0.1:8000/3d/` and `http://127.0.0.1:8000/docs/`. Run `localhost --help` for the rest.

## Docker

Each folder mounted under `/srv` becomes a path.

```
docker run -d --name localhost -p 127.0.0.1:8000:8000 \
  -v ~/prj/3d:/srv/3d:ro -v ~/notes/site:/srv/docs:ro megamanics/localhost
```

To keep it always on, download [compose.yaml](compose.yaml) and run:

```
docker compose up -d
```

That serves `~/prj` at `http://127.0.0.1:8000/`, read-only. Set `LOCALHOST_ROOT` to serve another folder and `LOCALHOST_PORT` to use another port.
