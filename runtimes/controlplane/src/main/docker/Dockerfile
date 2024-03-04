# -buster is required to have apt available
FROM eclipse-temurin:21.0.2_13-jre-alpine

# Optional JVM arguments, such as memory settings
ARG JVM_ARGS=""
ARG JAR
ARG ADDITIONAL_FILES

RUN apk --no-cache add curl

WORKDIR /app


COPY ${JAR} edc-controlplane.jar
COPY ${ADDITIONAL_FILES} ./

EXPOSE 8080

ENV WEB_HTTP_PORT="8080"
ENV WEB_HTTP_PATH="/"

HEALTHCHECK --interval=5s --timeout=5s --retries=10 CMD curl --fail http://localhost:8080/api/check/health

# Use "exec" for graceful termination (SIGINT) to reach JVM.
# ARG can not be used in ENTRYPOINT so storing value in an ENV variable
ENV ENV_JVM_ARGS=$JVM_ARGS
# use the "exec" syntax so that SIGINT reaches the JVM -> graceful termination
CMD ["sh", "-c", "exec java  -Djava.util.logging.config.file=/app/logging.properties -Djava.security.egd=file:/dev/urandom -jar edc-controlplane.jar"]