# 🚀 GitBook 배포 가이드

## 📋 배포 개요

이 프로젝트는 GitBook 형태로 구성되어 있으며, 다양한 방법으로 배포할 수 있습니다.

## 🔧 GitBook CLI를 사용한 로컬 배포

### 1. GitBook CLI 설치
```bash
# GitBook CLI 전역 설치
npm install -g gitbook-cli

# GitBook 초기화 (프로젝트 루트에서)
gitbook init

# 플러그인 설치
gitbook install
```

### 2. 로컬 서버 실행
```bash
# 개발 서버 실행 (자동 리로드)
gitbook serve

# 빌드만 실행
gitbook build

# 특정 포트로 실행
gitbook serve --port 4001
```

### 3. 접속
- 브라우저에서 `http://localhost:4000` 접속
- 자동으로 GitBook 형태로 렌더링된 문서 확인

## 🌐 GitHub Pages 배포

### 1. GitHub 저장소 생성 및 푸시
```bash
# GitHub에 저장소 생성 후
git remote add origin https://github.com/username/uni-search.git
git branch -M main
git push -u origin main
```

### 2. GitHub Pages 설정
1. GitHub 저장소 → Settings → Pages
2. Source: Deploy from a branch
3. Branch: main / root 선택
4. Save 클릭

### 3. 자동 배포
- GitHub Actions를 통한 자동 배포 설정 가능
- 커밋 시 자동으로 GitBook 빌드 및 배포

## 📱 GitBook.com 클라우드 배포

### 1. GitBook 계정 생성
- [GitBook.com](https://www.gitbook.com)에서 계정 생성
- GitHub 계정으로 연동 가능

### 2. 저장소 연결
- New Space 생성
- GitHub Integration으로 저장소 연결
- 자동으로 GitBook 문서 생성

### 3. 실시간 동기화
- GitHub 커밋 시 자동으로 GitBook 업데이트
- 협업 및 댓글 기능 활용 가능

## 🖥️ Netlify 배포

### 1. Netlify 계정 생성
- [Netlify.com](https://www.netlify.com)에서 계정 생성

### 2. GitBook 빌드 설정
```bash
# package.json에 빌드 스크립트 추가
{
  "scripts": {
    "build": "gitbook build"
  }
}
```

### 3. 배포 설정
- New site from Git 선택
- GitHub 저장소 연결
- Build command: `npm run build`
- Publish directory: `_book`

## 🐳 Docker 배포

### 1. Dockerfile 생성
```dockerfile
FROM node:14-alpine

WORKDIR /app
COPY package*.json ./
RUN npm install -g gitbook-cli
RUN gitbook install

COPY . .
RUN gitbook build

FROM nginx:alpine
COPY --from=0 /app/_book /usr/share/nginx/html
EXPOSE 80
```

### 2. Docker 실행
```bash
# 이미지 빌드
docker build -t uni-search-guide .

# 컨테이너 실행
docker run -p 8080:80 uni-search-guide
```

## 📊 배포 방식 비교

| 방식 | 장점 | 단점 | 추천도 |
|------|------|------|---------|
| **GitHub Pages** | 무료, 간단, GitHub 연동 | GitBook 플러그인 제한 | ⭐⭐⭐⭐⭐ |
| **GitBook.com** | 전문적, 협업 기능 | 유료 (프리미엄 기능) | ⭐⭐⭐⭐☆ |
| **Netlify** | 빠름, CDN, 커스터마이징 | 빌드 설정 필요 | ⭐⭐⭐⭐☆ |
| **로컬 서버** | 개발용, 빠른 테스트 | 외부 접근 불가 | ⭐⭐⭐☆☆ |
| **Docker** | 일관성, 확장성 | 복잡, 서버 필요 | ⭐⭐⭐☆☆ |

## 🔍 추천 배포 전략

### 1단계: 로컬 테스트
```bash
gitbook serve
```
- 내용 확인 및 수정

### 2단계: GitHub Pages 배포 (무료)
- 가장 간단하고 빠른 공개 배포
- URL: `https://username.github.io/uni-search`

### 3단계: 도메인 연결 (선택)
- GitHub Pages에 커스텀 도메인 연결
- 예: `uni-guide.com`

## 📱 모바일 최적화

GitBook은 기본적으로 반응형 디자인을 제공하여 모바일에서도 최적화된 사용자 경험을 제공합니다.

- **자동 반응형**: 화면 크기에 따른 자동 조정
- **터치 네비게이션**: 모바일 친화적 메뉴
- **검색 기능**: 모바일에서도 완전한 검색 지원

## 🚀 빠른 시작 (권장)

**GitHub Pages로 5분 내 배포**:

1. 현재 프로젝트를 GitHub에 푸시
```bash
git remote add origin https://github.com/yourusername/uni-search.git
git push -u origin main
```

2. GitHub 저장소 Settings → Pages → main 브랜치 선택

3. 5-10분 후 `https://yourusername.github.io/uni-search` 접속

🎉 **완료! 이제 전 세계 어디서든 가이드북에 접근 가능합니다.**

## 📞 문제 해결

### 플러그인 오류
```bash
gitbook uninstall
gitbook install
```

### 빌드 오류
```bash
gitbook build --debug
```

### 포트 충돌
```bash
gitbook serve --port 4001
```