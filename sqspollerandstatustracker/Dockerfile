FROM maven:3.8.6-openjdk-8    
COPY . /app
WORKDIR /app
RUN mvn clean install -DskipTests
VOLUME  ../culturebie_csv_downloader ./directory
RUN ls -la
COPY target/SqsPollerAndStatusTracker-1.0-SNAPSHOT.jar directory/
RUN ls -la
RUN ls -la directory
ENV CB_NLP_ENV=DEVELOPMENT
ENTRYPOINT [ "java","-jar","target/SqsPollerAndStatusTracker-1.0-SNAPSHOT.jar" ]

