---
layout: post
title: "GitHub Pages + Jekyll(Bay 테마)로 블로그 만들기"
category: tech-docs
tags: [github-pages, jekyll, blog]
blurb: "github.io 블로그를 만들면서 겪은 설정 문제와 해결 과정 정리"
---

## GitHub Pages란?

GitHub Pages는 GitHub 저장소에 올린 정적 파일(HTML/CSS/JS)을 그대로 웹사이트로 호스팅해 주는 무료 서비스다.
저장소 이름을 `<사용자명>.github.io`로 만들면 `https://<사용자명>.github.io/` 주소의 **유저 페이지**가 되고,
다른 이름의 저장소는 `https://<사용자명>.github.io/<저장소명>/` 형태의 **프로젝트 페이지**가 된다.

Jekyll은 Markdown으로 쓴 글을 정적 HTML로 바꿔 주는 사이트 생성기로, GitHub Pages와 궁합이 좋다.
이 블로그는 [Bay](https://github.com/eliottvincent/bay) 테마를 기반으로 만들었다.

## 처음에 겪은 문제들

| 증상 | 원인 | 해결 |
|---|---|---|
| 메뉴 링크가 전부 원작자 사이트로 이동 | `_config.yml`의 `url`, `baseurl`이 테마 원작자 값 그대로 | 내 주소로 변경 |
| `main`에 push해도 사이트가 안 바뀜 | 배포 워크플로가 `master` 브랜치만 감시 | `branches: ["main"]`으로 수정 |
| (보안) 방문 기록이 남의 GA로 전송 | 원작자의 Google Analytics ID가 남아 있음 | ID 제거, 내 ID가 있을 때만 로드 |

특히 마지막 항목은 템플릿을 포크할 때 놓치기 쉬운 부분이다. 내 블로그 방문자의 접속 정보가
제3자의 분석 계정으로 넘어가고 있었던 셈이라, 템플릿을 가져다 쓸 때는 `head`에 들어간
외부 스크립트부터 확인하는 습관을 들이는 게 좋다.

## 카테고리 구성

글은 6개 카테고리로 나눈다. 카테고리 목록은 `_data/categories.yml`에서 관리하고,
글마다 front matter에 `category` 값을 지정한다.

```yaml
---
layout: post
title: "글 제목"
category: ctf-wargame   # dev / ctf-wargame / bugbounty / tech-docs / paper-conference / contest-cert
tags: [pwnable, dreamhack]
blurb: "목록에 보일 한 줄 요약"
---
```

## 배포 흐름

1. `_posts/YYYY-MM-DD-제목.md` 파일을 만들어 글을 쓴다.
2. `main` 브랜치에 push한다.
3. GitHub Actions가 Jekyll로 빌드해 Pages에 배포한다 (1~2분).
