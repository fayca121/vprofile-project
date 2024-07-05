FROM eclipse-temurin:11.0.23_9-jdk AS BUILD_IMAGE
RUN apt update && apt install -y ca-certificates git maven
RUN git clone https://github.com/fayca121/vprofile-project.git && \
    cd vprofile-project && \
    git checkout docker && \
    mvn install

FROM tomcat:9.0.90-jre11
LABEL "Project"="Vprofile"
LABEL "Author"="Bououza"
RUN rm -fr /usr/local/tomcat/webapps/*
COPY --from=BUILD_IMAGE vprofile-project/target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war
EXPOSE 8080
CMD ["catalina.sh","run"]