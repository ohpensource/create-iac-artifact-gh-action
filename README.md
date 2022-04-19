# CREATE-IAC-ARTIFACT-GH-ACTION

Repository containing Ohpen's Github Action to create and upload the folder with IAC content.

- [CREATE-IAC-ARTIFACT-GH-ACTION](#TERRAFORM-APPLY-GH-ACTION)
  - [code-of-conduct](#code-of-conduct)
  - [github-action](#github-action)

## code-of-conduct

Go crazy on the pull requests :) ! The only requirements are:

> - Use _conventional-commits_.
> - Include _jira-tickets_ in your commits.
> - Create/Update the documentation of the use case you are creating, improving or fixing. **[Boy scout](https://biratkirat.medium.com/step-8-the-boy-scout-rule-robert-c-martin-uncle-bob-9ac839778385) rules apply**. That means, for example, if you fix an already existing workflow, please include the necessary documentation to help everybody. The rule of thumb is: _leave the place (just a little bit)better than when you came_.

### github-action

This action will zip and upload to S3 the IAC folder that is specified. The (required) inputs are:

- _region_: aws region name.
- _access-key_: user access key to be used.
- _secret-key_: user secret key to be used.
- _destination-account_: AWS account id where the S3 bucket is located.
- _role-name_: IAM role to assume when uploading the artifact.
- _version_: Unique version of the artifact being uploaded (1.2.3, 1.5.8.1, feature/branch, ...)
- _service-name_: Name of the unique service.
- _iac_: folder where the IAC is located.
- _butcket-name_: Name of the bucket to upload the artifact

Here is an example:

```yaml
name: CI
on:
  pull_request:
    branches: ["main"]
jobs:
  upload-iac-artifact:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: ohpensource/platform-cicd/actions/artifacts/create-iac-artifact@0.0.0.1
        name: Upload Terraform artifact
        with:
          region: $REGION
          access-key: $COR_AWS_ACCESS_KEY_ID
          secret-key: $COR_AWS_SECRET_ACCESS_KEY
          destination-account: $ARTIFACTS_AWS_ACCOUNT_ID
          role-name: $COR_CICD_AUTOMATION_ROLE_NAME
          version: $GITHUB_HEAD_REF
          service-name: $SERVICE_NAME
          iac: $IAC
          butcket-name: $ARTIFACTS_BUCKET_NAME
```
