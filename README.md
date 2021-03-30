# Action - AWS CLI V2

This action provides capability to run any of the AWS CLI commands using 
version 2 of the CLI tool.

```yaml
- name: AWS CLI v2
  uses: imehedi/actions-awscliv2@v1
  with:
    args: s3 ls
```

We are using the base image from AWS and simply providing a dockerised 
interface to the tool, we can perform activities within our repo as if we 
were using the tool locally.

```shell

aws s3 ls
```

The above then requires us to pass the credentials from GitHub secrets, 
which we can do as below:

```yaml
- name: AWS CLI v2
  uses: imehedi/actions-awscliv2@v1
  with:
      args: s3 ls
  env:
      AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
      AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
      AWS_DEFAULT_REGION: "eu-west-1"
```

###Materials for curious minds

* [AWS CLI V2 Changelog](https://github.com/aws/aws-cli/blob/v2/CHANGELOG.rst)
* [How add secrets to repo?](https://docs.github.com/en/actions/reference/encrypted-secrets#creating-encrypted-secrets-for-a-repository)