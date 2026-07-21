---
title: "2. Prerequisites"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.2. </b> "
---

To complete this Workshop, you need to prepare the following tools and resources:

### 1. AWS Account & IAM User
Absolutely **DO NOT** use the Root account for this lab. (As seen in the GuardDuty findings later, using Root to call APIs is flagged as a security risk).

**Steps to create a proper IAM User:**
1. Log in to AWS using the Root account, open **IAM Console** -> **Users** -> **Create user**.
2. Name the User (e.g., `huynhtuan1`) and check **Provide user access to the AWS Management Console**.
3. In the Set permissions section, select **Attach policies directly** and grant `AdministratorAccess`.
4. Finish creating the User, copy the password and login URL.
5. Log out of the Root account and **log back in using the newly created IAM User**.

* Select Region: `us-east-1` (N. Virginia) or `ap-southeast-1` (Singapore) for the entire Lab.

![Create IAM User](/images/Workshop/iam_user.jpg)

### 2. Tools
* Web browser (Chrome/Firefox).
* [AWS CLI](https://aws.amazon.com/cli/) installed and configured using `aws configure` (using the Access Key of the newly created IAM User).
* (Optional) **AWS Cloud9** environment to run code.

*(Note: For the IAM Role of Lambda and other services, we will use the AWS Console's automatic role creation mechanism in this Workshop to speed up deployment).*
