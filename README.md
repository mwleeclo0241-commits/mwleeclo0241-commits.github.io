# Minwoo's Security Log

[Bay](https://github.com/eliottvincent/bay) Jekyll 테마 기반의 개인 보안 블로그입니다.

## 카테고리

| slug | 이름 |
|---|---|
| `dev` | 개발 |
| `ctf-wargame` | CTF/Wargame |
| `bugbounty` | BugBounty |
| `tech-docs` | 블로그/기술문서 |
| `paper-conference` | 논문/컨퍼런스 |
| `contest-cert` | 공모전/자격증 |

카테고리 이름·설명은 `_data/categories.yml`에서 바꿀 수 있습니다.

## 새 글 쓰기

`_posts/` 폴더에 `YYYY-MM-DD-영문-제목.md` 파일을 만들고 아래 머리말을 붙입니다.

```markdown
---
layout: post
title: "[Dreamhack] basic_exploitation_000 풀이"
category: ctf-wargame
tags: [pwnable, bof]
blurb: "목록에 표시될 한 줄 요약"
---

본문을 Markdown으로 작성합니다.
```

- 이미지: `assets/img/posts/` 에 넣고 `![설명](/assets/img/posts/파일명.png)`
- 임시 저장: 머리말에 `draft: true` 를 넣으면 목록에서 숨겨집니다.

## 배포

`main` 브랜치에 push하면 GitHub Actions(`.github/workflows/deploy.yml`)가 자동으로 빌드·배포합니다.
Settings → Pages → Source 가 **GitHub Actions** 로 되어 있어야 합니다.
