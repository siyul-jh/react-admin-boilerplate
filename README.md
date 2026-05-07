# react-admin-boilerplate

FSD v2.1 기반 React 어드민 보일러플레이트 — AI 개발 친화적 구조

## 특징

- **FSD v2.1** — 확장 가능한 Feature-Sliced Design 아키텍처
- **AI 친화적** — CLAUDE.md + .cursorrules로 AI가 바로 컨텍스트 파악
- **axios 인스턴스** — 토큰 자동 주입, Refresh 큐잉, 공통 에러 처리
- **RBAC** — 역할 기반 권한 관리 (admin / manager / viewer)
- **i18next** — 한국어/영어 다국어 지원
- **DevHelper** — 개발 환경 전용 토큰 디버깅 유틸
- **공통 컴포넌트** — Button, Input, Modal, Table, Toast, ConfirmDialog, ErrorBoundary

## 기술 스택

| 목적      | 선택                         |
| --------- | ---------------------------- |
| Framework | React 19 + TypeScript + Vite |
| 아키텍처  | FSD v2.1                     |
| 라우팅    | React Router v6              |
| 스타일    | Tailwind CSS v4              |
| 상태관리  | Zustand                      |
| 서버상태  | TanStack Query               |
| API       | axios + 커스텀 인스턴스      |
| 폼        | React Hook Form + Zod        |
| 다국어    | i18next (ko/en)              |
| 코드품질  | ESLint + Prettier + Husky    |

## 시작하기

```bash
# 설치
yarn install

# 환경변수 설정
cp .env.example .env.local

# 개발 서버
yarn dev
```

## 디렉토리 구조

```
src/
├── app/              # 앱 진입점, Provider, Router
├── pages/            # 라우트 단위 페이지
├── widgets/          # 복합 UI 블록 (Header, Sidebar, Layout)
├── features/         # 사용자 행동 단위 기능
├── entities/         # 도메인 모델
└── shared/
    ├── api/          # axios 인스턴스 + 인터셉터
    ├── config/       # RBAC 권한 설정
    ├── lib/          # 유틸, i18n, DevHelper, env 검증
    ├── model/        # 전역 Zustand 스토어
    ├── types/        # 공통 타입 정의
    └── ui/           # 공통 컴포넌트
```

## 인증 구조

```
accessToken  → 메모리 (Zustand)
refreshToken → httpOnly Cookie (프로덕션 / 서버 관리)
             → localStorage DevHelper (개발 환경만)
```

토큰 갱신은 axios 인터셉터에서 자동 처리되며, 동시 다발적 401 요청 시 큐잉으로 중복 갱신을 방지합니다.

## RBAC 권한 구조

| Role    | 권한                    |
| ------- | ----------------------- |
| admin   | 전체 권한               |
| manager | 읽기 + 쓰기 (삭제 제외) |
| viewer  | 읽기 전용               |

```typescript
import { hasPermission } from '@/shared/config'

if (hasPermission(user.role, 'user:write')) { ... }
```

## AI로 개발하기

`CLAUDE.md`와 `.cursorrules`에 프로젝트 컨텍스트가 정의되어 있습니다.
Claude Code, Cursor 등 AI 도구가 이 파일을 읽고 FSD 규칙에 맞게 코드를 생성합니다.

```bash
# Claude Code 시작
claude
```

# test
