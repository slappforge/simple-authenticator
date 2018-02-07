# Simple Authenticator

This is a databases backed simple authenticator implementation using AWS RDS, API Gateway and Lambda.

## Prerequisites

All the deployments of this application are based on Amazon AWS. To open the project, you will need the Sigma IDE which can be found at [Sigma IDE](https://sigma.slappforge.com). You will need to create an account and provide your AWS credentials to open the project (Your AWS credentials will not be acquired by SLAppForge under any circumstances).

## Use Case Description

This application is supposed to showcase a simple authenticator implementation using AWS RDS, API Gateway and Lambda.

It will create an RDS MySQL instance by instance identifier `authDatabase` and initialize it with the following DDL.
 
```sql
CREATE TABLE users (    
    UserId int NOT NULL AUTO_INCREMENT,
    Email varchar(255) NOT NULL UNIQUE,
    Password varchar(255) NOT NULL,
    LastName varchar(255),
    FirstName varchar(255),
    Address varchar(255),
    PRIMARY KEY (UserId)
);
```

Further it will create an API Gateway proxy by the name `auth-api` with two endpoints, one for `signup` (https://{api-id}.execute-api.{region}.amazonaws.com/prod/signup) and the other for `signin` (https://{api-id}.execute-api.{region}.amazonaws.com/prod/signin).

## Getting Started

In order to get started you just have to open the sample project from the SLAppForge IDE and deploy it on top of your AWS account. While deploying the project, IDE will get a clone of this and commit it to your own GitHub account to allow you to keep playing with the source code to get familiar with the application.

## Deployment

Click on the deployment button and it should deploy all lambdas that are required to run the application.

## Testing

After the deployment, you can test this sample application by first sending HTTP request to signup and then by sending another request to signin. First we need to find the URL of the created API Gateway proxy "auth-api". To find the endpoint URL, please follow these steps.

1. Sign in to the AWS Management Console, and then open the API Gateway console at [https://console.aws.amazon.com/apigateway/](https://console.aws.amazon.com/apigateway/ "Amazon API Gateway").
2. Make sure that you are signed in to the AWS region where you selected when creating the Sigma project.
3. On the API Gateway page, in the APIs list, look for the name "auth-api".
4. Select the API entry and then click on the the Stages menu in the navigation pane. Now click on the prod stage. Then copy the invoke URL value in the format of https://{api-id}.execute-api.{region}.amazonaws.com/prod.
5. Similarly find the other invoke URL as well.
6. Now, first to signup, send an HTTP POST request to the signup endpoint (https://{api-id}.execute-api.{region}.amazonaws.com/prod/**signup**) you found in the earlier step with a sample JSON payload as follows.
```json
{
  "email": "rajind@adroitlogic.com",
  "password": "12345678",
  "lastName": "Ruparathna",
  "firstName": "Rajind",
  "address": "12 A /5, Pirivena Rd, Mount Lavinia"
}
```
7. In the signup call an entry will be added to the users table. If you were successful you'll get a 200 OK response with the response message `Successfully added a new user with email`.
8. Then, to check the signin, send an HTTP POST request to the signin endpoint (https://{api-id}.execute-api.{region}.amazonaws.com/prod/**signin**) you found in the earlier steps with a sample JSON payload as follows. Note that the values should match the values used in signup request.
```json
{
  "email": "rajind@adroitlogic.com",
  "password": "12345678"
}
```
If the signin is successful you'll get a `200 OK` response with the response message `true`.

## Authors

* **Randika Navagamuwa**
* **Rajind Ruparathna**

## License

```
Licensed under the Apache License, Version 2.0 (the "License"); you may not use this file except in 
compliance with the License. You may obtain a copy of the License at 

http://www.apache.org/licenses/LICENSE-2.0 

Unless required by applicable law or agreed to in writing, software distributed under the License is 
distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. 
See the License for the specific language governing permissions and limitations under the License. 
```

## Acknowledgments

* Awesome SLAppForge team
