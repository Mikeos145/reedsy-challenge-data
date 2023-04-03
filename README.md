# reedsy-challenge-data
reedsy technical task

**Question 0
Write a paragraph about yourself, your hobbies and your major achievements in your career or study so far. Add another one about your professional experience and commercial projects you've been involved with.**

Hi, I’m Michael - I’m an outgoing, social person with a positive outlook on life. I enjoy physical activities, frequently involving myself in sports, outdoor pursuits and adventure based getaways. I love nature, hold the value of friends and family in high regard, and enjoy challenging myself mentally, always looking to expand my skill and knowledge base. My major achievements in my career and study so far include receiving a 1st Class Hons Degree, gaining a placement at IBM and then going on to start from the bottom on a Data Analyst Internship and working my way up through two promotions to managing the biggest account in the business (Amazon) within 9 months. 

Since then I’ve applied my skills across a broad range of settings, never resting on my laurels, but always looking to take on new challenges, self-teaching to meet those. In my last role this took the form of working on two academic papers with Imperial College London which are soon to be published as well as developing a publicly accessing respiratory data hub to democratise respiratory data for campaigners and patients alike. In my current role, I came in to a business with no analytics tech stack and a scattered, error prone “system” of manual reporting. Within 10 months, I provided stop gap solution for automated reporting, while scoping, designing and implementing a full, best in class, analytics tech stack, to set the business up for scale. This includes ETL, Data Warehousing, Reverse ETL and BI Tool (Tableau) with a full suite of dashboards to serve 4 distinct areas of the business. These are Engagement and Programmes, Commercial, Product and Leadership.

**Question 1
The Marketing Team at Bookly wants to merge and analyze all the data that is being collected by the different products in order to extract useful business insights of various kinds. Examples of such analytics include (but are not restricted to):**

**List all-time top rated books and trending ones;**
**Measure user sign-up rate over certain periods (weekly, quarterly, etc);
Show the total number of real-time (current) page views for any given book description page (product page);
...**

**Design a conceptual data pipeline to drive and aggregate data from all the different sources to ultimately be accessible by a user-friendly data exploration/dashboarding tool of your choice. Feel free to pick any technology available (e.g. open source, cloud providers, etc.).**

**Describe the different components of the architecture, tools involved and compare possible approaches.****

**TL;DR**
This is a data pipeline that covers data collection and integration, data transformation, data storage, data exploration/dashboarding, communications, and orchestration. The principles it follows are scalability, ease of use, maintenance, governance, and collaboration. The recommended stack is a GCP first stack, and while combining services from other providers is possible, there are advantages in sticking to one service provider where possible. The data pipeline starts with various data sources, and an ETL tool like Fivetran is recommended for data collection and integration. For data transformation, dbt Cloud is used, and for storage, BigQuery is recommended. Tableau is used for data exploration/dashboarding, and for communications, Customer.io is used. dbt Cloud and Fivetran are used for orchestration. 

**Detail**
The below data pipeline will cover the following areas:

<li>Data Collection & Integration
<li>Data Transformation
<li>Data Storage
<li>Data Exploration/Dashboarding
<li>Communications
<li>Orchestration 

It has been suggested based on the following principles:

<li>Scalability
<li>Ease of use
<li>Maintenance
<li>Governance 
<li>Collaboration

I have chosen a GCP analytics tech stack and while combining services across the likes of GCP and AWS is fairly straightforward, there are advantages both in terms of cost and integration by sticking with one. However, in some instances the use of services across cloud service providers is sensible. An instance like this may be the use of AWS personalise, a machine learning service offered by Amazon Web Services (AWS) that enables businesses to create personalized recommendations for their customers 

The data pipeline would be as follows:

<li>Data Sources (various e.g. Social Media, Google Analytics, Production Database)
<li>ETL (Data Integration): Fivetran
<li>Data Transformation: dbt Cloud
<li>Data Warehouse (Storage / Transformation): BigQuery
<li>Data Exploration/Dashboarding: Tableau 
<li>Communications: Customer.io
<li>Orchestration: dbt Cloud, Fivetran

<u>**Pipeline description and rationale**<u>
Data Collection**
For data collection and integration, depending on the balance of the sources needed vs the sources serviced through a tool, I would opt for an out of the box ETL tool such as Fivetran, a cloud-based data integration tool that provides pre-built connectors. The reason I'd opt for this is that it can save considerable time and money when compared to the salary of a data engineer and can allow for a leaner team and free up time for other value adding work such as driving insights through analysis. This is because Fivetran connectors are automatically maintained and updated, for example in the case of schema changes. It’s a best in class solution you’ll find in many early stage businesses, integrates seamlessly with GCP and can even be used via GCP start-up credits. It’s the solution I use in my current business and I’ve had an excellent experience with it. Fivetran automatically integrates the collected data into your Data Warehouse, in this case I would opt for BigQuery, more on this below. You could go for an entirely custom approach to ETL but I would argue the upkeep and resource allocation make it the lesser choice, unless you have a lot of custom requirements not serviced by pre-built connectors. 

Practicalities: Set up involves setting up connectors using service accounts or appropriate credentials and scheduling these according to your needs. 

Data Transformation
I would opt for dbt Cloud for data transformation. dbt (Data Build Tool) is an open-source tool that allows analysts to write SQL queries to transform data in a reproducible and maintainable way. dbt Cloud is the cloud-based version of dbt that provides additional features, such as scheduling and orchestration of dbt runs and additional features via the IDE. dbt cloud offers advantages in bringing software development principles and data governance into one place seamlessly, through the likes of version control, documentation and testing. It encourages best practice approaches to SQL through enabling a modular approach, and provides easy to access data lineage. It’s best in class and has been growing in popularity over the last few years. It’s free for one developer seat and very low cost from there on out. For all these reasons dbt Cloud would be what I would employ for data transformation. There is also dbt Core which is entirely command line based and completely free should costs become prohibitive or there be a desire for more control or customisation.

Practicalities: Set up involves layering on top of your data warehouse using a service account or appropriate credentials connected via the dbt cloud UI.

Data Storage
For storage I would opt for BigQuery. It offers a better pricing structure than Snowflake for earlier stage businesses and provides superior functionality to Redshift, particularly when it comes to maintenance due to its systems architecture. However, I think one of the most compelling reasons to choose BigQuery over the likes of Redshift would be free streaming of events from Google Analytics, reducing ingress and egress costs.

Practicalities: Set up is seamless with this being a GCP product with considerations needing to be made regarding governance, in terms of identity and access management (IAM), such as roles and permissions as well as service/data location e.g. eu-west-2. 

Data Exploration/Dashboarding;
When considering BI tools, the two options worth considering in my opinion are Looker and Tableau. Looker is superior in terms of enabling self service analytics due to its governance and modeling layers. However, Tableau offers superior flexibility. The biggest divide though is cost, with Looker being orders of magnitude more expensive, especially if opting for features such as white labeled embedded dashboards within your own site, such as for client or investor dashboards. For this reason I would choose Tableau. It can be used for both dashboarding and  data exploration/analysis. The results of the data analysis are presented to end-users through dashboards and customized to provide a user-friendly interface for exploring the data, including filters, parameters, drill downs, views and exports. I would opt for Tableau Cloud in the first instance as it provides a fully managed service, but you can opt for Tableau server if you have specific requirements. 

Practicalities: Set up involves connecting with BigQuery via service account or appropriate credentials connected via the Tableau Desktop UI.

Communications:
Comms are an important end point for an analytics pipeline as they allow insights to turn into actions that affect users. Through a platform like Customer.io you are able to send targeted, personalized messages to their customers based on their behavior and interests that are relevant and timely. Customer.io integrates seamlessly with BigQuery with the ability to write SQL against tables in the warehouse to enable various customer journeys. 

Practicalities: Set up involves connecting with BigQuery via service account or appropriate credentials connected via the customer.io UI.

Orchestration:
Orchestration can be handled through a mix of sequential triggered workflows and chronological time based scheduling. 
Using Fivetran, you can schedule your data sources to sync with your target data warehouse on a regular basis. This will ensure that your data is up-to-date for your dbt jobs. 
Within dbt Cloud you are able to then create sequential workflows, where a series of dbt jobs are triggered by the completion of the previous job. 
You are able to build a dashboard in Tableau or use dbt Cloud tests to monitor your workflows to ensure that they are running smoothly. If there are any errors, use the logging and error reporting features in Fivetran and dbt Cloud to troubleshoot the issue. 
There is the option to have a sequential workflow from the point of data integration from source though transformations through use Fivetran transformations (which run on dbt Core), however this would mean not using dbt Cloud and would arguably result in an over dependence on Fivetran, should a switch to another ETL option down the line be required. Given that for most regular reporting needs a near real time, or usually daily option, is more than enough, it is unlikely this is necessary. Other options such as Airflow are also available for orchestration. 


Advantages:
Scalability: BigQuery is a highly scalable data warehouse that can handle large volumes of data, making it well-suited for this use case.
Ease of use: Fivetran and dbt Cloud and BigQuery are all cloud-based options that are easy to set up and use. They provide a user-friendly interface for data integration, storage and transformation.
Data governance: dbt Cloud provides version control and testing capabilities, which are important for maintaining data governance and ensuring data accuracy. Fivetran handles schema and data changes for you ensuring data is always up to date and clean. 
Integration: All tools chosen integrate seamlessly with one another with easy steps for upkeep monitoring and maintenance. 
Visualization: Tableau provides a wide range of visualization options and is well-suited for creating user-friendly dashboards.

Overall, this stack provides a robust and scalable solution that ensures a seamless flow of data from source to dashboard.

Question 2
The Customer Support team spends considerable time scanning through customer reviews and comments in order to filter out illegitimate ones. Multiple factors can contribute to label comments as authentic or not:

Comment is made by a registered user vs. anonymous;
Level of user activity (eg: number of past reviews and comments);
Content of the comment (eg: unauthorized advertising)
...
In order to automate the filtering process, design a conceptual, real-time, decision support system that takes data as input (user properties, user actions, content, etc) and automatically labels comments as legitimate/illegitimate for the Customer Support Team to quickly flag and remove the unwanted.

Describe possible approaches and architecture, focusing more on algorithms, libraries and tools that could be used.

TLDR:
To automate comment filtering, build a machine learning model that classifies comments as legitimate/illegitimate based on user properties, actions, and content. Collect and preprocess data, engineer features, and choose a binary classification or regression model. Train, test, and deploy the model as a real-time decision support system, integrating it with the existing Customer Support system. Use Python, Scikit-learn, Pandas, NLTK, and Flask, and consider logistic regression or decision tree algorithms. In real-time deployment, the CRM system sends data to the model through an API, which preprocesses the data and returns a prediction label or score. The CRM system takes action based on the prediction and provides feedback to the model for retraining or fine-tuning. Microservices architecture with a message broker can achieve real-time deployment on GCP.

Detail:
To be transparent, to implement the below solution is outside my scope of expertise but I would confidently work with other technical stakeholders to design, develop and deploy such a system. 

To automate the filtering process, you could build a machine learning model that classifies comments as legitimate/illegitimate based on the available data. The approach would be as such:

Model Development:
Data collection: Gather data on user properties (e.g., registration status, activity level), user actions (e.g., past reviews and comments), and comment content (e.g., text, presence of unauthorized advertising).
Data preprocessing: Clean and preprocess the data to remove any irrelevant or redundant features, handle missing values, and normalize the data.
Feature engineering: Create new features based on the available data, such as user status, reputation score, presence of specific keywords or sentiment analysis. 
Model selection: Choose an appropriate machine learning model to classify comments as legitimate/illegitimate. The model can be a binary classification model such as logistic regression or a decision tree that predicts a binary label (legitimate/illegitimate) or a regression model that predicts a continuous score representing the comment's authenticity. A score would enable an additional layer of classification logic at the discretion of the stakeholders which could be desirable, while a binary option would leave this level of decision making down to the model. 
Training and testing: Split the data into training and testing sets, train the model on the training set, and evaluate its performance on the testing set. Use cross-validation to ensure the model's robustness. The training set would be a historical set where data was classified by humans. 
Deployment/Integration: Once the model is trained, deploy it as a real-time decision support system that takes user properties, user actions, and comment content as input and outputs a label of legitimate or illegitimate. Integrate the decision support system with the existing Customer Support system to provide automated labeling of comments.

Tools and libraries:
Language: Python is a good choice for this task as it has many libraries for machine learning and data preprocessing.
Scikit-learn: A popular machine learning library in Python that provides various classification models and tools for data preprocessing and feature engineering.
Pandas: A data manipulation library in Python that can handle data preprocessing tasks such as cleaning and normalization.
NLTK (Natural Language Toolkit): A library in Python for natural language processing, which can be used to preprocess the comment text data. This could also be achieved via a basic logic of certain words being flagged.

Algorithms:
Logistic regression: A simple and interpretable binary classification model that works well with high-dimensional data.
Decision tree: A tree-based model that can handle non-linear relationships between the features and the target variable.


Real-time Deployment:
Data input: The CRM system sends comment data to the machine learning model through an API with the relevant user properties (e.g., registration status, activity level), user actions (e.g., past reviews and comments), and comment content (e.g., text, presence of unauthorized advertising).
Data preprocessing: The machine learning model preprocesses the input data to clean and transform it into a format that can be used for model inference (feature engineering, data normalization, and data cleaning).
Model inference and prediction output: The machine learning model uses the preprocessed data to make a prediction on the legitimacy of the comment. The machine learning model returns the predicted label or score as a JSON response to the CRM system. 
Action triggering: Based on the predicted label or score, the CRM system can take action on the comment, such as flagging it for further review, removing it, or sending an alert to the Customer Support team. The action can be triggered automatically based on predefined logic.
Feedback loop: The CRM system can also provide feedback to the machine learning model on the accuracy and relevance of the predictions. This can be done by sending labeled data or user feedback to the model for retraining or fine-tuning. The feedback loop can help improve the model's performance over time and ensure its relevance to the business needs.
Real-time: My understanding is that real-time deployment could be achieved through microservices architecture with a message broker, such as Apache Kafka or RabbitMQ, deployed on Google Cloud Platform (GCP).
