# CertOne confidential compliance scan (GitHub Action)

Sends the AI project to CertOne, where it is scanned inside an attested confidential computer
(AMD SEV-SNP VM or Kata confidential containers), and fails the job unless the verdict passes.
The verdict, where it ran and the findings are written to the job summary; the findings are also
written as SARIF (`certone.sarif`) for GitHub code scanning.

```yaml
permissions:
  contents: read
  security-events: write   # upload the SARIF to code scanning

steps:
  - uses: actions/checkout@v4
  - uses: admin-certkorai/certone-action@v1
    with:
      api-key: ${{ secrets.CERTONE_API_KEY }}
      path: adas-perception
      asset: "ADAS Forward Perception"
      country-code: EU
  - uses: github/codeql-action/upload-sarif@v4
    if: always()
    with:
      sarif_file: certone.sarif
      category: certone-adas-perception
```

The API key is read from a secret and never printed. The action installs `certone-sdk` from PyPI.
