---
layout: article
date: 2024-01-12 
modify_date: 2024-01-12 
title: "The problem with Elastic Search's dynamic field-mapping and it's solution!"
excerpt: "Let's dive into a real-world scenario where Elastic's dynamic mapping caused problems in data-view and how it was resolved"
tags: [Elastic Search, Kibana, Logstash, ELK, Data Views]
key: elastic-search-dynamic-mapping
---

> *At the heart of ELK stack is Elasticsearch, a distributed search and analytics engine. Then, we have Logstash which facilitate collecting, aggregating, and enriching our data and storing it in Elasticsearch. Finally, there is Kibana which enables us to interactively explore, visualize, and share insights into out data, manage and monitor the stack. Elasticsearch is where the indexing, search, and analysis magic happens..* 


## Problem Statement

Recently, I came across an issue(or feature?🤔) regarding Elasticsearch(ES) at my workplace. One of my colleagues has created a `Data View` in Kibana but there is a problem! 

A field in that view appears as a `Timestamp` field type but she wanted it to be a `Text` field.

For the remainder of this post, we'll refer to it as **Field-X**.

So, how did the field type change? The answer is --- it didn't change, it was always a `Date` or `Timestamp` type. To understand the flow and how the type of a field is determined by ES, I will briefly walk you through the steps involved from data ingestion to data-view creation in Kibana.

<u>This is how it goes: </u>

- Raw data is ingested through [Nifi](https://nifi.apache.org/documentation/v2/) to [HDFS](https://hadoop.apache.org/docs/r1.2.1/hdfs_design.html) and corresponding [Hive](https://hive.apache.org/) tables.
- Data is fetched from HDFS and is processed in Spark (perform some complex join queries).
- After processing, the final dataframe output is written to a CSV file on an Edge node.
- The CSVs are transferred to the Logstash server using sftp or by [mounting the directory](https://serverfault.com/questions/410588/how-to-mount-a-directory-from-another-server) to an ES node.
- A Logstash config file is created and the index name along with the conf file path is set in `pipelines.yml` file, &nbsp; &nbsp; &nbsp; the [conf file](https://raw.githubusercontent.com/is-this-echo/blog-img-hosting/main/images/insight_forge_data.conf) contains details like CSVs path & delimiter, logfile path, field names, Kibana credentials etc.
- Data collected in Logstash is then used by ES to visualize in Kibana based on the conf file.


**Important!**  All the stuff from here on has been tested on ES 8.6.x, at the time of writing this post the latest version of ES available is [8.11.14](https://www.elastic.co/guide/en/elasticsearch/reference/current/mapping.html) and the content explained here applies to both the tested version and the latest one.
{:.info}

***

## Dynamic Mapping - boon or a bane?

ES has a super cool feature - _dynamic field mapping_, straight from ES official site : 
> *To index a document, you don’t have to first create an index, define a mapping type, and define your fields — you can just index a document and the index, type, and fields will display automatically*


In our case, we didn't specify the index field mappings in Kibana beforehand, although later we modified the conf file to mutate **Field-X** to a string but our efforts were in vain as dynamic mapping has yet another trick up it's sleeve --  _**date detection**_ (enabled by default). Since the string value in **Field-X** passed the detection it was considered as a `Date` field nonetheless.

```json
mutate {
      convert =>{"FIELD-X" => "string"}
	  ...
   }
```

So, it turns out the source of our problem was relying only on Logstash config to create index, load data and render the views on Kibana. ES offers a lot more control via its APIs, read on to find out how we solved the issue.

***

## Explicit Mapping to the rescue!

As the name suggests, _explicit field mapping_ was introduced to overpower  _dynamic field mapping_, it allows us to specify our own explicit mappings for an index as we know more about our data than ES can guess.

Since our index has already been created, we couldn't change the mapping or field type of an existing field as it could invalidate loaded data in the view.

<u>Therefore, these are the steps we followed: </u>

- Create a new index with explicit field mapping.
- Copy data from old index to new index using ES **Reindex API**.
- Modify the Logstash conf file to change index name.

Lets go through the steps in detail in the next section.

***

## Implementing the solution



- Open terminal and type:
		
	```bash
	cd ~
	touch .bash_profile
	open -e .bash_profile
	```

<img src="https://github.com/Zhenye-Na/Zhenye-Na.github.io/blob/master/assets/images/posts-img/mysql-installation/mysql7.jpg?raw=true" class="pics" />

- Type this piece of codes in the file you opened, then save and quit.

	```
	export PATH=${PATH}:/usr/local/mysql/bin
	```
	
- Use this piece of code and the password appeared in notification center to log in.

	```bash
	mysql -u root -p
	```
- If you successfully log in using `Terminal`, you can use this piece of code to reset/change your password.
	
	```bash
	SET PASSWORD FOR 'root'@'localhost' = PASSWORD('new password');
	```

<img src="https://github.com/Zhenye-Na/Zhenye-Na.github.io/blob/master/assets/images/posts-img/mysql-installation/mysql8.jpg?raw=true" class="pics" />
	
- This is it! Now you have `MySQL` installed and secured on your Mac.

> *If you notice mistakes and errors in this post, don't hesitate to leave a comment and I would be super happy to correct them right away!*



<style>
img.pics {
    display: block;
    margin: 0 auto;
    width: 70%;
}
</style>