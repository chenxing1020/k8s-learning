FROM openjdk:8
COPY *.jar /app.jar
CMD ["--spring.profiles.active=prod"]
EXPOSE 8080
ENTRYPOINT ["java","-jar","/app.jar"]
