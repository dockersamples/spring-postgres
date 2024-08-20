# spring-postgres

This repository demonstrates the steps of seamlessly connecting a locally running Spring Boot application to a containerized PostgreSQL database, providing a practical foundation for your development projects. The overall project augment traditional development workflows. Developers maintain their familiar local development environments while offloading specific dependencies into isolated containers. This hybrid model optimizes resource utilization and enhances development efficiency.

## Prerequisite:

- [OpenJDK](https://www.java.com/en/download/)
- [Docker Desktop](https://www.docker.com/products/docker-desktop/)
- [Eclipse](https://www.eclipse.org/downloads/download.php)

## Importing the project to Eclipse

Before you follow the steps, ensure that you clone the repository locally on your system.

- Open Eclipse
- Go to File -> Import. 
- Select Maven -> Existing Maven Projects.
- Click Next.  
- Browse to the root directory of your Spring Boot project.
- Select the project and click Finish.

## Build the application project

Right-click on the main project and select “Maven Build” under “Run as”.

```
[INFO] Scanning for projects...
[INFO]
[INFO] [1m------------------------< [0;36mcom.company:project[0;1m >-------------------------[m
[INFO] [1mBuilding New App 0.0.1-SNAPSHOT[m
....
---------------------------------------------------[m
[INFO] [BUILD SUCCESS[m
[INFO] [1m------------------------------------------------------------------------[m
[INFO] Total time:  2.320 s
[INFO] Finished at: 2024-08-15T19:22:25+05:30
[INFO] [1m------------------------------------------------------------------------[m
```



## Running Postgres in a Docker container

```
docker run --name postgres_container -e POSTGRES_PASSWORD=mysecretpassword -d -p 5432:5432 -v postgres_data:/var/lib/postgresql/data postgres
```

## Configuring the application properties

Open `application.properties` in your project's `src/main/resources` directory. 
Replace the entries with the actual name of the Postgres host, database and credentials details.

```
spring.jpa.properties.hibernate.dialect = org.hibernate.dialect.PostgreSQLDialect
spring.jpa.hibernate.ddl-auto=none
spring.jpa.hibernate.show-sql=true
spring.datasource.url=jdbc:postgresql://localhost:5432/postgres
spring.datasource.username=postgres
spring.datasource.password=mysecretpassword
spring.datasource.initialization-mode=always
spring.datasource.initialize=true
spring.datasource.schema=classpath:/schema.sql
spring.datasource.continue-on-error=true
```

Save the file once you make the changes by clicking on “Save” option in the top navigation.

## Running the application

- Running the Spring Boot application
- Right-click on your project.
- Select "Run As" -> "Maven Build".
- In the "Goals" field, enter `spring-boot:run`.

## Verify if the Spring Boot is up and running.

```
curl https://localhost:8080
Hello from Docker
```
