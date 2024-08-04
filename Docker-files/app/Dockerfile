FROM openjdk:11 AS BUILD_IMAGE

# Install Maven and Git
RUN apt update && apt install -y maven git

# Clone the repository
RUN git clone https://github.com/chinmayasahu17/vprofile-project.git

# Set the working directory
WORKDIR vprofile-project

# Checkout the 'docker' branch and build the project
RUN git checkout docker && mvn install

# Check contents of target directory
RUN ls -l target

# Create the final image with Tomcat
FROM tomcat:9-jre11

# Remove existing webapps
RUN rm -rf /usr/local/tomcat/webapps/*

# Copy the built WAR file to Tomcat's webapps directory
COPY --from=BUILD_IMAGE vprofile-project/target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war

EXPOSE 8080
CMD ["catalina.sh", "run"]
