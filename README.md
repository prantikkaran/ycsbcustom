This YCSB module pushes custom json to MongoDB in below format -> 
    {
  "_id": "user6284781860667377211",
  "name": "Johnnie Doe",
  "age": 30,
  "email": "john@example.com",
  "address": "1234 Elm Street, Springfield",
  "phone": "123-456-7890"
}

You can change the json inside mongodbclient.java file. 
Path -> /ycsbcustom/mongodb/src/main/java/site/ycsb/db/MongoDbClient.java

Userformat is kept like this as ycsb does read operation on id of format user12334

after cloning you need to download below jars and poms and execute following commands :-

org.restlet-2.3.0.jar
org.restlet.ext.servlet-2.3.0.jar
org.restlet.ext.servlet-2.3.0.pom
org.restlet.parent-2.3.0.pom

mvn install:install-file -DgroupId=org.restlet.jee \
    -DartifactId=org.restlet \
    -Dversion=2.3.0 \
    -Dpackaging=jar \
    -Dfile=pathToFile/org.restlet-2.3.0.jar


mvn install:install-file -DgroupId=org.restlet.jee \
    -DartifactId=org.restlet.ext.servlet \
    -Dversion=2.3.0 \
    -Dpackaging=jar \
    -Dfile=pathToFile/org.restlet.ext.servlet-2.3.0.jar


mvn install:install-file -DgroupId=org.restlet.jee \
    -DartifactId=org.restlet.ext.servlet \
    -Dversion=2.3.0 \
    -Dpackaging=pom \
    -Dfile=pathToFile/org.restlet.ext.servlet-2.3.0.pom

mvn install:install-file \
  -DgroupId=org.restlet.jee \
  -DartifactId=org.restlet.parent \
  -Dversion=2.3.0 \
  -Dpackaging=pom \
  -Dfile=pathToFile/org.restlet.parent-2.3.0.pom


After this you're good to go : 

to load data into DB - 
./bin/ycsb load mongodb -s -P workloads/workloada -p mongodb.url="mongodb://127.0.0.1:27018/ycsb" -threads 2

to execute complete workload - 
./bin/ycsb run mongodb -s -P workloads/workload_custom -p mongodb.url="mongodb://127.0.0.1:27018/ycsb" -threads 2  
Note - Check workload_custom file inside workloads directory to check scenario. 

