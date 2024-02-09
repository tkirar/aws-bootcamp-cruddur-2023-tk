# Week 0 — Billing and Architecture

## Install AWS CLI and ensure it works.

Currently i'm working on ubuntu and going to install AWS CLI on ubuntu using terminal.
- Installed awscli using
```sh
  apt install awscli
```
![Screenshot from 2024-01-27 01-15-15](https://github.com/tkirar/aws-bootcamp-cruddur-2023-tk/assets/69767391/39f844ab-dc1e-4bc5-b71e-cfe9d29d4085)



- Configuring AWS Credentials and Access keys
 ```
  aws configure
 ```
 
- Checking AWS Configured credentials
```
  aws configure list
```
  
- checking aws caller identity
 ``` 
  aws sts get-caller-identity
 ```

### Create a Budget
- Created a zero Doller billing Alarm
- Created a monthly Budget alarm of 10$
  
### Recreate Logical Architecture

![Cruddur Logical](https://github.com/tkirar/aws-bootcamp-cruddur-2023-tk/assets/69767391/26cbccfb-0e55-4ce4-97d6-f62cd8837898)




  

  

  
