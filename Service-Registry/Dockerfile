# -------- build stage --------
FROM maven:3.9.4-eclipse-temurin-21 AS build

WORKDIR /app

COPY pom.xml .
COPY src ./src

RUN mvn clean package -DskipTests

# -------- runtime stage --------
FROM eclipse-temurin:21-jre-jammy

WORKDIR /app

COPY --from=build /app/target/Service-Registry-0.0.1-SNAPSHOT.jar service-registry.jar

EXPOSE 8761

ENTRYPOINT ["sh", "-c", "java ${JAVA_OPTS:-} -jar service-registry.jar"]
