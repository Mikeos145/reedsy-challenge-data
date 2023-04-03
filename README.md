## **Question 0**

Write a paragraph about yourself, your hobbies and your major achievements in your career or study so far. Add another one about your professional experience and commercial projects you've been involved with.

## **Answer 0**

Hi, I’m Michael - I’m an outgoing, social person with a positive outlook on life. I enjoy physical activities, frequently involving myself in sports, outdoor pursuits and adventure based getaways. I love nature, hold the value of friends and family in high regard, and enjoy challenging myself mentally, always looking to expand my skill and knowledge base. My major achievements in my career and study so far include receiving a 1st Class Hons Degree, gaining a placement at IBM and then going on to start from the bottom on a Data Analyst Internship and working my way up through two promotions to managing the biggest account in the business (Amazon) within 9 months. 

Since then I’ve applied my skills across a broad range of settings, never resting on my laurels, but always looking to take on new challenges, self-teaching to meet those. In my last role this took the form of working on two academic papers with Imperial College London which are soon to be published as well as developing a publicly accessing respiratory data hub to democratise respiratory data for campaigners and patients alike. In my current role, I came in to a business with no analytics tech stack and a scattered, error prone “system” of manual reporting. Within 10 months, I provided stop gap solution for automated reporting, while scoping, designing and implementing a full, best in class, analytics tech stack, to set the business up for scale. This includes ETL, Data Warehousing, Reverse ETL and BI Tool (Tableau) with a full suite of dashboards to serve 4 distinct areas of the business. These are Engagement and Programmes, Commercial, Product and Leadership.

## **Question 1**

The Marketing Team at Bookly wants to merge and analyze all the data that is being collected by the different products in order to extract useful business insights of various kinds. Examples of such analytics include (but are not restricted to):

<li>List all-time top rated books and trending ones;
<li>Measure user sign-up rate over certain periods (weekly, quarterly, etc);
<li>Show the total number of real-time (current) page views for any given book description page (product page);
<li>...

Design a conceptual data pipeline to drive and aggregate data from all the different sources to ultimately be accessible by a user-friendly data exploration/dashboarding tool of your choice. Feel free to pick any technology available (e.g. open source, cloud providers, etc.).

Describe the different components of the architecture, tools involved and compare possible approaches.

## **Answer 1**

### **TL;DR**
This is a data pipeline that covers data collection and integration, data transformation, data storage, data exploration/dashboarding, communications, and orchestration. The principles it follows are scalability, ease of use, maintenance, governance, and collaboration. The recommended stack is a GCP first stack, and while combining services from other providers is possible, there are advantages in sticking to one service provider where possible. The data pipeline starts with various data sources, and an ETL tool like Fivetran is recommended for data collection and integration. For data transformation, dbt Cloud is used, and for storage, BigQuery is recommended. Tableau is used for data exploration/dashboarding, and for communications, Customer.io is used. dbt Cloud and Fivetran are used for orchestration. 

### **Detail**
_The below data pipeline will cover the following areas:_

<li>Data Collection & Integration
<li>Data Transformation
<li>Data Storage
<li>Data Exploration/Dashboarding
<li>Communications
<li>Orchestration 

_It has been suggested based on the following principles:_

<li>Scalability
<li>Ease of use
<li>Maintenance
<li>Governance 
<li>Collaboration

I have chosen a GCP analytics tech stack and while combining services across the likes of GCP and AWS is fairly straightforward, there are advantages both in terms of cost and integration by sticking with one. However, in some instances the use of services across cloud service providers is sensible. An instance like this may be the use of AWS personalise, a machine learning service offered by Amazon Web Services (AWS) that enables businesses to create personalized recommendations for their customers 

_The data pipeline would be as follows:_

<li>Data Sources (various e.g. Social Media, Google Analytics, Production Database)
<li>ETL (Data Integration): Fivetran
<li>Data Transformation: dbt Cloud
<li>Data Warehouse (Storage / Transformation): BigQuery
<li>Data Exploration/Dashboarding: Tableau 
<li>Communications: Customer.io
<li>Orchestration: dbt Cloud, Fivetran

#### **Pipeline description and rationale**
_**Data Collection**_
<br>For data collection and integration, depending on the balance of the sources needed vs the sources serviced through a tool, I would opt for an out of the box ETL tool such as Fivetran, a cloud-based data integration tool that provides pre-built connectors. The reason I'd opt for this is that it can save considerable time and money when compared to the salary of a data engineer and can allow for a leaner team and free up time for other value adding work such as driving insights through analysis. This is because Fivetran connectors are automatically maintained and updated, for example in the case of schema changes. It’s a best in class solution you’ll find in many early stage businesses, integrates seamlessly with GCP and can even be used via GCP start-up credits. It’s the solution I use in my current business and I’ve had an excellent experience with it. Fivetran automatically integrates the collected data into your Data Warehouse, in this case I would opt for BigQuery, more on this below. You could go for an entirely custom approach to ETL but I would argue the upkeep and resource allocation make it the lesser choice, unless you have a lot of custom requirements not serviced by pre-built connectors. 

_**Practicalities**:_ Set up involves setting up connectors using service accounts or appropriate credentials and scheduling these according to your needs. 

_**Data Transformation**_
<br>I would opt for dbt Cloud for data transformation. dbt (Data Build Tool) is an open-source tool that allows analysts to write SQL queries to transform data in a reproducible and maintainable way. dbt Cloud is the cloud-based version of dbt that provides additional features, such as scheduling and orchestration of dbt runs and additional features via the IDE. dbt cloud offers advantages in bringing software development principles and data governance into one place seamlessly, through the likes of version control, documentation and testing. It encourages best practice approaches to SQL through enabling a modular approach, and provides easy to access data lineage. It’s best in class and has been growing in popularity over the last few years. It’s free for one developer seat and very low cost from there on out. For all these reasons dbt Cloud would be what I would employ for data transformation. There is also dbt Core which is entirely command line based and completely free should costs become prohibitive or there be a desire for more control or customisation.

_**Practicalities**:_ Set up involves layering on top of your data warehouse using a service account or appropriate credentials connected via the dbt cloud UI.

_**Data Storage**_
<br>For storage I would opt for BigQuery. It offers a better pricing structure than Snowflake for earlier stage businesses and provides superior functionality to Redshift, particularly when it comes to maintenance due to its systems architecture. However, I think one of the most compelling reasons to choose BigQuery over the likes of Redshift would be free streaming of events from Google Analytics, reducing ingress and egress costs.

_**Practicalities**_: Set up is seamless with this being a GCP product with considerations needing to be made regarding governance, in terms of identity and access management (IAM), such as roles and permissions as well as service/data location e.g. eu-west-2. 

_**Data Exploration/Dashboarding**_
<br>When considering BI tools, the two options worth considering in my opinion are Looker and Tableau. Looker is superior in terms of enabling self service analytics due to its governance and modeling layers. However, Tableau offers superior flexibility. The biggest divide though is cost, with Looker being orders of magnitude more expensive, especially if opting for features such as white labeled embedded dashboards within your own site, such as for client or investor dashboards. For this reason I would choose Tableau. It can be used for both dashboarding and  data exploration/analysis. The results of the data analysis are presented to end-users through dashboards and customized to provide a user-friendly interface for exploring the data, including filters, parameters, drill downs, views and exports. I would opt for Tableau Cloud in the first instance as it provides a fully managed service, but you can opt for Tableau server if you have specific requirements. 

_**Practicalities**_: Set up involves connecting with BigQuery via service account or appropriate credentials connected via the Tableau Desktop UI.

_**Communications**_
<br>Comms are an important end point for an analytics pipeline as they allow insights to turn into actions that affect users. Through a platform like Customer.io you are able to send targeted, personalized messages to their customers based on their behavior and interests that are relevant and timely. Customer.io integrates seamlessly with BigQuery with the ability to write SQL against tables in the warehouse to enable various customer journeys. 

_**Practicalities**_: Set up involves connecting with BigQuery via service account or appropriate credentials connected via the customer.io UI.

_**Orchestration**_
<br>Orchestration can be handled through a mix of sequential triggered workflows and chronological time based scheduling. 
<br>Using Fivetran, you can schedule your data sources to sync with your target data warehouse on a regular basis. This will ensure that your data is up-to-date for your dbt jobs. 
<br>Within dbt Cloud you are able to then create sequential workflows, where a series of dbt jobs are triggered by the completion of the previous job. 
<br>You are able to build a dashboard in Tableau or use dbt Cloud tests to monitor your workflows to ensure that they are running smoothly. If there are any errors, use the logging and error reporting features in Fivetran and dbt Cloud to troubleshoot the issue. 
<br>There is the option to have a sequential workflow from the point of data integration from source though transformations through use Fivetran transformations (which run on dbt Core), however this would mean not using dbt Cloud and would arguably result in an over dependence on Fivetran, should a switch to another ETL option down the line be required. Given that for most regular reporting needs a near real time, or usually daily option, is more than enough, it is unlikely this is necessary. Other options such as Airflow are also available for orchestration. 


_**Advantages**_
<br>**Scalability**: BigQuery is a highly scalable data warehouse that can handle large volumes of data, making it well-suited for this use case.
<br>**Ease of use**: Fivetran and dbt Cloud and BigQuery are all cloud-based options that are easy to set up and use. They provide a user-friendly interface for data integration, storage and transformation.
<br>**Data governance**: dbt Cloud provides version control and testing capabilities, which are important for maintaining data governance and ensuring data accuracy. Fivetran handles schema and data changes for you ensuring data is always up to date and clean. 
<br>**Integration**: All tools chosen integrate seamlessly with one another with easy steps for upkeep monitoring and maintenance. 
<br>**Visualization**: Tableau provides a wide range of visualization options and is well-suited for creating user-friendly dashboards.

Overall, this stack provides a robust and scalable solution that ensures a seamless flow of data from source to dashboard.

## **Question 2**
 
The Customer Support team spends considerable time scanning through customer reviews and comments in order to filter out illegitimate ones. Multiple factors can contribute to label comments as authentic or not

<li>Comment is made by a registered user vs. anonymous;
<li>Level of user activity (eg: number of past reviews and comments);
<li>Content of the comment (eg: unauthorized advertising)
<li>...
 
In order to automate the filtering process, design a conceptual, real-time, decision support system that takes data as input (user properties, user actions, content, etc) and automatically labels comments as legitimate/illegitimate for the Customer Support Team to quickly flag and remove the unwanted.

Describe possible approaches and architecture, focusing more on algorithms, libraries and tools that could be used.

## **Answer 2**

### **TLDR:**
To automate comment filtering, build a machine learning model that classifies comments as legitimate/illegitimate based on user properties, actions, and content. Collect and preprocess data, engineer features, and choose a binary classification or regression model. Train, test, and deploy the model as a real-time decision support system, integrating it with the existing Customer Support system. Use Python, Scikit-learn, Pandas, NLTK, and Flask, and consider logistic regression or decision tree algorithms. In real-time deployment, the CRM system sends data to the model through an API, which preprocesses the data and returns a prediction label or score. The CRM system takes action based on the prediction and provides feedback to the model for retraining or fine-tuning. Microservices architecture with a message broker can achieve real-time deployment on GCP.

### **Detail:**
To be transparent, to implement the below solution is outside my scope of expertise but I would confidently work with other technical stakeholders to design, develop and deploy such a system. 

To automate the filtering process, you could build a machine learning model that classifies comments as legitimate/illegitimate based on the available data. The approach would be as such:

#### **Model Development:**
<br>_**Data collection**_: Gather data on user properties (e.g., registration status, activity level), user actions (e.g., past reviews and comments), and comment content (e.g., text, presence of unauthorized advertising).
<br>_**Data preprocessing**_: Clean and preprocess the data to remove any irrelevant or redundant features, handle missing values, and normalize the data.
<br>_**Feature engineering**_: Create new features based on the available data, such as user status, reputation score, presence of specific keywords or sentiment analysis. 
<br>_**Model selection**_: Choose an appropriate machine learning model to classify comments as legitimate/illegitimate. The model can be a binary classification model such as logistic regression or a decision tree that predicts a binary label (legitimate/illegitimate) or a regression model that predicts a continuous score representing the comment's authenticity. A score would enable an additional layer of classification logic at the discretion of the stakeholders which could be desirable, while a binary option would leave this level of decision making down to the model. 
<br>_**Training and testing**_: Split the data into training and testing sets, train the model on the training set, and evaluate its performance on the testing set. Use cross-validation to ensure the model's robustness. The training set would be a historical set where data was classified by humans. 
<br>_**Deployment/Integration**_: Once the model is trained, deploy it as a real-time decision support system that takes user properties, user actions, and comment content as input and outputs a label of legitimate or illegitimate. Integrate the decision support system with the existing Customer Support system to provide automated labeling of comments.

#### **Tools and libraries**:
<br>_**Language**_: Python is a good choice for this task as it has many libraries for machine learning and data preprocessing.
<br>_**Scikit-learn**_: A popular machine learning library in Python that provides various classification models and tools for data preprocessing and feature engineering.
<br>_**Pandas**_: A data manipulation library in Python that can handle data preprocessing tasks such as cleaning and normalization.
<br>_**NLTK (Natural Language Toolkit)**_: A library in Python for natural language processing, which can be used to preprocess the comment text data. This could also be achieved via a basic logic of certain words being flagged.

#### **Algorithms**:
<br>_**Logistic regression**_: A simple and interpretable binary classification model that works well with high-dimensional data.
<br>_**Decision tree**_: A tree-based model that can handle non-linear relationships between the features and the target variable.


#### **Real-time Deployment:**
<br>_**Data input**_: The CRM system sends comment data to the machine learning model through an API with the relevant user properties (e.g., registration status, activity level), user actions (e.g., past reviews and comments), and comment content (e.g., text, presence of unauthorized advertising).
<br>_**Data preprocessing**_: The machine learning model preprocesses the input data to clean and transform it into a format that can be used for model inference (feature engineering, data normalization, and data cleaning).
<br>_**Model inference and prediction output**_: The machine learning model uses the preprocessed data to make a prediction on the legitimacy of the comment. The machine learning model returns the predicted label or score as a JSON response to the CRM system. 
<br>_**Action triggering**_: Based on the predicted label or score, the CRM system can take action on the comment, such as flagging it for further review, removing it, or sending an alert to the Customer Support team. The action can be triggered automatically based on predefined logic.
<br>_**Feedback loop**_: The CRM system can also provide feedback to the machine learning model on the accuracy and relevance of the predictions. This can be done by sending labeled data or user feedback to the model for retraining or fine-tuning. The feedback loop can help improve the model's performance over time and ensure its relevance to the business needs.
<br>_**Real-time**_: My understanding is that real-time deployment could be achieved through microservices architecture with a message broker, such as Apache Kafka or RabbitMQ, deployed on Google Cloud Platform (GCP).

## **Part B**
 
The marketing Team at Bookly introduced A/B Testing on their blog - each blog post displays a registration popup picked up from a collection of pre-configured popups. Popups can differ in certain properties such as title, description and picture.

The raw dataset in dataset.tsv offers a table with each combination of blog post and registration popup, their corresponding properties and statistics like the total number of page views and registrations. Bookly's main goal is to convert page views into registrations.

Other considerations:
<li>each A/B experiment has a start date;
<li>rows with empty popup_version values are not running A/B experiments.

## **Question 3**
 
For each A/B experiment, find the most performant popup version (A or B) and show the corresponding conversion rate.

Describe in detail all the steps you take to perform the analysis, provide code snippets, relevant data transformations and results.

## **Answer 3**

### **Steps taken**
Initially it’s important to eyeball the data getting a sense of what each column contains and initial thoughts on any cleaning steps. For this a simple SELECT * query will suffice:

```
-- TAKE A LOOK AT THE DATA
SELECT * FROM `oceanic-hash-382522.reedsy.reedsy_AB` LIMIT 1000;
```

From here it’s clear that data will need to be extracted from an array of terms within the popup_version_start_date_popup_category field. So through the use of SAFE_CAST, REPLACE, SPLIT, OFFSET, terms can be extracted. Checking for any null or empty results. In this case there were some for A/B which was expected but also some for date, which outlines data quality issues for a small portion of total views ~2%. Through the use of order by, null results can be identified.

```
-- TAKE A LOOK AT POPUP NAMES TO SEE HOW TO EXTRACT DATA FROM THESE
SELECT DISTINCT
popup_version_start_date_popup_category,
SAFE_CAST(REPLACE(SPLIT(popup_version_start_date_popup_category, ",")[OFFSET(1)],'"',"") AS DATE) AS date,
REPLACE(REPLACE(SPLIT(popup_version_start_date_popup_category, ",")[OFFSET(0)],'"',""),"[","") as AB,
REPLACE(REPLACE(SPLIT(popup_version_start_date_popup_category, ",")[OFFSET(2)],'"',""),"]","") as category
FROM `oceanic-hash-382522.reedsy.reedsy_AB`
ORDER BY 2 ASC
LIMIT 1000;
```

It wasn’t entirely clear from the brief what the unifying field would be across the A/B tests so a look at the data filtered by blog post url sheds light on what varies across the blog post, revealing the A/B split across blog post and date, as per details in the brief. However the blog post field needs to be cleaned to ensure correct groupings, due to excess backslashes at the end of URLs.

```
-- FURTHER LOOK AT BLOG POST GROUPINGS TO SEE WHAT VARIES BY BLOG POST
SELECT * FROM `oceanic-hash-382522.reedsy.reedsy_AB` 
ORDER BY REPLACE(blog_post_url,"/","")
```

At this point a first iteration of the final table seems appropriate, using a campaign_id of a CONTENATED field of blog post and the extracted date as the unique identifier for the A/B tests. A common table expression (CTE) serves as a suitable option to create a staging table to keep the code from becoming too bulky or repetitive with the lengthy functions needed to extract items from the popup_version. It was clear from the data interrogation that there were multiple rows that needed to be aggregated per campaign id. These were generally due to multiple languages of the same text creating distinct rows. This is something I would discuss with relevant stakeholders as this may be something to deliberately keep distinct if there’s a rationale that different regions should be segmented due to confounding factors but in this instance I opted to aggregate the views and registrations and create a conversation rate based on registrations/views. This allowed for the creation of a most_performant flag using a window function based on the conversion rates (CVR), as well as a data sanity flag to check if there were both an A and a B present for a given campaign, also using a window function. There were instances where there was only either A or B. Further investigation on this by ordering on this field revealed that in these instances, the solo A or B line item had low views and therefore it is assumed that its counterpart is simply missing due to no views - making the present line item the most performant. To validate this, a check to ensure that there are no 0 view line items reveals that this is indeed the case. As there are no placeholder or 0 value rows the assumption seems reasonable. However this is something that could easily be checked with other stakeholders or through a better understanding of the data source.

```
-- PRODUCE FINAL TABLE AFTER SOME INTERATIONS WITH FLAGS FOR MOST PERFORMANT
WITH `cte_a_b_popup_staging` AS (
 SELECT
 REPLACE(blog_post_url,"/","") AS blog_url_fixed,
 SAFE_CAST(REPLACE(SPLIT(popup_version_start_date_popup_category, ",")[OFFSET(1)],'"',"") AS DATE) AS start_date,
CONCAT(REPLACE(blog_post_url,"/",""),REPLACE(SPLIT(popup_version_start_date_popup_category, ",")[OFFSET(1)],'"',"")) AS campaign_id,
 REPLACE(REPLACE(SPLIT(popup_version_start_date_popup_category, ",")[OFFSET(0)],'"',""),"[","") as AB,
 REPLACE(REPLACE(SPLIT(popup_version_start_date_popup_category, ",")[OFFSET(2)],'"',""),"]","") as category,
 popup_name,
 SUM(registrations) AS sum_registrations,
 SUM(views) AS sum_views,
 ROUND(SUM(registrations)/SUM(views),2) AS CVR
 FROM `oceanic-hash-382522.reedsy.reedsy_AB`
 GROUP BY 1,2,3,4,5,6
 ORDER BY 1,2,3,4,5,6
)

SELECT
campaign_id,
blog_url_fixed,
start_date,
AB,
category,
popup_name,
sum_registrations,
sum_views,
CVR,
COUNT(*) OVER (PARTITION BY campaign_id) AS A_B_present_flag,
ROW_NUMBER() OVER (PARTITION BY campaign_id ORDER BY CVR DESC) AS most_performant_flag
FROM `cte_a_b_popup_staging`
WHERE LENGTH(AB) > 0
ORDER BY start_date DESC, campaign_id, CVR DESC
```

Here is the code to confirm there are no 0 value rows. 
```
-- DOUBLE CHECK IF THERE ARE ROWS OF DATA WITH 0 VIEWS
SELECT * FROM `oceanic-hash-382522.reedsy.reedsy_AB` WHERE VIEWS = 0
```
 
## **Question 4**
 
**For each start date, compute the total views, registrations and conversion for that date. Present the results in the following formats**:

<li>**a table where we can see the views, registrations and conversion value per start date;
<li>**a chart where we can see the evolution of conversion over time (views and registrations not necessary here).**

**As before, provide code snippets and relevant data transformations.**

## **Answer 4** 
 
### **Steps taken**
For this a simple adaptation of the final table above can be made to achieve a date level aggregation. 

```
-- START DATE OVER TIME
WITH `cte_a_b_popup_staging` AS (
 SELECT
 SAFE_CAST(REPLACE(SPLIT(popup_version_start_date_popup_category, ",")[OFFSET(1)],'"',"") AS DATE) AS start_date,
 SUM(registrations) AS total_registrations,
 SUM(views) AS total_views,
 ROUND(SUM(registrations)/SUM(views),2) AS total_CVR
 FROM `oceanic-hash-382522.reedsy.reedsy_AB`
 GROUP BY 1
 ORDER BY 1 DESC
)


     SELECT
     start_date,
     total_registrations,
     total_views,
     total_CVR,
     FROM `cte_a_b_popup_staging`
     ORDER BY start_date DESC
```

I also explored adding a date scaffold to fill in blank dates out of interest on the assumption that if popups were constantly running and missing days were due to no hits, using a date scaffold could provide a clearer picture of regularity. 

```
-- START DATE OVER TIME WITH DATE SCAFFOLD
WITH `cte_a_b_popup_staging` AS (
 SELECT
 SAFE_CAST(REPLACE(SPLIT(popup_version_start_date_popup_category, ",")[OFFSET(1)],'"',"") AS DATE) AS start_date,
 SUM(registrations) AS total_registrations,
 SUM(views) AS total_views,
 ROUND(SUM(registrations)/SUM(views),2) AS total_CVR
 FROM `oceanic-hash-382522.reedsy.reedsy_AB`
 GROUP BY 1
 ORDER BY 1 DESC
),


 `cte_date_scaffold` AS (
   SELECT date_date_scaffold FROM
   UNNEST(GENERATE_DATE_ARRAY(
   (SELECT MIN(SAFE_CAST(REPLACE(SPLIT(popup_version_start_date_popup_category, ",")[OFFSET(1)],'"',"") AS DATE)) FROM `oceanic-hash-382522.reedsy.reedsy_AB`)
   ,
   (SELECT MAX(SAFE_CAST(REPLACE(SPLIT(popup_version_start_date_popup_category, ",")[OFFSET(1)],'"',"") AS DATE)) FROM `oceanic-hash-382522.reedsy.reedsy_AB`)
   ,
   INTERVAL 1 DAY)) as date_date_scaffold)


     SELECT
     date_date_scaffold,
     start_date,
     total_registrations,
     total_views,
     total_CVR,
     FROM `cte_a_b_popup_staging`
     FULL JOIN `cte_date_scaffold`
       ON start_date = date_date_scaffold
     ORDER BY date_date_scaffold DESC
```

Once the tables were made I pulled these into google sheets to interrogate further. Ultimately I produced a simple line chart to meet the request. From this it can be seen that CVR has remained relatively flat across the period on average, although with significant variance and with the max CVR on one of the later dates. Popups are gaining traffic more often in later dates, possibly a feature of running more often, or if not then it is interesting as to why they are getting a higher frequency of engagement, but with lower CVR. This may be expected due to user fatigue. Before going further with this analysis I would ask the following questions:

<li>Have these popups ran constantly, if not what has the approach been?
<li>What is the ultimate ambition, efficiency or overall registrations? Are we looking for high CVR with as low impact as possible to not fatigue end users but still drive registrations, or are we willing to go with a high frequency approach which delivers more overall registrations at a lower CVR - which is the current state of affairs - but may cause user fatigue.

_**Considerations:**_
<li>There is also a risk in comparing episodes of high frequency with episodes of low frequency as frequency has a bearing on the validity of the data.
