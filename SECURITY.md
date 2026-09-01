# Security policy

## Reporting

Please do not open a public issue for a suspected credential leak or vulnerability. Contact the maintainer privately through the GitHub profile so the report can be triaged safely.

## Repository hygiene

CI rejects common token and private-key patterns. This is a backstop, not a substitute for secret management: use the deployment platform's secret store and rotate credentials immediately if exposure is suspected.
