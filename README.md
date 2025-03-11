# Overview
In this project we focus mainly on how to manage, streamline, and perform analysis on structured and semi-structured youtube videos data based on video category and the trending metrics

# Project Goals
Data Ingestion: We need to build a proper mechanism to ingest data from various sources.
ETL System: We always get the data in raw format, so we must transform this data into usable format by using required transformations.
Data lake: We get data from different sources so we need to have a centralized repo to store them.
Scalability: You never know when we are going to get huge volumes of data, so we need to make sure that our system is able to cope up with that sudden change.
Cloud: When we have vast data it is always better to go with cloud because it is easy to use and scalable. Here we are using AWS cloud environment.
Reporting: Build a dashboard to better understand the insights.
# Services that we are using for this project
Amazon S3: Amazon S3 is an object storage service that provides manufacturing scalability, data availability, security, and performance.
AWS IAM: This is nothing but identity and access management which enables us to manage access to AWS services and resources securely.
QuickSight: Amazon QuickSight is a scalable, serverless, embeddable, machine learning-powered business intelligence (BI) service built for the cloud.
AWS Glue: A serverless data integration service that makes it easy to discover, prepare, and combine data for analytics, machine learning, and application development.
AWS Lambda: Lambda is a computing service that allows programmers to run code without creating or managing servers.
AWS Athena: Athena is an interactive query service for S3 in which there is no need to load data it stays in S3.
# Dataset Used
This Kaggle dataset contains statistics (CSV files) on daily popular YouTube videos over several months. There are up to 200 trending videos published every day to many locations all over the world. The data for each region is in its own file. The video title, channel title, publication time, tags, views, likes and dislikes, description, and comment count are among the items included in the data. A category_id field, which differs by area, is also included in the JSON file linked to the region

Link: https://www.kaggle.com/datasets/datasnaek/youtube-new
# Architecture used
![image](https://github.com/user-attachments/assets/f221ce46-e015-42db-aee0-a7d3029ff768)

# High level project Flow
Kaggle Dataset --> Landing Area --> Glue job and Lambda function --> enriched/cleansed --> ETL pipeline --> Analytics/Reporting --> Quicksight Dashboard.
# Detailed Project Flow
Ingest all the data from kaggle data set to an S3 bucket (You can use CLI or direct upload)
Now build tables by crawling all the data and build a Glue Catalog for ETL.
Go to AWS Lambda to preprocess the data to handle json data to convert into tables (I provided the scripts required) and put in in clean bucket.
Again we need to build another crawler on the cleansed data. Now lets go to AWS Athena (Ad hoc query tool) and query our cleaned/enriched data.
Its finally time to build an ETL pipeline on our enriched/cleansed data to make it available for analytics purpose. For this process we use AWS Glue Studio and select the source as Cleaned data and Raw data from glue catalog and join them on category ID. Then store the destination data in new AWS S3 bucket and call it analytics bucket.
ETL_Pipeline

![image](https://github.com/user-attachments/assets/3b84f5a2-fe09-45d3-b16e-e66370d4908d)


Lets Do some Visualization using AWS Quicksight and select all the buckets we previously created. We need to visualize on the analytics bucket data and build the dashboard according our requirement.
You need to have good knowledge on AWS services and be able to build required IAM roles and permissions on the fly when required.
