
<!-- PROJECT LOGO -->
<br />
<p align="center">
  <a href="https://www.ecom.io">
    <img src="./ecom-logo.png" alt="Logo" width="80" height="80">
  </a>

  <h3 align="center">Cloud Architecture for ECOM website</h3>

  <p align="center">
    Host your e-commerce website on ECOM cloud.
    <br />
 


<!-- TABLE OF CONTENTS -->
<details open="open">
  <summary><h2 style="display: inline-block">Table of Contents</h2></summary>
  <ol>
    <li>
      <a href="#about-the-project">About The Project</a>
      <ul>
        <li><a href="#built-with">Built With</a></li>
      </ul>
    </li>
    <li><a href="#usage">Usage</a></li>
    <li><a href="#roadmap">Roadmap</a></li>
    <li><a href="#contributing">Contributing</a></li>
    <li><a href="#license">License</a></li>
    <li><a href="#contact">Contact</a></li>
  </ol>
</details>



<!-- ABOUT THE PROJECT -->
## About The Project

ECOM Multi Tenant E-commerce website on cloud

Network, Application Diagram and Architecture to host and monitor a e-commerce website on AWS cloud in efficient manner.
Services used are chosen in such a way that they will provide maximum throughput along with cost saving.
    
  <p align="center">
  <a href="https://www.ecom.io">
    <img src="./aws-network.png" alt="Network Diagram" width="1080" height="1920">
  </a>



### Built With

ECOM Technical Requirements
Phase Tools/Technology
* Store Template - HTML, CSS - React.js - Next.js (Server-side rendering). - Apollo - PWA
(Progressive Web App)
* Merchant App - React Native
* Merchant Panel - HTML, CSS - React.js - Apollo Super Admin Panel - HTML, CSS - React.js - Apollo Backend - MongoDB - NodeJS - GraphQL


<!-- GETTING STARTED -->
## Getting Started

To get a start you should visit https://www.ecom.io up and running follow steps.


### Setup

Description:
1. We used M4 type EC2 instance to bear high computation and storage.
2. AMI with the instance and assign a Auto Scaling group.
3. A Elastic Load Balancer with stickiness enabled to balance the network traffic efficiently.
4. backend database we will use RDS with multiple read replicas to store user data.
5. AWS ElastiCache for fast performance and less reads from database using cache.
6. We will use aws sns for email,text and other notifications.
7. Amazon Cloudwatch for continuous health check and monitoring.
8. Aws S3 for Static content and images and thumbnails.
9. AWS Route53 for DNS and routing.
10. AWS Cloudfront for for fast access to website through edge locations or delivering application.
11. Aws cognito for identity check/credential check.
12. Moreover we will use web clients for storing cookies and making website stateless.

Step-wise description:
1. User will access website and will be directed to route 53.
2. Route 53 will direct the traffic towards Cloudfront which serves data or point towards ELB depending upon scenario along with cognito checking identity.
3. ELB will direct traffic to EC2 ASG instances.
4. Static website data like product images and thumbnails will be served through aws s3.
5. ELB sticky session will make sure that user is connected to same instance.
6. For database EC2 instance will check Elasticache if it is a cache-hit it will server data or it will look into RDS and cache data.
7. Finally the data is served back to customer.
8. SNS will help in notification services like order confirmation calls or other notifications (Using lambda function or APIs)
9. CloudWatch will help to Monitor.

Security Perspective:
- Tight Security with security groups referencing each other. No instance or Database will be publicly accessible.


Based on our business requirements ECOM application architecture should look like this:

We implemented this architecture by building an Android App, an iOS App, a React based Javascript front end for Desktop and Mobile Web and have this connected through a node.js application that fetches you the product catalog, takes the order and gets your customers all the information about orders and account as and when required. You can store the product catalog and user and orders related information in a MySQL Database. If you are expecting your company to be wildly popular you may want the ability to deliver the product catalog to your customers super quick and have the ability to modify product information as and when you want. You can split your database into a product catalog database which you can store in a document database such as MongoDB or Couch DB and store your transaction related information like orders and customers information in MySQL database.

Signup and authentication
To signup and authenticate users into ECOM system you can store the user credentials and information in a MySQL database and use your node.js javascript code to manage the signup and authentication of users.

Search
Selecting a search algorithm for your product search on the site is dependent on the importance of search as a product discovery method on ECOM application. If you have few products and are not adding products every day or continuously, having a sophisticated search functionality may actually be a waste of time and resources, on the other hand if you have a large selection of products and you want customers to be able to accurately search for products you should have a sophisticated search engine that can understand customers intent better. Based on your need you can use full text search functionality of your database or use Elasticsearch or Solr.


Search prompts on Amazon
For example a customer searching for a phone should find the phone most relevant to his search. If a customers searching for
should get different search results and search results should be closest to what the customer has been searching for.

Integration with other systems
No application is an island so you would need to integrate ECOM applications with other systems such as payment gateway to take payments from customers, inventory management system to show customers available products, logistics and shipping to ship the order to customers and manage returns, CRM to manage the customer history and finance to manage all the financial information about a transaction conducted on your website. You can do all this by writing custom code for each application. The challenge you will face is that if your code fails then your order details may be lost leading to a customer satisfaction issue. It happens to Amazon so be assured that it can happen to you also. To overcome this you want a system where the disparate systems do not lose messages from other systems and all the interactions and interfacing occurs smoothly. You can build this using a Microservice architecture using a Messaging based system that uses messages to integrate disparate systems. While choosing the messaging system you have to ensure that the system runs all the time, does not lose any messages and if there are errors in messages the same should be alerted to the administrator. You do not want a system where the customer successfully pays for an order and the shipping system has no record of that order. A good choice would be between Rabbit MQ and Apache Kafka, both provide excellent message queues that allow you to integrate your e-commerce application to different systems. To get a better understanding and help you choose you can read this article Apache vs Rabbit MQ.

Notifications system
To keep your customers informed about everything that they are doing on your application like what are you doing about the orders, when is it shipped when is it arriving and so on, you need to send a large number of messages to the customer via WhatsApp, SMS/Text, e-mail and in-App, last I counted Amazon sent me 12 messages on different channels for a single order, this is when the order was shipped seamlessly. In case of delays and returns the number of messages increase exponentially. Add to that the need to authenticate the email and phone numbers of the customers again requiring another set of notifications. To cross-sell and up-sell to the customers you need to send a bunch of notifications both in-App and through e-mails, WhatsApp Messages and SMS/Text. This means you need a notification system that is able to send e-mails, WhatsApp Messages, SMS/Text and in-App notifications.


Different Kinds of Notifications
To enable all these notifications you would need to develop a robust and reliable notification system that sends e-mail, SMS/Text, Push Notification and WhatsApp messages, sometimes to the scale of millions of messages in a day (Assuming you become hugely successful).

Recommendation engine
A nice to have system on your website would be to show customers recommendations based on what they are looking at on the site, like Amazon’s the “customers who bought this also bought this section”, or based “order again” and here is your your browsing history.


Recommendations and browsing history based suggestions.
You can build this recommendations engine using a MySQL database, by running queries on previous orders and showing the result of the query on the results page of the customer. This will work efficiently if your customers are few and they don't mind the slow loading times of the search query. A more efficient way would be to store all your order data in a Redis database. You can use Redis to duplicate all your orders data from transactional database to the Redis database and then use Redis Sets to find items most associated with this kind of cart and sort the items in the different orders in order to find the highest scores to make a recommendation. Once we have the items we can pull their details from the product catalog in the MySQL database or Document store to show to the customer. Using Redis instead of making recommendations through a transactional database would be faster and easier and execute.

Amazon also shows you your browsing history, and recommendations based on your browsing history, and they do this across multiple devices. So if you have looked at a book in your app, it will show you the same book in your browsing history on the browser and vice-versa. And it is able to do so in under 5 seconds. Based on your browsing history it also sends you recommendations on email and sends you recommendations on the app and website. This feature is slightly complicated to implement as it uses things like streaming data analysis, or analyzing and using data while the data is still in motion. In simple terms it means that we are analyzing the data while it is still being generated instead of storing it in a data warehouse or a data lake for analyzing it in the future and act on a group of data. This is like personalization on steroids. Based on this streaming data we can recommend products, conduct fraud analytics and even train our AI models. The architecture for doing this is broadly -


Analyzing and using data while still in motion
We can use a combination of Kafka and Spark to achieve our goal of analyzing live or streaming data and making it actionable, where Kafka works as the message broker for events based and live data. The data received in Kafka can then be analyzed using Spark and converted into actionable information, such as data being passed to APIs, being visualized in a Dashboard or be used to send an Alert or notification and then eventually be stored in a long term data store for future analysis and as input for Artificial Intelligence and Machine Learning models.

Data Warehousing and analytics
Last but not the least for better management you need a system where you can analyze all the data coming in through various systems. You should be able to get a view of all the visitors coming in, time they are spending on the site, things they are buying or abandoning, products that are performing well, the marketing campaigns working and not working, the ads that are performing or not performing etc, analysis of the demographics of the customers and their performance and preferences by demographics. Add to that an analysis of the shipping and handling, and inventory, to understand products in stock, not in stock and the time taken to fulfill an order, so on and so forth.

With all the data collected you should be able to also created Machine Learning models and Artificial Intelligence models to better manage your business and merge this with human experience and expertise to create better advertising, marketing, shipping models.


Data Warehousing & Data Lake Architecte
We can create a warehousing and analytics sub-system using Kafka, Spark, HDFS and if the scale is pretty low using the normal RDBMS like MySQL. For Dashboard and Visualization we can use open source software like Superset or buy something like Qlikview or Tableau.

Designing the system for cloud
Now that we know the different components that we need to build and deploy we can go about developing the operational architecture of the e-commerce system. We know that we would need a Node.js server, a MySQL Server, Mongo DB, LDAP, Elastisearch, Rabbit MQ, Spark, Kafka, Tableau, LDAP etc. we can start by hosting instances of these application middlwares on Cloud providers like Amazon AWS and Microsoft Azure.


ECOM Solution Architecture Based on AWS Platform

E-Commerce Solution Architecture Based on Azure Platform
As you can see to achieve high availability and resilience we would need to host these applications on multiple virtual machines or EC2 instances to achieve high availability. That would be a lot of machines and for those machines we would need a large number of human resources to man those machines for availability, scaling and performance. Needless to say some of these machines would be running at very low capacities initially. Overall this becomes a very expensive proposition.

Now lets step back and think how we can leverage the cloud to be more than just network, storage and computing resource provider. How do we leverage it so that our operational overheads, costs and development times are greatly reduced while our solution and software capabilities increase substantially. As you can see from the graphics above these cloud providers do not just provide the compute resources, they also provide these platforms and softwares as a service. So instead of hosting our own MySQL server and MongoDB and managing its availability and scaling, we let Amazon or Microsoft do it and we just use these database services (like Amazon RDS MySQL, Amazon Dynamo DB, Azure Database for MySQL, Azure Cosmos DB) in our application. Similarly instead of building our own authentication subsystem we use Amazon Cognito or Azure Active Directory B2C to signup users, and manage their sessions. For search we don’t build our own instead using Amazon CloudSearch or Azure Cognitive Search. For integration instead of building our own highly available Rabbit MQ / Kafka based integration we can build using Amazon SQS or Azure Services Bus, which does everything we need at scale. For notifications we can use the best in class service available from Amazon — Amazon SNS which can take care of SMS/Text, e-mail and In-App notifications, building this on your own would mean integrating different vendors and managing a large number of moving parts to achieve the same functionality and reliability. Microsoft Azure does provide equivalent service through Azure Notifications Hub and Azure Services Hub but you would have to integrate third party providers such as Sendgrid and Twilio to send notifications through e-mail and SMS/Text. Lastly for building e-commerce recommendations engine and doing data warehouse, analytics and analytics based marketing you can use Amazon Pinpoint (For events and analytics based marketing, Azure does not have an equivalent product), Amazon Redshift or Azure Data Lakes Analytics (for data lakes, data warehouse), Amazon Kinesis & Amazon Athena (for recommendations engine and analytics) and Amazon Quicksight (for Dashboard and KPIs management).

As you can infer, for all technical requirements you can use the cloud platform components provided by AWS and Azure to run your e-commerce application, and let them manage the operations and running of the infrastructure while you focus on development and strategy. In fact if you repurpose your code to run on AWS Lambda or Azure Function you can host your entire application serverlessly.




<!-- CONTACT -->
## Contact

Email : abdelwahidjr@cryptdev.com
