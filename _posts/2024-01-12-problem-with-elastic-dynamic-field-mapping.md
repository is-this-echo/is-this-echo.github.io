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

Recently, I came across an issue(or feature?🤔)

Mac OS X doesn't ship with its own copy of `MySQL`, nor does `Sequel Pro`. You will have to install a copy on your local machine, or connect to the MySQL server on a machine somewhere on the Internet.

Most webservers and website packages will include a MySQL installation as part of the services they provide, and usually provide external connection details to allow you to connect to them in an external program like Sequel Pro. (See [Web Hosting Providers](https://sequelpro.com/docs/Web_Hosting_Providers) for a list of hosting options).

**Important!** IncoPOS for macOS can now download, install and configure MySQL server for you when it is started for the first time. You can download it from [here](https://vladster.net/en/downloads/).
{:.info}

## Download MySQL

The first step is to download `MySQL` server on your Mac. 

Go to the [MySQL web site](https://dev.mysql.com/downloads/mysql/) and select the version that matches your version of Mac OS. Select the `DMG archive` version which I recommend. Open the installer and follow the installation steps.

**Warning!** Because Oracle has changed the MySQL installer and the default parameters of the MySQL server in newer versions the following steps may no longer work. These steps were tested with MySQL server version 5.7.18 for macos10.12 in 2017 and I hoped this still worked fine with latest version. If not, feel free to leave a comment and I will update this post ASAP.
{:.warning}


```bash
$ mysql --version
mysql  Ver 14.14 Distrib 5.7.18, for macos10.12 (x86_64) using  EditLine wrapper
```


Please download and install version 5.5.48 to make sure that all the steps will work correctly. If for some reason the installer is no longer available on the MySQL web site you can download it from here.

<img src="https://github.com/Zhenye-Na/Zhenye-Na.github.io/blob/master/assets/images/posts-img/mysql-installation/mysql1.png?raw=true" class="pics" />
<br>
<img src="https://github.com/Zhenye-Na/Zhenye-Na.github.io/blob/master/assets/images/posts-img/mysql-installation/mysql2.png?raw=true" class="pics" />
<br>
<img src="https://github.com/Zhenye-Na/Zhenye-Na.github.io/blob/master/assets/images/posts-img/mysql-installation/mysql3.png?raw=true" class="pics" />
<br><br>
Pay attention to the password in notification center. If you do not save the proper `password` for `admin`, open notification center and scroll a little bit, you will find something like this:

<img src="https://github.com/Zhenye-Na/Zhenye-Na.github.io/blob/master/assets/images/posts-img/mysql-installation/mysql4.jpg?raw=true" class="pics" /> 


## MySQL Configuration

- Choose Apple () menu > System Preferences > MySQL, select MySQL and start MySQL server and move to the next step. If you use MySQL frequently, make sure to leave the checkbox **“Automatically Start MySQL Server on Startup”** so you won’t have to do that again and again.

<img src="https://github.com/Zhenye-Na/Zhenye-Na.github.io/blob/master/assets/images/posts-img/mysql-installation/mysql6.png?raw=true" class="pics" />


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