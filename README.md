## ELK

ELK setup for Virtual Machine while using Microsoft Azure Cloud. We will set up ElasticSearch, Logstash and kibana on master server. Filebeat will be there to fetch the logs from client server. Curator will be there to delete the older logs. elast-alert to raise the alert for matching pattern and keywords. We will also configure kibana dashboard.

We will be doing it in different repositories and setup for our VM. 

First of all we will configure dependencies before setting up Elasticsearch. Dependencies include openjdk and nginx. 

***Note: All Text written in italic should be executed in linux command line.*

**java version -**

The ELK stack requires Java 8 to be installed. Check the java version first, if it indicates java is installed then ok.  

*java -version*

Otherwise install java 8 using below commands

*sudo apt-get install openjdk-8-jdk*

If prompted, type y and hit the Enter for process to finish. 

**nginx -**

Nginx works as a web server and proxy server. it's used to configure pasword-controlled access to the kibana dashbaord. 

Install Nginx by entering: 

*sudo apt-get install nginx*

## Now we will start configuration for Elastic search

** Before going for ELK setup, one thing need to keep in mind that we install all packages of Elastic search, kibana, logstash and filebeat. after checking their compatablity through given link https://www.elastic.co/support/matrix **

We will add ** Elastic Repository **

it enable us to have the access to ELK stack. 

* We will import PGP key and install apt-transport-https package. then we will add elastic repository to our system repository list: Run the following commands one by one: 
```
1. * wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add - *

2. * sudo apt-get install apt-transport-https

3. * echo "deb https://artifacts.elastic.co/packages/7.x/apt stable main" | sudo tee -a /etc/apt/sources.list.d/elastic-7.x.list *

```



