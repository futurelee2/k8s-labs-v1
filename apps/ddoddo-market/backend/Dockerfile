# 1단계: 빌드용 이미지 (Gradle + JDK)
FROM gradle:7.6-jdk17 AS build

WORKDIR /app

# 소스 복사
COPY . .

# 빌드 (테스트 스킵)
RUN gradle clean build -x test

# 2단계: 실행용 이미지 (JRE)
FROM eclipse-temurin:17-jre

WORKDIR /app

# 빌드 산출물 복사 (보통 build/libs/*.jar)
COPY --from=build /app/build/libs/*.jar app.jar

ENTRYPOINT ["java", "-jar", "/app/app.jar"]

EXPOSE 8080
