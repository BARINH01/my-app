# Koristimo openjdk:11 kao base image
FROM openjdk:11-jre-slim

# Radni direktorij unutar containera
WORKDIR /app

# Kopiraj JAR datoteku u container
COPY target/my-java-app-1.0-SNAPSHOT.jar app.jar

# Naredba koja se izvršava kad se container pokrene
CMD ["java", "-jar", "app.jar"]
