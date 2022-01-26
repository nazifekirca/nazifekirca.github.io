--- 
layout: post 
title: Database Design 
subtitle: Notes from Datacamp Course 
categories: Databases 
tags: [Database Design, Intro]
---

The content is mainly taken from (Database Design) by Lis Sulmont 

## Understand the requirements

### Questions worth asking

- **Schemas**: How should my data be logically organized?
- **Normalization**: Should my data have minimal dependency and redundancy?  
- **Views**: What joins will be done most often?
- **Access control**: Should all users of the data have the same level of access?
- **DBMS**: How do I pick between all the SQL and noSQL options?

### OLTP or OLAP?

- `OLTP` stands for ***Online Transaction Processing***
    - Find the price of a book
    - Update latest customer transaction
    - Keep track of employee hours

- `OLAP` stands for ***Online Analytical Processing***
    - Calculate books with best profit margin
    - Find most loyal customers
    - Determine employee of the month

|   | OLTP | OLAP |
|---|---|---|
|**Purpose**|support daily transactions|report and analyze data|
|**Design**|application-oriented|subject-oriented|
|**Data**|up-to-date, operational|consolidated, historical|
|**Size**|snapshot, gigabytes|archive, terabytes|
|**Queries**|simple transaction and frequent updates|comples, aggregate queries & limited updates|
|**Users**|thousands|hundreds|

<hr>

![OLAP_VS_OLTP](/assets/images/post_images/database_design/OLAP_VS_OLTP.png)*[Database Design](https://campus.datacamp.com/courses/database-design) by Lis Sulmont*




<hr>

### Summary

Aks yourself: Is my project *OLAP*, *OLTP* or *something else*? 

## Storing Data

### Structured vs. unstructured

| Structured data | Unstructured data | Semi-structured data |
|---|---|---|
| Follows a schema | Schemaless | Does not follow larger schema |
| Defined data types and relationships | Makes up most of data in the world | self-describing structure |
| SQL, tables in a relational database | photos, chat logs, MP3 |NoSQL, XML, JSON |

### Beyond traditional databases

| Traditional databases | Data warehouses | Data lakes |
|---|---|---|
|for storing real-time relational structured data | for analyzing archived structured data | for storing data of all structures (flexibility and scalability)|
|**OLTP**|**OLAP**|**Big data**|

#### Data warehouses

![Data Warehouse Image](/assets/images/post_images/database_design/Data_Warehouse_Image.png)*[Database Design](https://campus.datacamp.com/courses/database-design) by Lis Sulmont*


##### Overview

- optimized for analytics - **OLAP**
    - organized for reading/aggregating data
    - usually read-only
- contains data from multiple sources
- massively parallel processing (MPP)
- typically uses a denormalized schema and dimensional modeling
- *Data marts* are subsets of data warehouses dedicated to specific topics

##### Practice

- Deploy [a data warehouse on AWS](https://aws.amazon.com/getting-started/hands-on/deploy-data-warehouse/)
- Deploy [a data warehouse on Azure](https://www.sqlshack.com/the-new-sql-data-warehouse-in-azure/)
- Deploy [a data warehouse on Google](https://cloud.google.com/bigquery)

#### Data lakes

- Store all types of data at a lower cost
    - e.g., raw, operational databases, IoT device logs, real.time, relational and non-relational
- Retains all data and can take up petabytes
- Schema-on-read as opposed to schema-on-write
- Need to catalog data otherwise becomes a **data swamp**
- Run **big data analytics** using services such as **Apache Spark** and **Hadoop**
    Useful for deeplearning and data discovery because activities require so much data

### Data flows

#### ETL

ETL stands for `Extract Transform Load`

![ETL scheme](/assets/images/post_images/database_design/ETL_scheme_1.png)*[Database Design](https://campus.datacamp.com/courses/database-design) by Lis Sulmont*


ELT stands for `Extract Load Transform`

![ELT scheme](/assets/images/post_images/database_design/ELT_scheme_1.png)*[Database Design](https://campus.datacamp.com/courses/database-design) by Lis Sulmont*


### What is database design?

- Determines how data is logically stored
    - How is data to be read and updated?
- Uses **database models**: high-level specifications for database structure
    - Most popular: relational model
    - Some other options: NpSQL models, object-oriented model, network model
- Uses **schemas**: blueprint of the database
    - Defines tables, fields, relationships, indexes, and views
    - When inserting data in relational datbases, schemas must be respected

### Data modeling

#### Conceptual ER diagram

Entities, Relationships, and Attributes

![ER diagram](/assets/images/post_images/database_design/ER_diagram.png)

*[Database Design](https://campus.datacamp.com/courses/database-design) by Lis Sulmont*

