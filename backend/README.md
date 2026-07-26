---
title: KOOK Backend
emoji: 🍲
colorFrom: green
colorTo: gray
sdk: docker
app_port: 7860
pinned: false
short_description: 투석환자 맞춤 AI 식단 생성 API (FastAPI + TensorFlow)
---

# KOOK 백엔드 API

투석 환자를 위한 한 끼 식단을 생성·조정하는 API 서버입니다.
프론트엔드(React)는 별도로 Vercel에 배포되어 있고, 이 Space는 API만 제공합니다.

## 주요 엔드포인트

| 경로 | 설명 |
|---|---|
| `GET /health` | 서버·DB 상태 확인 |
| `GET /menus`, `/ingredients` | 메뉴·재료 목록 |
| `POST /generate` | 한 끼 식단 생성 (AI 엔진 + 영양 레버) |
| `POST /generate_day` | 하루 세 끼 연속 생성 |
| `POST /recipe` | 조리법 LLM 편집 |
| `POST /auth/signup`, `/auth/login` | 회원 기능 (Neon Postgres) |

전체 스펙은 서버 실행 후 `/docs` 에서 확인할 수 있습니다.

## 구성

- **식단 생성**: KLUE-BERT 기반 시퀀스 생성 모델 + 칼륨·인·나트륨 조정 레버
- **영양 기준**: 대한신장학회 투석환자 영양관리 지침 기반
- **DB**: Neon Postgres (회원·저장 식단·즐겨찾기)

## 환경변수 (Space Settings → Variables and secrets)

| 이름 | 필수 | 설명 |
|---|---|---|
| `DATABASE_URL` | ✅ | Neon Postgres 접속 문자열 |
| `CORS_ORIGINS` | ✅ | 허용할 프론트엔드 주소 (쉼표 구분) |
| `OPENAI_API_KEY` | 선택 | `/recipe`, `/tts` 에서만 사용 |

> 메모리 사용량은 TensorFlow 모델 상주 기준 약 470MB입니다.
