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

- Baseline: default jvm
java -jar discovery-center-0.0.1-SNAPSHOT.jar

	- Timing
		
		5.814 = 2019-06-25 22:32:57.974 - 2019-06-25 22:33:03.788

	- jstat -gc 

		 S0C    S1C    S0U    S1U      EC       EU        OC         OU       MC     MU    CCSC   CCSU   YGC     YGCT    FGC    FGCT     GCT
		7168.0 8192.0 7160.1  0.0   494080.0 332080.5  82944.0    15609.6   46760.0 44845.5 6312.0 5953.5     12    0.063   2      0.118    0.181



- 1st try: still 1 FGC
java -jar -Xms768m -Xmx768m -Xmn700m  -XX:SurvivorRatio=10 -XX:+PrintGCDetails  -XX:MetaspaceSize=50M discovery-center-0.0.1-SNAPSHOT.jar

5.542 = 2019-06-25 22:46:48.423 - 2019-06-25 22:46:53.965

S0C    S1C    S0U    S1U      EC       EU        OC         OU       MC     MU    CCSC   CCSU   YGC     YGCT    FGC    FGCT     GCT
59392.0 59392.0  0.0    0.0   598016.0 264071.9  69632.0    23958.9   51200.0 48840.8 7040.0 6531.4      4    0.122   1      0.192    0.313

- 2nd try: 0 Full GC
java -jar -Xms768m -Xmx768m -Xmn700m  -XX:SurvivorRatio=10 -XX:+PrintGCDetails  -XX:MetaspaceSize=80M discovery-center-0.0.1-SNAPSHOT.jar

5.166 = 2019-06-25 22:57:28.061 - 2019-06-25 22:57:33.227

S0C    S1C    S0U    S1U      EC       EU        OC         OU       MC     MU    CCSC   CCSU   YGC     YGCT    FGC    FGCT     GCT
59392.0 59392.0  0.0   24209.6 598016.0 204594.4  69632.0     104.0    51584.0 49021.5 7040.0 6555.6      3    0.127   0      0.000    0.127


## Heap dump

jmap -dump:format=b,file=discovery-center.dump $java-pid
jhat -port 8888 discovery-center.dump



