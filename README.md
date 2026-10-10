# PT Logitek Website

Static Astro homepage for PT Logitek Communication Services. Phase 2A expands positioning toward foreign investors while retaining the Pakistan–Indonesia connection. Shared navigation, value propositions, services, checklist, and process content live in `src/data/content.ts`; design tokens live in `src/styles/global.css`.

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

Contact phone, WhatsApp, email, representatives, and booking destination remain unverified. Consultation links lead to an honest contact-information section, not to a working booking flow. Replace the unavailable contact channels with verified information before inviting customer enquiries.

The Phase 2A text brief refers to a foreign-investor poster, but the poster image was not included in the supplied attachment or repository. The navy/red/gold/cream palette and abstract architectural illustration interpret the written direction; verify against the actual poster when it is supplied. No third-party photography was added.
