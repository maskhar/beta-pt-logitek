# PT Logitek Website Prototype

Static Astro recreation of the supplied `PT Logitek Communication Services.html` template.

## Local development

```bash
npm install
npm run dev
```

Open `http://localhost:4321`.

## Quality checks

```bash
npm run check
npm run lint
npm run build
```

## Docker deployment

Host port `8088` was selected after checking local listeners and Docker-published ports. It binds only to loopback so an existing reverse proxy or tunnel can route the production hostname safely.

Required external Docker networks:

- `carubra-network`
- `uteroindonesia-network`
- `utero-id-network`

Create only missing networks:

```bash
docker network create carubra-network
docker network create uteroindonesia-network
docker network create utero-id-network
```

Build and start:

```bash
docker compose build
docker compose up -d
docker compose ps
```

Runtime checks:

```bash
curl http://127.0.0.1:8088/
curl http://127.0.0.1:8088/health
docker inspect pt-logitek-web
```

## NGINX and domain

NGINX serves the static Astro output on container port `80`, exposes `/health`, enables compression and static-asset caching, and sends baseline security headers. Production hostname is `logitek.carubra.com`.

DNS and TLS remain external infrastructure concerns. Route the hostname through the existing reverse proxy or tunnel to `http://127.0.0.1:8088`; do not bind this Compose stack over host ports `80` or `443`.

The supplied template has placeholder contact fields (`[number]`, `[email]`, `[website]`, `[contact]`). The consultation CTA in the contact section links to that same section, as in the source. Replace these with verified contact information and a booking destination before publishing to customers. The source hides section navigation at widths up to `860px`; this prototype retains that visual behavior.
