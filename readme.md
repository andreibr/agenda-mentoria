# Projeto: AGENDA API (API para armazenamento/leitura de tarefas)

# required apps:
  - maven
  - java 11
  - mysql/mariadb
  - curl (or similar)
  - jq (to a best view of results)

# to running as container (optional):
    - kind

# database configure:
  - create database db_todolist
  - create table task(
                 id int auto_increment primary key,
                 task_name varchar(50),
                 task_status tinyint,
                 task_description varchar(256),
                 task_init_date date,
                 task_final_date date) default charset=utf8;

# to compile and run (on localhost), if you want to run this on your machine, it isn't necessary
  - database must be running
  = adjuste your database connection on src/main/resorces/applicaiton.properties
  - mvn clean package -DskipTests
  - java -jar target/agenda-1.0.0.jar

# to do some tests:
  - task_status: pending or completed
  - POST (insert)
    - curl -H 'Content-Type: application/json' -d '{"task_name":"task1","task_status":"pending","task_description":"task1 desc","task_init_date":"yyyy-mm-dd","task_final_date":null}' 
	   -X POST http://127.0.0.1:25000/v0/to-do/ | jq
  - GET (query)
    - curl -H 'Content-Type: application/json' -X GET http://127.0.0.1:25000/v0/to-do/ | jq
    - curl -H 'Content-Type: application/json' -X GET http://127.0.0.1:25000/v0/to-do/<b>ID</b> | jq
  - PUT (update)
    - curl -H 'Content-Type: application/json' -d '{"id":"<b>ID</b>","task_name":"task1","task_status":"pending","task_description":"task1 desc","task_init_date":"yyyy-mm-dd","task_final_date":null}' -X PUT http://127.0.0.1:25000/v0/to-do/<b>ID</b> | jq
  - DELETE
    - curl -H 'Content-Type: application/json' -X DELETE http://127.0.0.1:25000/v0/to-do/<b>ID</b> 

# Exercise:
    -  Run this application in a k8s cluster (kind), you must run:
	- mysql as a pod (and it needs a volume)
	- java application as a pod
  
### good wekend!
