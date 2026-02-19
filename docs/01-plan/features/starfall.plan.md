# Plan: STARFALL — 잔별 부원모집 웹사이트

> 작성일: 2026-02-19
> 상태: Draft
> 레벨: Starter (Single HTML)

---

## 1. 개요

중앙대학교 다빈치캠퍼스 천체관측 동아리 "잔별"의 26-1학기 신규부원 모집을 위한 몰입형 인터랙티브 웹사이트.

### 핵심 목표
- 스토리텔링 기반의 차별화된 부원모집 경험 제공
- 모바일 우선(90%) 최적화
- 부원 신청 + 별 유형 테스트 + Google Sheets 자동 저장

### 핵심 메시지
> 은하에서 별이 탄생 → 수만 광년을 여행 → 다빈치캠퍼스에 도착
> = "우연이 아닌 인연"

---

## 2. 제약 조건

| 항목 | 조건 |
|------|------|
| 스택 | Single HTML (Vanilla HTML/CSS/JS + Canvas API) |
| 외부 의존성 | 0개 (폰트 CDN + Google Fonts만 허용) |
| 배포 | Vercel 또는 Netlify (무료 플랜) |
| 데이터 저장 | Google Sheets + Apps Script |
| 타겟 디바이스 | 모바일 우선 (90%), 데스크톱 호환 |
| 커스텀 폰트 | KOTRA_LEAP.otf / .ttf (동봉) |
| 마감 | 03/11 (수) 이전 배포 필요 |

---

## 3. 기능 범위 (Scope)

### 3.1 씬 구조 (10개 파트)

| # | 씬 | 전환 방식 | 핵심 요소 |
|---|-----|-----------|-----------|
| P1 | 은하 탄생 | 자동 3초 | 300개 다색 파티클 소용돌이, 중앙 flash |
| P2 | 별의 여행 | 자동 3초 | 스피드라인 + 성운 blob + 밝은 별 |
| P3 | 도착 | 자동 3초 | 별똥별 대기권 진입, 다색 trail, 땅 실루엣 |
| S1 | 잔별 타이틀 | 스크롤 | "잔별" KOTRA LEAP, 별 가득 밤하늘 |
| S2-3 | 별똥별 → 초대장 | 자동+버튼 | 봉투 열림, 초대 카드, 수락 버튼 |
| S4 | 소개 + 폼 | 폼 제출 | 4개 활동 카드, 7필드 신청 폼 |
| S5 | 별 유형 퀴즈 | 자동 전환 | 6문항 4지선다, 프로그레스 바 |
| S5.5 | 로딩 | 2.5초 | 궤도 애니메이션, 백그라운드 Sheets 전송 |
| S6 | 결과 | 스크롤 | 유형 아이콘/이름/설명/배지 |
| S7 | 마무리 | 끝 | 가입 안내, 회비, 문의, 링크 복사 |

### 3.2 핵심 기능

1. **Canvas 별 렌더링 엔진**: 3가지 별 타입(원형/글로우/스파클), 다색, twinkle
2. **프롤로그 시퀀스**: 은하 탄생 → 별의 여행 → 도착 (각 3초 자동, 스킵 가능)
3. **씬 매니저**: 10개 씬 전환 (자동/수동/스크롤)
4. **부원 신청 폼**: 7필드, 유효성 검사, 연락처 자동 포매팅
5. **별 유형 테스트**: 6문항 4지선다, 선택지 랜덤 셔플, 4가지 유형
6. **결과 렌더링**: 유형별 아이콘/이름/설명/배지 표시
7. **Google Sheets 전송**: fetch POST (no-cors), 로딩 중 백그라운드 전송
8. **링크 복사**: 클립보드 API

### 3.3 별 유형 (4가지)

| 유형 | 아이콘 | 이름 | 설명 |
|------|--------|------|------|
| first | 🌙 | 첫별 | 별을 처음 만나는 당신 |
| yard | 🏡 | 마당별 | 편하게 별을 즐기는 당신 |
| explorer | 🚗 | 탐별러 | 별을 찾아 떠나는 당신 |
| obsessed | ✨ | 별에 미친 사람 | 별이 인생인 당신 |

---

## 4. 디자인 기준

- **스타일**: Kurzgesagt 2D (플랫, 선명, 기하학적, 글로우)
- **원칙**: 다채로운 색상 (모노톤 금지), 동화적/낭만적 감성
- **확정 시안**: `design-scenes-CONFIRMED.html` (시각적 기준)
- **컬러**: 핵심 3색 (시안 #4fc3f7, 퍼플 #7c4dff, 핑크 #ff4081) + 보조 8색
- **폰트**: KOTRA LEAP (제목), Pretendard (본문), Libre Baskerville (영문 장식)

---

## 5. 기술 아키텍처

### 모듈 구조 (Single HTML 내 논리적 분리)

| 모듈 | 담당 |
|------|------|
| `StarEngine` | Canvas 별 렌더링 (다색, 스파클, 성운, twinkle) |
| `PrologueSequence` | 프롤로그 3개 Canvas 씬 |
| `SceneManager` | 10개 씬 전환, IntersectionObserver |
| `FormHandler` | 폼 렌더링, 유효성 검사, 포매팅 |
| `QuizEngine` | 6문항 로직, 카드 전환, 점수 계산 |
| `ResultRenderer` | 로딩 애니메이션 → 결과 렌더링 |
| `DataPipeline` | fetch POST → Google Apps Script |
| `App.init()` | 전체 초기화, 이벤트 흐름, 전역 상태 |

### 전역 상태

```javascript
APP_STATE = {
  currentScene, formData, quizScores,
  quizAnswers, quizCurrentQ, resultType, submitted
}
```

---

## 6. 데이터 흐름

```
[브라우저] formData + quizResult
    ↓ fetch POST (JSON, mode: 'no-cors')
[Google Apps Script] doPost(e)
    ↓ sheet.appendRow()
[Google Sheets] "지원자" 시트 (A~K 컬럼)
```

시트 컬럼: 타임스탬프 | 학번 | 학부_전공 | 연락처 | 생년월일 | 운전가능 | 입금자명 | 희망활동 | 별유형 | 유형점수 | 퀴즈답변

---

## 7. 구현 우선순위

### Phase 1: 기반 구조
1. HTML 스켈레톤 + CSS 디자인 시스템 (변수, 컴포넌트)
2. Canvas StarEngine (별 렌더링 엔진)
3. 반응형 레이아웃 (모바일 우선)

### Phase 2: 프롤로그 + 타이틀
4. 프롤로그 3개 씬 (은하/여행/도착 Canvas)
5. Scene 1 타이틀 + 스크롤 힌트
6. SceneManager (자동/스크롤 전환)

### Phase 3: 초대장 + 폼
7. Scene 2-3 초대장 (봉투 열림, 카드)
8. Scene 4 소개 카드 + 신청 폼 (7필드, 유효성 검사)

### Phase 4: 퀴즈 + 결과
9. Scene 5 별 유형 테스트 (6문항, 셔플, 점수)
10. Scene 5.5 로딩 애니메이션
11. Scene 6 결과 렌더링

### Phase 5: 마무리 + 데이터
12. Scene 7 가입 안내/회비/문의/링크 복사
13. Google Sheets 전송 (DataPipeline)
14. 중복 제출 방지

### Phase 6: 최적화 + 배포
15. 모바일 Safari/Chrome 테스트
16. Canvas 성능 최적화 (모바일 150개 이하)
17. OG 메타태그, favicon
18. Vercel/Netlify 배포

---

## 8. 주의사항

1. 모바일 우선: 모든 CSS는 mobile-first, min-width 360px 기준
2. Canvas 성능: 모바일 별 150개 이하, `window.innerWidth < 768` 분기
3. 프롤로그 스킵: 터치/클릭 시 즉시 Scene 1로 이동
4. XSS 방지: 모든 입력값 `textContent`로 렌더링 (innerHTML 금지)
5. 폼 중복 제출: disabled + submitted 플래그
6. no-cors: Apps Script 응답 읽기 불가 → 전송 후 성공 처리
7. backdrop-filter: `@supports`로 fallback 처리
8. overscroll-behavior: none (당김 방지)

---

## 9. 배포 파일

```
index.html          ← 전체 통합 (HTML + CSS + JS)
KOTRA_LEAP.otf      ← 커스텀 폰트
KOTRA_LEAP.ttf      ← 커스텀 폰트 (호환)
```

---

## 10. 성공 기준

- [ ] 모든 10개 씬 정상 전환
- [ ] 프롤로그 자동 재생 + 스킵 동작
- [ ] 폼 유효성 검사 + 연락처 자동 포매팅
- [ ] 퀴즈 6문항 + 4유형 결과 정상 표시
- [ ] Google Sheets 데이터 수신 확인
- [ ] 모바일 Safari/Chrome 정상 동작
- [ ] 데스크톱 Chrome 정상 동작
- [ ] 60fps Canvas 애니메이션 (모바일)
- [ ] 링크 복사 기능 동작
