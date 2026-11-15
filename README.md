# CertOne confidential compliance scan (GitHub Action)

Sends the AI project to CertOne, where it is scanned inside an attested confidential computer
(AMD SEV-SNP VM or Kata confidential containers), and fails the job unless the verdict passes.
The verdict, findings and (for a pass) the attestation are written to the job summary.

```yaml
- uses: actions/checkout@v4
- uses: admin-certkorai/certone-action@v1
  with:
    api-key: ${{ secrets.CERTONE_API_KEY }}
    path: adas-perception
    asset: "ADAS Forward Perception"
    country-code: EU
```

The API key is read from a secret and never printed. The action installs `certone-sdk` from PyPI.
