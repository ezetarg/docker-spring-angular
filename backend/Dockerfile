FROM gradle:jdk11 as builder

WORKDIR /home/gradle/project
RUN git clone https://github.com/ezetarg/springboot-sample1.git . &&  gradle build --no-daemon

FROM openjdk:11-jdk-slim

WORKDIR /home/server/
COPY --from=0 /home/gradle/project/build/libs/*.jar /home/server/service.jar

ENTRYPOINT ["java", "-XX:+UnlockExperimentalVMOptions", "-Djava.security.egd=file:/dev/./urandom","-jar","/home/server/service.jar"]
