---
title: "Blog 3: Automated Cloud Security Monitoring with Amazon GuardDuty"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 3. </b> "
---

### The Importance of Cloud Security
During the project deployment, I realized that merely storing logs is not enough. System engineers need immediate alerts if someone is trying to compromise their AWS accounts.

### The Power of Amazon GuardDuty
I configured **Amazon GuardDuty** - a threat detection service utilizing Artificial Intelligence (AI) and Machine Learning. GuardDuty continuously analyzes VPC Flow Logs and CloudTrail to search for anomalies.
In a testing scenario, I deliberately used Root credentials to call the GetCostAndUsage API. Almost instantly, GuardDuty detected this and generated a Finding:
> "The API GetCostAndUsage was invoked using root credentials."

### Lessons Learned
Using the Root account for daily tasks is a massive security vulnerability. Through this project, I applied the **Principle of Least Privilege**: creating specific IAM Users and granting them exactly the permissions they need instead of using Root. GuardDuty acts as a silent guardian, ensuring the entire AWS system remains secure 24/7.
