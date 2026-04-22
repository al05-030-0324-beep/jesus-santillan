# Primera etapa: construir el WAR con Maven
FROM maven:3.9-eclipse-temurin-11 AS build
WORKDIR /app

# Copiar el archivo pom.xml y el código fuente
COPY pom.xml .
COPY src ./src

# Ejecutar Maven para generar el WAR (el archivo quedará en /app/target/)
RUN mvn clean package

# Segunda etapa: imagen final con Tomcat
FROM tomcat:11.0-jdk11

# Eliminar la aplicación por defecto de Tomcat
RUN rm -rf /usr/local/tomcat/webapps/ROOT

# Copiar el WAR generado en la etapa anterior
COPY --from=build /app/target/*.war /usr/local/tomcat/webapps/ROOT.war

# Exponer el puerto que usa Tomcat
EXPOSE 8080

# Comando para iniciar Tomcat
CMD ["catalina.sh", "run"]
