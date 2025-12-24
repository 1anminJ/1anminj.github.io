---
title: GitHub Pages로 기술 블로그 만들기 (with Jekyll Chirpy)
date: 2025-12-24 17:00:00 +0900
categories: [Project, Setup]
tags: [github-pages, jekyll, chirpy, troubleshooting, blog]
---

## 👋 시작하며: 바이브코딩 탈출을 선언하다

2026년 1, 2월 겨울방학을 앞두고 다짐을 하나 했다.
지금까지 AI와 자동완성에 의존하던 '바이브코딩(Vibe Coding)'을 멈추고, **"내가 짠 코드가 왜 돌아가는지 아는"** 진짜 개발 공부를 하기로.

그 여정을 기록하기 위해 **GitHub Pages**에 블로그를 만들기로 결심했다. Velog도 좋지만, Git 관리 역량도 보여주고 나만의 커스텀 공간을 갖고 싶었기 때문이다.

테마는 깔끔하고 기능이 강력한 [Chirpy](https://github.com/cotes2020/jekyll-theme-chirpy)를 선택했다. 하지만 시작부터 순탄치 않았다.

## 🚨 문제 발생: 배포가 안 된다?

가이드대로 Fork를 뜨고 설정을 마쳤는데, GitHub Actions에서 계속 빨간불(❌)이 떴다.
로그를 살펴보니 `HTMLProofer`가 링크가 다 깨졌다고 아우성이었다.

```
At _site/github.io/404.html:1:
  internally linking to /assets/css/jekyll-theme-chirpy.css, which does not exist
...
HTML-Proofer found 107 failures!

```

자세히 보니 경로가 이상했다.
원래라면 `_site/404.html`이어야 하는데, 중간에 `github.io` 라는 폴더가 하나 더 껴있는 것이었다.

### 💡 원인: 저장소 이름(Repository Name)의 실수

알고 보니 **저장소 이름**이 문제였다.
GitHub Pages에는 두 가지 종류가 있다.

1. **User Site**: `username.github.io` (루트 도메인 사용)
2. **Project Site**: `username.github.io/project-name` (하위 경로 사용)

나는 내 아이디(`1anminj`)를 포함한 `1anminj.github.io`로 만들었어야 했는데, **그냥 `github.io`라고만 이름을 지었던 것**이다.
그러다 보니 GitHub는 이걸 '내 메인 블로그'가 아니라 'github.io라는 이름의 프로젝트'로 인식했고, 경로가 꼬이면서 모든 링크가 터져버린 것이었다.

## 🛠️ 해결 과정

### 1. 저장소 이름 변경 (Rename)

GitHub 저장소의 `Settings` > `General` 탭으로 가서 이름을 수정했다.

- (X) `github.io`
- (O) **`1anminj.github.io`**

### 2. `_config.yml` 설정 수정

이름을 바꾸면서 설정 파일(`_config.yml`)도 다시 꼼꼼히 손봤다.
특히 URL 부분과 특수문자(`&`) 처리가 중요했다.

```
# URL에 내 아이디가 포함된 전체 주소 입력
url: 'https://1anminj.github.io'

# 특수문자(&)가 들어간 문구는 따옴표('')로 감싸기
tagline: 'Dev(Java & Python) Journey'

```

이렇게 수정하고 나니 드디어 Actions 탭에 초록불(✅)이 들어왔다!

## 🚀 앞으로의 계획

이제 1월 1일부터 본격적으로 달릴 준비가 끝났다.
이곳에는 주로 **깊이 있는 기술 분석(Deep Dive)** 글을 올릴 예정이다.

- **Java:** JVM 메모리 구조, OOP의 본질, Spring 동작 원리
- **Python:** 데이터 핸들링, 효율적인 코드 작성법
- **Troubleshooting:** 개발하다 마주친 에러와 해결 과정

가벼운 요약이나 팁은 [Velog](https://velog.io/)에 올리고, 깊게 판 내용은 여기에 정리하는 **Two-Track 전략**으로 운영해볼 생각이다.

2026년 겨울, 제대로 성장해보자. 🔥

### 📢 더 쉬운 요약이 필요하다면?

이 글은 블로그 구축 과정의 기술적 트러블슈팅을 다룬 내용입니다.
가볍게 읽기 좋은 개발 팁이나 회고는 제 [Velog](https://velog.io/)에서도 확인하실 수 있습니다!
