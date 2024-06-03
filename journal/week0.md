# Week 0 — Billing and Architecture

### Install AWS CLI

- We are going to install the AWS CLI when our Gitpod enviroment lanuches.
- We are are going to set AWS CLI to use partial autoprompt mode to make it easier to debug CLI commands.
- The bash commands we are using are the same as the [AWS CLI Install Instructions]https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html


Update our `.gitpod.yml` to include the following task.

```sh
tasks:
  - name: aws-cli
    env:
      AWS_CLI_AUTO_PROMPT: on-partial
    init: |
      cd /workspace
      curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
      unzip awscliv2.zip
      sudo ./aws/install
      cd $THEIA_WORKSPACE_ROOT
```

We'll also run these commands indivually to perform the install manually



### Create a new User and Generate AWS Credentials

- Go to (IAM Users Console) create a new user. I created a new user AwsAdmin user for cli access.
- `Enable console access` for the user
- Create a new `Admin` Group and apply `AdministratorAccess`
- Create the user and go find and click into the user
- Click on `Security Credentials` and `Create Access Key`
- Choose AWS CLI Access
- Download the CSV with the credentials

### Set Env Vars

We will set these credentials for the current bash terminal
```
export AWS_ACCESS_KEY_ID=""
export AWS_SECRET_ACCESS_KEY=""
export AWS_DEFAULT_REGION=us-east-1
```

- Checking AWS Configured credentials
```
  aws configure list
```
  
- checking aws caller identity
 ``` 
  aws sts get-caller-identity
 ```

### Faced commit error on GITPOD

while doing a commit through the left side commit button. It showed me that
"You din't have permissions to push to the repository"

- For this you need to open https://gitpod.io/access-control/ and give Gitpod permissions necessary to allow git push.
- You can solve it manually by navigating to https://gitpod.io/access-control/ and allowing "write public repos".

### Create a Budget
- Created a zero Doller billing Alarm
- Created a monthly Budget alarm of 10$



### Recreate Logical Architecture

![Crudder Logical Diagram](https://github.com/tkirar/aws-bootcamp-cruddur-2023-tk/assets/69767391/930db12d-6261-43e0-a005-f2c010546c14)




  

  
