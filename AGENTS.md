# Lesson 6 — notes for agents

## What this project is
`Lesson 6/` is a flat folder of standalone HTML/CSS/JS practice pages uploaded to the
repo. There is no package manager, build step, framework or backend, and no
`index.html`; files are not wired to each other.

## How it runs
`docker-compose.base44.yml` serves `Lesson 6/` with a stock `nginx:1.27-alpine`
container, bind-mounted read-only at the web root on host port 3000.
`docker/nginx.conf` enables `autoindex` so the directory listing is the entry point
(without it the root would 403 because no `index.html` exists).

```sh
docker compose -f docker-compose.base44.yml up -d
```

Pages are read straight off the bind mount, so edits to files under `Lesson 6/`
appear on reload with no restart or rebuild. Only a change to
`docker/nginx.conf` needs `docker compose -f docker-compose.base44.yml restart web`.

## How to verify
`curl -s -o /dev/null -w '%{http_code}' http://localhost:3000/` → 200, and any page,
e.g. `/000666999.html`, → 200.

## Quirks
- No external services or credentials are required; the only network dependency is a
  Bootstrap 4 CDN stylesheet linked by a couple of pages.
- Some filenames are unusual (`====.html`, `D9.HTML`, `32`), and a few files
  (`364.html`, `dc.html`, `cd`, `tj.js`, `skill.d`, `dkw.s`, `222817/sw2`) are empty
  placeholders.
