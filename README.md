# amplify-ruby-image

Creates a minimal Docker image based on the official Ruby image in Docker Hub. This is intended to be used as the base image for Jekyll static sites to be deployed via Amplify, as the AWS base image installs Ruby 2.7 but not Ruby 3+. This is also a minimal image - the AWS image not only installs Ruby but also two versions of Python, dot.NET, and other tools that are not needed for a Jekyll site.

## Usage
1. Create a public image repository somewhere (we are using a public ECR in AWS) and find the URI for the repository.
2. Build the image: `docker build . -t <image-repository-uri>:<tag>`
3. Push the image: `docker push <image-repository-uri>:<tag>`

## Notes about AWS public ECR
The AWS public ECR is a little different than a standard ECR. You can't use the AWS CLI to push to it, and you can't use the AWS CLI to log in to it. Instead, you need to use the AWS CLI to get a login token, then use the Docker CLI to log in to the repository. The following commands will log you in to the public ECR:

```
aws ecr-public get-login-password --region us-east-1 --profile <aws-profile> | docker login --username AWS --password-stdin public.ecr.aws/<aws-account-id>
```
