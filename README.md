ELK-

ELK setup for Virtual Machine while using Microsoft Azure Cloud. We will set up ElasticSearch, Logstash and kibana on master server. Filebeat will be there to fetch the logs from client server. Curator will be there to delete the older logs. elast-alert to raise the alert for matching pattern and keywords. We will also configure kibana dashboard.

We will be doing it in different repositories and setup for our VM. 



The ELK stack requires Java 8 to be installed. Check the java version first, if it indicates java is installed then ok.  

*java -version*

Otherwise install java 8 using below commands
 sudo apt-get install openjdk-8-jdk

If prompted, type y and hit the Enter for process to finish. 
