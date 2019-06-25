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


## Use cases

- Default jvm
java -jar discovery-center-0.0.1-SNAPSHOT.jar

	- Timing
		
		5.814 = 2019-06-25 22:32:57.974 - 2019-06-25 22:33:03.788

- jstat -gc 

 S0C    S1C    S0U    S1U      EC       EU        OC         OU       MC     MU    CCSC   CCSU   YGC     YGCT    FGC    FGCT     GCT
7168.0 8192.0 7160.1  0.0   494080.0 332080.5  82944.0    15609.6   46760.0 44845.5 6312.0 5953.5     12    0.063   2      0.118    0.181




java -jar -Xms300m -Xmx300m -XX:NewRatio=1  -XX:SurvivorRatio=10 -XX:+PrintGCDetails  -XX:MetaspaceSize=100M discovery-center-0.0.1-SNAPSHOT.jar




