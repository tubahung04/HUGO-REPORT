---
title: "Blog 3"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---

# How Hypermonk Games Built a Game Analytics Platform on AWS — What I Learned After Reading an AWS Blog

Hello everyone,

While exploring AWS, I regularly read articles on the **AWS GameTech Blog** to understand how businesses apply AWS services to real-world problems. Recently, I read the article ["Hypermonk Games transforms mobile game development with data powered by AWS"](https://aws.amazon.com/blogs/gametech/hypermonk-games-transforms-mobile-game-development-with-data-powered-by-aws/), and I found it a very valuable read for anyone interested in Data Architecture or game development on the Cloud.

At first, I thought the article would only list the AWS services Hypermonk Games used. But after finishing it, I realized what the author wanted to emphasize wasn't any single service — it was how they were combined to build a complete data analytics system, helping the development team make data-driven decisions instead of relying on intuition.
![Blog 3](/images/Blog/blog3.jpg)
### Player Data — An Important Asset of a Game

The first thing that impressed me was how Hypermonk Games treats player data as an important asset. Every player action — starting a level, completing a quest, watching an ad, or making a purchase — generates valuable data.

Without a proper collection and analytics system, this volume of data becomes very hard to leverage. Understanding player behavior, evaluating in-game event effectiveness, or optimizing revenue would take a lot of time and could easily lead to inaccurate decisions.

### The Solution: Building a Data Analytics Platform on AWS

What I found interesting is that Hypermonk Games built an internal platform called **Orange**, based on AWS services.

Data from the game is sent in real time through **Amazon Kinesis**, then processed by **AWS Lambda** before being stored in **Amazon S3** and **Amazon DynamoDB**. Services such as **Amazon Athena**, **Amazon EventBridge**, and **Amazon SQS** are used to query data, orchestrate events, and handle asynchronous tasks.

Thanks to this architecture, the development team can monitor player behavior almost in real time, easily run A/B tests, evaluate advertising campaign performance, and optimize in-game experiences.

### Automation Helps Optimize Operations and Reduce Cost

I think the article's strongest point isn't just its data collection capability, but how Hypermonk Games optimized the system after going live.

The article shares that they applied storage lifecycle policies on **Amazon S3** to significantly reduce long-term storage costs, while adjusting **Amazon DynamoDB** configuration based on actual usage traffic to optimize operational costs.

This shows that when building systems on the Cloud, optimizing cost is just as important as building a stable, functioning architecture.

### A Real-World Example of Data Architecture on AWS

Something I liked about the article is that the author doesn't just introduce each AWS service individually — it shows how multiple services combine into a complete system.

Through the article, I better understood how components like **Amazon Kinesis**, **AWS Lambda**, **Amazon S3**, **Amazon Athena**, **Amazon DynamoDB**, **Amazon EventBridge**, and **Amazon SQS** work together to build a scalable data pipeline capable of handling large volumes of events from a game.

### Personal Reflection

After reading this blog, I realized that data isn't just for statistics — it plays a crucial role throughout the entire product development process.

Instead of making decisions based on gut feeling, developers can rely on real data to optimize gameplay, improve player experience, and increase business efficiency. The article also helped me understand how AWS supports businesses in building scalable, cost-optimized data analytics systems.

### Conclusion

For me, this article isn't just about how Hypermonk Games uses AWS — it offers a practical perspective on building a data platform for modern game development.

If you're exploring AWS, Data Engineering, or real-time data processing architectures, I think this is a very worthwhile read. Thank you for taking the time to read my sharing. If you've built a data analytics system on AWS or have experience with data pipelines, I'd love to hear more from you.

**Original article:** <https://www.facebook.com/groups/awsstudygroupfcj/permalink/2209746196457007/?rdid=5qxZq6kRlOs3vf1O#>
