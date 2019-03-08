# Integration testing with Spring Boot, Elasticsearch, Testcontainers and JUnit5

Simple example demonstrating how testcontainers and JuUnit 5 can play together.

## Used technologies

* Spring Boot 2.1.3.RELEASE
* Kotlin 1.3.21
* Elasticsearch 6.6.1 with [RestHighLevelClient](https://www.elastic.co/guide/en/elasticsearch/client/java-rest/current/java-rest-high-getting-started-initialization.html)
* Testcontainers 1.10.6
* JUnit 5.4.0

## Requirements

* Java 11
* Maven >= 3.2.1 (Kotlin comes as maven dependency)
* Docker >= 3.0 (for integration tests)

##### Clone repository and build project

Integration test ```TweetControllerIT``` will be startet in maven phase ```verify```.

```ssh
git clone https://github.com/larmic/testcontainers-junit5
mvn clean verify
```

##### Local testing

```ssh
# start local elasticsearch
docker run -d -p 9200:9200 -p 9300:9300 --name testcontainers-junit5-demo -e "discovery.type=single-node" -e "xpack.security.enabled=false" -e "cluster.name=elasticsearch" docker.elastic.co/elasticsearch/elasticsearch-oss:6.6.1

# start application
mvn spring-boot:run

# HTTP request examples
# Get all tweets
curl -i -H "Accept: application/json" --request GET http://localhost:8080/

# Post a new tweet
curl -i -H "Content-Type: application/json" --request POST --data 'hello, this is a tweet!' http://localhost:8080/

# Read a specific tweet     
curl -i -H "Accept: application/json" --request GET http://localhost:8080/{tweet-id}      
 
# Delete a specific tweet
curl -i -H "Accept: application/json" --request DELETE http://localhost:8080/{tweet-id}

# Update a specific tweet    
curl -i -H "Content-Type: application/json" "Accept: application/json" --request PUT --data 'hello, this is a changed tweet!' http://localhost:8080/{tweet-id}        
```
