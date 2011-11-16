NUTCH-MONGODB-INDEXER README

Compatible With:
   Nutch 1.3

For the latest information about Nutch, please visit the website at:

   http://nutch.apache.org

our the wiki, at:

   http://wiki.apache.org/nutch/

To get started using Nutch read Tutorial:

   http://wiki.apache.org/nutch/NutchTutorial

For the latest information about elastic search, please visit the website at:

   http://www.elasticsearch.org/

our the wiki, at:

   http://www.elasticsearch.org/guide/

To get started using Mongodb and Java read these Tutorials

   http://www.elasticsearch.org/guide/reference/setup/
   http://www.elasticsearch.org/guide/reference/api/
   http://www.elasticsearch.org/guide/reference/java-api/

Important Stuff

This patch was created to allow for the indexing of Nutch crawl data directly into elasticsearch.  This is similar in nature to that of the SolrIndexer that comes with Nutch which let you index directly into Solr.  This provides a way directly index data into elasticsearch coming directly from Nutch.    

This is just the code necessary to create the solution.  You must start by having the Nutch codebase and have it setup in your development environment (Eclipse) see http://wiki.apache.org/nutch/RunNutchInEclipse for how do this.  Once you are set up and is working well.  You are ready to get started.  The following files below are necessary to integrate into the notch base and then re-build notch.

In order to run this you need a working copy of the Nutch source and access to a elasticsearch environment.

Folder Structure
----> java/org/apache/nutch/indexer/elasticsearch/ElasticsearchConstants.java
----> java/org/apache/nutch/indexer/elasticsearch/ElasticsearchIndexer.java
----> java/org/apache/nutch/indexer/elasticsearch/ElasticsearchWriter.java
----> ivy/ivy.xml

Step 1. Create a new package called "java.org.apache.nutch.indexer.elasticsearch" and place the the files "ElasticsearchConstants.java", "ElasticsearchIndexer.java" and "ElasticsearchWriter.java" in the package

Step 2. Modify your ivy configuration.  Open the ivysettings.xml and ivy.xml and add the elastic search java driver information to the existing ivy/ivysettings.xml and ivy/ivy.xml files.

Step 3. Rebuild and you should be ready to test

Step 4. To test you can run the following commands from terminal

Make sure you have seeded your crawl db with URLs

----> bin/nutch org.apache.nutch.indexer.elasticsearch.Elasticsearch localhost 9302 crawl/crawldb crawl/linkdb crawl/segments/*
To see the available parameters

localhost - is the location of your mongodb database (used to connect)
port - is the port location of your elastic search server
crawldb - location of your crawled
linkdb - location of your linkdb
segments - location of your segments

----> Once you verified there are no errors, you can test to see if you can access "http://localhost:9200/nutch/index/_search?q=*"