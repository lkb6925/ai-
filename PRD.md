# AI.DIR.KR 제품 요구사항 정의서 (PRD)

## 1. 프로젝트 개요 (Executive Summary)

### 1.1 목표
한국의 AI 초보자(학생, 직장인, 크리에이터)가 **자신에게 필요한 AI 도구를 가장 빠르고 직관적으로 찾을 수 있는 한국형 AI 큐레이션 플랫폼** 구축.

### 1.2 핵심 차별화(USP)
단순 해외 DB 번역이 아닌 아래 3가지를 중심으로 큐레이션:
- **한국어 성능**
- **목적(용도)**
- **가격(무료 여부)**

### 1.3 비전
초기 트래픽 확보 이후:
1. 제휴 마케팅(Affiliate)
2. 프리미엄 광고 슬롯 판매

을 통해 자동화 수익 구조를 빠르게 구축.

---

## 2. 핵심 기능 요구사항 (Functional Requirements)

## 2.1 하이브리드 검색 엔진 (Search Engine)

### 2.1.1 Alias(별칭) 지원 검색
- 영어 원문, 한국어 발음, 약칭을 모두 검색 대상으로 지원.
- 예시:
  - 검색어: `나노`
  - 검색어: `나노바나나`
  - 결과: `Nano Banana Pro`

### 2.1.2 다중 매핑 구조
- 하나의 도구가 여러 카테고리에 동시 소속 가능.
- 예시:
  - `Higgsfield` → `이미지`, `영상`

## 2.2 지능형 필터 및 태그 시스템 (Filter & Tags)

### 2.2.1 상단 대분류 탭
용도 중심의 탭 제공:
- 텍스트/업무
- 이미지/사진
- 영상/모션
- 코딩
- 음성/음악

### 2.2.2 무료 전용 토글 (Free-Only Switch)
- 클릭 한 번으로 **결제 없는 완전 무료 툴만 필터링**.
- 초보자 유입을 위한 핵심 기능으로 정의.

### 2.2.3 자동 가격 태그 로직
- `is_free_only = true` → `#완전무료` 자동 생성
- `is_free_only = false` → `#무료`(체험판), `#유료` 동시 생성

## 2.3 운영 자동화 시스템 (Admin & Automation)

### 2.3.1 New! 배지 타이머
- `created_at` 기준 등록 30일 이내 도구에 `[New!]` 배지 노출.
- 30일 경과 시 배지 자동 제거.

### 2.3.2 반자동 데이터 수집 (향후 고도화)
- Product Hunt 등 외부 RSS 수집.
- 관리자 대시보드에 `승인 대기` 상태로 적재.
- 관리자 승인 시 즉시 퍼블리싱.

---

## 3. 기술 스택 (Tech Stack)

- **Frontend**: Next.js(App Router), React, Tailwind CSS
- **Backend**: Next.js API Routes(Serverless)
- **Database**: Supabase(PostgreSQL)
- **Deployment**: Vercel
- **State Management**: Zustand 또는 React Context API

---

## 4. 데이터베이스 스키마 설계 (Data Schema)

개발팀이 즉시 테이블 생성 가능한 기준 스키마.

| 필드명 | 타입 | 필수 여부 | 설명 |
| --- | --- | --- | --- |
| `id` | UUID | Y | 고유 식별자 |
| `name` | String | Y | 도구 공식 명칭 (예: Nano Banana Pro) |
| `aliases` | Array[String] | N | 검색용 별칭 (예: ["나노바나나", "실사"]) |
| `categories` | Array[String] | Y | 대분류 매핑 (예: ["이미지", "영상"]) |
| `tags` | Array[String] | N | 특징 태그 (예: ["#한국어성능", "#초보자용"]) |
| `description` | Text | Y | 한 줄 요약 설명 |
| `is_free_only` | Boolean | Y | 완전 무료 여부 (`true`/`false`) |
| `affiliate_link` | String | Y | 제휴 또는 원본 링크 |
| `created_at` | Timestamp | Y | 등록일 (New 배지 계산용) |

---

## 5. 수익성 및 비즈니스 모델 (Monetization Strategy)

## 5.1 제휴 마케팅 (최우선)
- 각 도구의 CTA(바로가기) 버튼에 제휴 코드 삽입 링크 적용.
- 사용자 가입/결제 시 수수료 자동 정산 구조 설계.

## 5.2 프리미엄 광고 슬롯 (Featured Placement)
- 메인 상단 3개 카드를 광고 구좌로 운영.
- 트래픽 일정 수준 도달 시 주 단위 판매 모델 적용.

## 5.3 B2B 큐레이션 리포트 (추가 모델)
- 직군별 AI 업무 세팅 가이드를 전자책(PDF)으로 제작 및 판매.
- 타겟: 기업 실무자, 마케터, 교육 기관.

---

## 6. 실행 우선순위 (MVP 제안)

1. 검색 + Alias + 카테고리 탭
2. 무료 전용 토글 + 가격 태그 자동화
3. 제휴 링크 구조 내장
4. New! 배지 자동화
5. 관리자 승인 기반 데이터 운영

