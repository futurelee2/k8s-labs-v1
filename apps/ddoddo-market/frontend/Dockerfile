# 1. 베이스 이미지 (Node.js)
FROM node:18-alpine AS build

# 2. 작업 디렉토리 설정
WORKDIR /app

# 3. 빌드용 ARG 선언 (빌드 시점에 전달받음)
ARG NEXT_PUBLIC_API_BASE_URL
ARG NEXT_PUBLIC_SUPABASE_URL
ARG NEXT_PUBLIC_SUPABASE_ANON_KEY

# 4. 환경변수 설정 (이미지 안에서 영구 적용)
ENV NEXT_PUBLIC_API_BASE_URL=$NEXT_PUBLIC_API_BASE_URL
ENV NEXT_PUBLIC_SUPABASE_URL=$NEXT_PUBLIC_SUPABASE_URL
ENV NEXT_PUBLIC_SUPABASE_ANON_KEY=$NEXT_PUBLIC_SUPABASE_ANON_KEY

# 5. 의존성 설치 준비 (package*.json 복사)
COPY package*.json ./

# 6. 의존성 설치
RUN npm install

# 7. 소스 코드 복사
COPY . .

# 8. Next.js 앱 빌드 (또는 Vite 등 빌드 명령어)
RUN npm run build
