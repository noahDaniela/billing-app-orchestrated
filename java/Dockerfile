# Usa una imagen base con JRE 17 en Alpine
FROM openjdk:8-jre-alpine

# Instalar el paquete 'shadow' que incluye 'addgroup' y 'adduser'
RUN apk add --no-cache shadow

# Crear el grupo 'devopsc' y el usuario 'admin'
RUN addgroup -g 1028 devopsc \
    && adduser -D -G devopsc admin

VOLUME /tmp

ARG JAR_FILE
ARG DB_PASSWORD

ENV DB_PASSWORD=$DB_PASSWORD

# Copiar el archivo JAR a /tmp
COPY ${JAR_FILE} /tmp/app.jar

# Dar permisos al usuario admin sobre /tmp
RUN chown -R admin:devopsc /tmp/app.jar

# Cambiar al usuario 'admin'
USER admin

# Ejecutar la aplicación como el usuario 'admin'
CMD ["java", "-jar", "/tmp/app.jar"]