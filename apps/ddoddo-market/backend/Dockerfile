# # 1단계: 빌드용 이미지 (Gradle + JDK)
# FROM gradle:7.6-jdk17 AS build

# WORKDIR /app

# # 소스 복사
# COPY . .

# # 빌드 (테스트 스킵)
# RUN gradle clean build -x test

# # 2단계: 실행용 이미지 (JRE)
# FROM eclipse-temurin:17-jre

# WORKDIR /app

# # 빌드 산출물 복사 (보통 build/libs/*.jar)
# COPY --from=build /app/build/libs/*.jar app.jar

# ENTRYPOINT ["java", "-jar", "/app/app.jar"]

# EXPOSE 8080


# ## 지은님 코드
# FROM openjdk:17-jdk-slim

# WORKDIR /app

# # Gradle Wrapper 파일 복사
# COPY gradlew /app/gradlew
# COPY gradle /app/gradle
# RUN chmod +x ./gradlew

# # 빌드 설정 파일 복사
# COPY build.gradle /app/build.gradle
# COPY settings.gradle /app/settings.gradle

# # 의존성 미리 다운로드
# RUN ./gradlew build --no-daemon --parallel --continue --stacktrace -x test || true

# # 전체 소스 코드 복사 (실제 실행 시에는 볼륨으로 대체)
# COPY . .
# RUN chmod +x ./gradlew
# # 개발 환경에서는 디버깅 포트를 열어둡니다.
# EXPOSE 8080

# # 애플리케이션을 devtools 모드로 실행
# CMD ["/bin/bash", "-c", "./gradlew bootRun"]


# # 경우님 코드
# #1단계: Gradle 이미지로 빌드
# FROM gradle:8.5-jdk17 AS builder
# WORKDIR /app

# #소스 전체 복사
# COPY . .

# #Gradle CLI로 BootJar 생성 (–no-daemon 옵션으로 데몬 없이 실행)
# RUN gradle bootJar --no-daemon

# #2단계: JRE만 담긴 슬림 이미지에 JAR 복사
# FROM openjdk:17-jdk-slim
# WORKDIR /app

# #빌드 결과 JAR 파일(app/build/libs/*.jar)을 app.jar로 복사
# COPY --from=builder /app/build/libs/*.jar app.jar

# #컨테이너 시작 시 Spring Boot 앱 구동
# ENTRYPOINT ["java", "-jar", "app.jar"]



#인수
FROM openjdk:17-jdk-slim

WORKDIR /app

#Gradle Wrapper 파일 복사
COPY gradlew /app/gradlew
COPY gradle /app/gradle
RUN chmod +x ./gradlew

#빌드 설정 파일 복사
COPY build.gradle /app/build.gradle
COPY settings.gradle /app/settings.gradle

#의존성 미리 다운로드
RUN ./gradlew build --no-daemon --parallel --continue --stacktrace -x test || true

#전체 소스 코드 복사 (실제 실행 시에는 볼륨으로 대체)
COPY . .
RUN chmod +x ./gradlew

#개발 환경에서는 디버깅 포트를 열어둡니다.
EXPOSE 8080

#애플리케이션을 devtools 모드로 실행
CMD ["./gradlew", "bootRun"]