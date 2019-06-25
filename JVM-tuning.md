# JVM-tuning

## History

- 2019.6.25 created

## Author

- Bruce Lu

## Env.

- Spring Cloud Greenwich
- Spring Boot 2.1.5
- Java HotSpot(TM) 64-Bit Server VM (build 25.181-b13, mixed mode)
- STS (Spring Tool Suite) 4.1.1
- MackBook Pro Mojave

## Objective

- Minimize Full GC, down to 0 if possible

## Prerequisites

- jar
mvn -B -DskipTests clean package


## Base line - default JVM settings

java -jar discovery-center-0.0.1-SNAPSHOT.jar

5.814 = 2019-06-25 22:32:57.974 - 2019-06-25 22:33:03.788






