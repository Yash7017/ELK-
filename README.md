## ELK

ELK setup for Virtual Machine while using Microsoft Azure Cloud. We will set up ElasticSearch, Logstash and kibana on master server. Filebeat will be there to fetch the logs from client server. Curator will be there to delete the older logs. elast-alert to raise the alert for matching pattern and keywords. We will also configure kibana dashboard.

We will be doing it in different repositories and setup for our VM. 

First of all we will configure dependencies before setting up Elasticsearch. Dependencies include openjdk and nginx. 

***Note: All Text written in copy file should be executed in command line*

**java version -**

The ELK stack requires Java 8 to be installed. Check the java version first, if it indicates java is installed then ok.  
```
java -version
```
Otherwise install java 8 using below commands
```
sudo apt-get install openjdk-8-jdk
```

If prompted, type y and hit the Enter for process to finish. 

**nginx -**

Nginx works as a web server and proxy server. it's used to configure pasword-controlled access to the kibana dashbaord. 

Install Nginx by entering: 
```
sudo apt-get install nginx
```

## Now we will start configuration for Elastic search

** Before going for ELK setup, one thing need to keep in mind that we install all packages of Elastic search, kibana, logstash and filebeat. after checking their compatablity through given link https://www.elastic.co/support/matrix **

We will add ** Elastic Repository **

it enable us to have the access to ELK stack. 

* We will import PGP key and install apt-transport-https package. then we will add elastic repository to our system repository list: Run the following commands one by one: 

```
wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add - 
```
```
sudo apt-get install apt-transport-https
```
```
echo "deb https://artifacts.elastic.co/packages/7.x/apt stable main" | sudo tee -a /etc/apt/sources.list.d/elastic-7.x.list 
```
## Install ElasticSearch

We will update the repositories and install ElasticSearch. Run the command one by one:

```
sudo apt-get update
```
```
sudo apt-get install elasticsearch
```
## Configure ElasticSearch

We configure Elasticsearch based on our need. We are updating here based on our basic need that includes, fetching logs from filebeat from client machine and ship that logs to logstash. logstash aggregates the data process it and sends all data to Elasticsearch where indexing and storage is done. then it will send to kibana to create dashboards. apart from this, we are gonna raise the alert for exceeding the matching pattern or keywords and we will configure curator too that will delete the older logs so that it doesnt overburden our system. 

We have commit how to do everything. if it helps go through all other commits too. 

so coming back to ElasticSearch configuration: 

We will configure the file on the given path. We will run the command in command line. 

```
sudo nano /etc/elasticsearch/elasticsearch.yml
```
* Here we will see a file with different entries and descriptions. this is an yml file, here the line that starts with # means these are in comment. While executing these commands are exempted. We can uncomment them by removing '#'. 

**what i am going to write here, is only uncomment section that I have in my file for making it work. you can configure it based on your needs. copy this and paste this in our elasticsearch.yml file. and exit the file with saving it. you can press ctrl+c and then follow the command in footer to save the file.**

```
cluster.name: my-application 
node.name: internal-tmp-kbmax 
path.data: /var/lib/elasticsearch 
path.logs: /var/log/elasticsearch 
network.host: "master server ip" 
http.port: 9200
cluster.initial_master_nodes: ["master server private ip"]
```
*Here we update master server private ip with our system private ip on which we are installing our ELK setup*

## Start Elasticsearch 

We will run this command to start Elasticsearch. This command will not give any output if successful. 
```
sudo systemctl start elasticsearch.service 
```



