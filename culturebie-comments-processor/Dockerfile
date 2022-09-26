FROM maven:3.8.6-openjdk-8    
COPY . /app
WORKDIR /app
RUN mvn clean install -DskipTests
ENV CB_NLP_ENV=DEVELOPMENT
ENTRYPOINT [ "java","-jar","target/culturebie-comments-processor-1.0-SNAPSHOT.jar" ]

