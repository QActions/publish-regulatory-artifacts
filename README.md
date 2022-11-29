# Publish regulatory artifacts

Publishes the regulatory artifacts to the correct location to be read by the Software Lifecycle Tool.

- Uploads test results to the targeted regulatory S3 bucket
  - The source file in Junit format, `test-reports/junit.xml` by default.
  - Target file in the root folder for the correct project/commit:
    `s3://${REGULATORY_S3_BUCKET}/projects/${project_name}/commits/${short_sha}/test-results.xml`

Expected environment variables:
```sh
# Settings
REGULATORY_S3_BUCKET=regulatory.extrahorizon.com
TEST_RESULTS_PATH=test-reports/junit.xml # Optional

# AWS credentials
AWS_ACCESS_KEY_ID=......
AWS_SECRET_ACCESS_KEY=......
AWS_REGION=eu-central-1
```

Example usage:
```yml
jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repo
        uses: actions/checkout@v2

      - name: Publish regulatory artifacts
        uses: QActions/publish-regulatory-artifacts@1.1.0
        env:
          REGULATORY_S3_BUCKET: regulatory.extrahorizon.com
          AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
          AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          AWS_REGION: ${{ secrets.AWS_REGION }}
```
