FROM gradle:7 AS base
CMD ["bash"]

# test-and-build
FROM base AS test-and-build
WORKDIR /workspace
COPY . .
RUN ./gradlew build

# production
# imageはgradleより軽いopenjdkを使用
FROM openjdk:17 AS production
COPY --from=test-and-build /workspace/build/libs/api-0.0.1-SNAPSHOT.jar ./api.jar
CMD ["java", "-jar", "api.jar"]