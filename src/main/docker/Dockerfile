# - to build a docker image from this Dockerfile: 'docker build -t spring-boot-docker .'
# - to run this local docker image: 'docker run -d --publish 8080:8080 spring-boot-docker'

FROM centos

# after updating springbootwebapp to Java 11,
# the docker image has to use java-11-openjdk
# default in centos is still Java 1.8
RUN yum install -y java-11

# Spring Boot expects a '/tmp'-folder
VOLUME /tmp

# moving Maven-packaged jar into container and renaming it
ADD spring-boot-web-0.0.1-SNAPSHOT.jar myapp.jar

# 'sh -c' runs the following command on the bourne-shell inside the container
# 'touch' updates the date (timestamp) on the jar-file
# this can be important for static ressources (images...), e.g. regarding cache etc.
RUN sh -c 'touch /myapp.jar'

# "from the Spring guys":
# ENTRYPOINT will run the given command on container start
# '-Djava-security.egd=file:/dev/./urandom' helps JRE starting faster
ENTRYPOINT ["java", "-Djava-security.egd=file:/dev/./urandom", "-jar", "/myapp.jar"]
