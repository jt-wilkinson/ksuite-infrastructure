# KSuite Infrastructure

Sanitized infrastructure patterns for the KSuite application stack.

This repository is intentionally narrow: it describes CI, container boundaries, environment configuration, and release hygiene without including application source, credentials, private hostnames, local paths, caches, or generated exports.

## Topology

```text
GitHub push / pull request
          ↓
GitHub Actions: Python tests + web lint/test/build
          ↓
container images or packaged artifacts
          ↓
explicitly configured deployment environment
```

The production API is the only authority for machine-ready PES output. The web studio must remain honest when that API is unavailable.

## Configuration contract

Set deployment values through the platform secret/configuration store. Never commit `.env` files or credentials.

- `KSUITE_CORS_ORIGINS` — explicit allowed web origins.
- `KSUITE_CPU_WORKERS` — bounded CPU worker count.
- `KSUITE_JOB_COORDINATORS` — lightweight async coordinator count.
- `NEXT_PUBLIC_KSUITE_API_URL` — public API origin for the web studio.
- `NEXT_PUBLIC_PAYMENTS_LIVE` — keep false unless verified checkout and webhook handling exist.

## Operational notes

- Async job state is process-local and expires after one hour.
- Use one API process per instance unless durable job storage is designed.
- Treat generated PES and preview files as diagnostic artifacts unless a test owns them.
- A public macOS release requires signing and notarization.
- A sew-out remains the final production gate.

## Security hygiene

The repository is sanitized by construction. Before publishing, scan history and the working tree for tokens, private URLs, local paths, environment files, and generated binaries. Rotate any credential that has ever been committed.

## License

MIT License. See `LICENSE`.
