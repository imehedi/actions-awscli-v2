[![GitHub Actions release flow](https://github.com/imehedi/actions-awscli-v2/actions/workflows/release-flow.yml/badge.svg)](https://github.com/imehedi/actions-awscli-v2/actions/workflows/release-flow.yml)

# Action - AWS CLI V2

This action provides capability to run any of the AWS CLI commands using
version 2 of the CLI tool (currently `amazon/aws-cli:2.37.9`).

```yaml
- name: AWS CLI v2
  uses: imehedi/actions-awscli-v2@latest
  with:
    args: s3 ls
```

We are using the base image from AWS and simply providing a dockerised
interface to the tool, we can perform activities within our repo as if we
were using the tool locally.

```shell
aws s3 ls
```

## Credentials

### Recommended: OpenID Connect (no stored keys)

Let the workflow assume an IAM role with a short-lived token. The credentials
that `aws-actions/configure-aws-credentials` exports are passed into this
action's container automatically.

```yaml
permissions:
  id-token: write
  contents: read

steps:
  - name: Configure AWS credentials (OIDC)
    uses: aws-actions/configure-aws-credentials@v6
    with:
      role-to-assume: arn:aws:iam::123456789012:role/github-actions-role
      aws-region: eu-west-1

  - name: AWS CLI v2
    uses: imehedi/actions-awscli-v2@latest
    with:
      args: s3 ls
```

### Alternative: access keys from repository secrets

```yaml
- name: AWS CLI v2
  uses: imehedi/actions-awscli-v2@latest
  with:
    args: s3 ls
  env:
    AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
    AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
    AWS_DEFAULT_REGION: "eu-west-1"
```

## Materials for curious minds

* [AWS CLI V2 Changelog](https://github.com/aws/aws-cli/blob/v2/CHANGELOG.rst)
* [Configuring OpenID Connect in Amazon Web Services](https://docs.github.com/en/actions/security-for-github-actions/security-hardening-your-deployments/configuring-openid-connect-in-amazon-web-services)
* [How to add secrets to a repo](https://docs.github.com/en/actions/security-for-github-actions/security-guides/using-secrets-in-github-actions)