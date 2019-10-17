FROM openjdk:8-jre-alpine

EXPOSE 8585

ENTRYPOINT ["java",\
            "-Djava.security.egd=file:/dev/./urandom",\
            "-Dhttp.nonProxyHosts=localhost",\
            "-jar",\
            "/cors-1.0-SNAPSHOT.jar"\
]

ADD build/libs/*.jar /cors-1.0-SNAPSHOT.jar
