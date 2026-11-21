# Étape 1 : Utiliser une image Maven avec Java 17 pour construire l'application
FROM maven:3.9-eclipse-temurin-17 AS build
WORKDIR /app
# On copie le pom.xml et le code source
COPY pom.xml .
COPY src ./src
# On compile et on crée le fichier .jar sans lancer les tests (ils seront lancés par Jenkins)
RUN mvn clean package -DskipTests

# Étape 2 : Utiliser une image Java légère pour exécuter l'application
FROM eclipse-temurin:17-jre-alpine
WORKDIR /app
# On copie le fichier .jar généré à l'étape 1
COPY --from=build /app/target/*.jar app.jar
# On expose le port (Spring Boot utilise 8080 par défaut)
EXPOSE 8080
# Commande pour lancer l'application
ENTRYPOINT ["java", "-jar", "app.jar"]
