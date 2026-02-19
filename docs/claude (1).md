# 🌠 STARFALL — 잔별 부원모집 웹사이트

> 중앙대학교 다빈치캠퍼스 천체관측 동아리 "잔별" 26-1학기 신규부원 모집
> 몰입형 인터랙티브 웹 경험을 통한 차별화된 모집 페이지

---

## 📋 프로젝트 제약

| 항목 | 조건 |
|------|------|
| 스택 | **Single HTML** (Vanilla HTML/CSS/JS + Canvas API) |
| 외부 의존성 | **0개** (폰트 CDN + Google Fonts만 사용) |
| 배포 | Vercel 또는 Netlify (무료 플랜) |
| 데이터 저장 | Google Sheets + Apps Script |
| 타겟 디바이스 | **모바일 우선 (90%)**, 데스크톱 호환 |
| 커스텀 폰트 | KOTRA_LEAP.otf / .ttf (같은 폴더에 동봉) |

---

## 🎭 스토리텔링 콘셉트

### 핵심 메시지 (말로 하지 않고, 비주얼로만 전달)

> 먼 우주 은하에서 하나의 별이 탄생
> → 수만 광년을 가로질러 여행
> → 다빈치캠퍼스에 도착
> = 다양한 지역에서 온 학생들이 이곳에 모인 것
> = **"우연이 아닌 인연"**

---

## 🎬 씬 구조 (프롤로그 3 + 본편 7 = 총 10개 파트)

```
PROLOGUE 1  은하 탄생 ─── (자동 3초) ───▶
PROLOGUE 2  별의 여행 ─── (자동 3초) ───▶
PROLOGUE 3  도착 ──────── (자동 3초) ───▶
SCENE 1     잔별 타이틀 ── (스크롤) ────▶
SCENE 2→3   별똥별 → 초대장 (자동+버튼) ▶
SCENE 4     소개 + 폼 ─── (폼 제출) ───▶
SCENE 5     퀴즈 6문항 ── (자동 전환) ──▶
SCENE 5.5   로딩 ──────── (2.5초) ─────▶
SCENE 6     결과 ──────── (스크롤) ────▶
SCENE 7     마무리 ────── (끝)
```

### 각 씬 상세

#### PROLOGUE 1: 은하 탄생 (Galaxy Birth)
- **Canvas**: 300개 다색 파티클이 중심을 기준으로 소용돌이치며 회전
- **중앙**: 밝은 빛 (별 탄생 flash)
- **하단 텍스트**: "138억 년 전, 먼 우주 어딘가에서 하나의 별이 태어났습니다"
- **전환**: 3초 후 자동 (스킵 가능)
- **참고**: reference-images/ref-05, ref-10

#### PROLOGUE 2: 별의 여행 (Star Journey)
- **Canvas**: 수직 스피드라인 + 성운 blob 통과 + 중앙에 밝은 ✦ 별
- **효과**: 별 주위로 성운 색이 스쳐지나감
- **하단 텍스트**: "수만 광년을 가로질러 수많은 은하와 성운을 지나 당신을 향해 날아갑니다"
- **전환**: 3초 후 자동
- **참고**: reference-images/ref-08, ref-11

#### PROLOGUE 3: 도착 (Arrival)
- **Canvas**: 밤하늘 + 대기권 진입 별똥별 (다색 trail: 흰→시안→퍼플→핑크→오렌지)
- **하단**: 땅 실루엣 (언덕/산 곡선)
- **하단 텍스트**: "그건 우연이 아닌 인연이었습니다"
- **전환**: 3초 후 자동

#### SCENE 1: 잔별 타이틀
- **"잔별"** KOTRA LEAP, #ffffff, fadeIn
- **"천체관측 동아리"** Pretendard, rgba(255,255,255,.3), fadeIn (0.7s 딜레이)
- **SCROLL 힌트** + 화살표 bounce
- **배경**: 별 가득한 밤하늘 (Kurzgesagt 스타일)

#### SCENE 2→3: 별똥별 → 초대장
- 별똥별이 우상단 → 초대장 위치로 낙하
- 도착 시 flash 효과
- 봉투 열림 (CSS rotateX) → 편지 카드 슬라이드업
- 카드: 다색 글로우 테두리 + 코너 L자 장식
- **"당신을 잔별에 초대합니다"**
- **"초대 수락하기 ✦"** 버튼

#### SCENE 4: 소개 + 부원 신청 폼
- 잔별 소개 + 4 활동 카드 (2×2 grid)
- 부원 신청 폼 (7필드)
- **"나의 별 유형 알아보기 ✦"** 버튼 → 유효성 검사 후 퀴즈 전환

#### SCENE 5: 별 유형 테스트
- 프로그레스 바 (시안→퍼플→핑크 그라데이션)
- ✦ 별 인디케이터 6개
- 한 화면 1문항, 4지선다
- 터치 → 0.3초 하이라이트 → 카드 슬라이드 전환
- 선택지 순서 매번 랜덤 셔플

#### SCENE 5.5: 로딩
- "당신의 별자리를 읽는 중..." (pulse 애니메이션)
- 이중 궤도 회전 (핑크 + 시안 포인트)
- **이 동안 백그라운드에서 Google Sheets 전송**
- 2.5초 후 결과 전환

#### SCENE 6: 결과
- 유형 아이콘 + 이름 (KOTRA LEAP) + 설명
- 배정 배지
- 아래로 스크롤 → 마무리 연결

#### SCENE 7: 마무리
- 가입 안내 카드: "가입폼 작성 후 회비 입금 → 단톡방 초대"
- 회비 카드: 신입 30,000원 / 기존 20,000원
- 문의 카드: 오유택 010-0000-0000 / 김운정 010-4816-6181
- 📅 신청 마감: 03/11 (수)
- **"링크 복사하기"** 버튼 (시안→퍼플→핑크 그라데이션)
- **"처음으로 돌아가기"** 고스트 버튼
- "우리의 밤하늘에서 만나요 ✨"

---

## 🎨 디자인 시스템 — Kurzgesagt 2D

### 확정 디자인 시안
`design-scenes-CONFIRMED.html` — 이 파일이 시각적 기준입니다.
KOTRA_LEAP 폰트와 같은 폴더에서 브라우저로 열면 전체 씬 미리보기 가능.

### 핵심 원칙
1. **Kurzgesagt**: 플랫 2D, 선명한 색, 기하학적 도형, 글로우
2. **다채로운**: 모노톤 절대 금지. 별마다 분홍/노랑/민트/라벤더/코랄 등 다양
3. **동화적**: 낭만적이고 따뜻한 감성. 차가운 UI 느낌 X
4. **스토리텔링**: 비주얼로 인연의 서사를 전달

### 컬러 팔레트

```css
:root {
  /* ── 핵심 3색 (버튼, 프로그레스, 강조) ── */
  --kurz-cyan:      #4fc3f7;
  --kurz-purple:    #7c4dff;
  --kurz-pink:      #ff4081;

  /* ── 보조 색상 (별, 파티클, 장식) ── */
  --kurz-orange:    #ff9100;
  --kurz-yellow:    #ffea00;
  --kurz-mint:      #64ffda;
  --kurz-coral:     #ff6e6e;
  --kurz-lavender:  #b388ff;
  --kurz-peach:     #ffab91;
  --kurz-cyan2:     #00e5ff;
  --kurz-white:     #ffffff;

  /* ── 배경 그라데이션 ── */
  --bg-1: #02040c;
  --bg-2: #04060e;
  --bg-3: #081428;
  --bg-4: #0c1e38;
  --bg-5: #061020;

  /* ── 텍스트 ── */
  --text-title:     #ffffff;
  --text-body:      rgba(255,255,255,.85);
  --text-sub:       rgba(255,255,255,.45);
  --text-faint:     rgba(255,255,255,.2);

  /* ── 카드/UI ── */
  --card-bg:        rgba(100,140,255,.03);
  --card-border:    rgba(100,140,255,.06);
  --card-bg-hover:  rgba(100,140,255,.06);
}
```

### 별 파티클 색상 배열 (Canvas에서 사용)

```javascript
const STAR_COLORS = [
  '#4fc3f7', '#7c4dff', '#ff4081', '#ff9100',
  '#ffea00', '#64ffda', '#ff6e6e', '#b388ff',
  '#ffab91', '#00e5ff', '#ffffff'
];
```

### 타이포그래피

| 용도 | 폰트 | 굵기 | 크기 | 색상 |
|------|------|------|------|------|
| 제목 "잔별" | KOTRA LEAP | normal | clamp(2.4rem,9vw,3.4rem) | #ffffff |
| 결과 유형명 | KOTRA LEAP | normal | clamp(1.6rem,6vw,2.2rem) | #ffffff |
| 영문 장식 | Libre Baskerville | 400/italic | 0.48~0.58rem | rgba(255,180,140,.4) |
| 본문 | Pretendard | 300 | 0.78~0.88rem | rgba(255,255,255,.85) |
| 강조 | Pretendard | 400 | same | #ffffff |
| 서브텍스트 | Pretendard | 300 | 0.55~0.68rem | rgba(255,255,255,.45) |

```css
@font-face {
  font-family: 'KOTRA LEAP';
  src: url('KOTRA_LEAP.otf') format('opentype'),
       url('KOTRA_LEAP.ttf') format('truetype');
  font-weight: normal;
  font-style: normal;
  font-display: swap;
}
```

### 폰트 CDN

```html
<!-- Pretendard -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/orioncactus/pretendard/dist/web/static/pretendard.min.css">
<!-- Libre Baskerville -->
<link href="https://fonts.googleapis.com/css2?family=Libre+Baskerville:ital,wght@0,400;0,700;1,400&display=swap" rel="stylesheet">
```

### 별 표현 — 3가지 타입

| 타입 | 비율 | 크기 | 특징 |
|------|------|------|------|
| 원형 별 | 80% | 0.3~1.2px | 단순 원, 다양한 색, twinkle |
| 글로우 별 | 14% | 1~2.5px | 원 + radialGradient glow |
| ✦ 스파클 별 | 6% | 4~11px | 4각 다이아몬드, Kurzgesagt 시그니처 |

### Canvas 별 렌더링 사양

```
별 개수: 모바일 150개, 데스크톱 250개
Twinkle: 각 별 sin(t * speed + phase), 개별 주기
성운 blob: 3~5개 radialGradient, 다른 색 (cyan/purple/pink), opacity 0.02~0.04
배경: linear-gradient 딥 네이비-인디고
프레임: requestAnimationFrame, 60fps 목표
반응형: ResizeObserver
```

### ✦ 4각 다이아몬드 스파클 그리기

```javascript
function draw4Star(ctx, x, y, size, color, alpha) {
  ctx.save();
  ctx.globalAlpha = alpha;
  ctx.fillStyle = color;
  ctx.beginPath();
  const inn = size * 0.2;
  for (let i = 0; i < 4; i++) {
    const a = (i * Math.PI / 2) - Math.PI / 2;
    const na = a + Math.PI / 4;
    if (i === 0) ctx.moveTo(x + Math.cos(a) * size, y + Math.sin(a) * size);
    else ctx.lineTo(x + Math.cos(a) * size, y + Math.sin(a) * size);
    ctx.lineTo(x + Math.cos(na) * inn, y + Math.sin(na) * inn);
  }
  ctx.closePath();
  ctx.fill();
  // Glow
  const [r, g, b] = hexToRgb(color);
  const gl = ctx.createRadialGradient(x, y, 0, x, y, size * 2);
  gl.addColorStop(0, `rgba(${r},${g},${b},${alpha * 0.2})`);
  gl.addColorStop(1, 'transparent');
  ctx.globalAlpha = alpha * 0.5;
  ctx.fillStyle = gl;
  ctx.beginPath();
  ctx.arc(x, y, size * 2, 0, Math.PI * 2);
  ctx.fill();
  ctx.restore();
}
```

### 초대장 카드 스펙

```
[외부 래퍼]
padding: 1.5px (border 두께)
border-radius: 6px
background: 4색 gradient shimmer (핑크→시안→퍼플→골드, 300% size, 5s cycle)
box-shadow: 퍼플 glow + 핑크 glow

[4 코너 L자 장식]
각 코너 다른 색 (핑크, 시안, 퍼플, 골드)
10px × 1px

[내부]
background: linear-gradient(165deg, rgba(10,14,30,.95), rgba(6,10,24,.97))
border-radius: 5px
```

### 버튼 스타일

```css
/* Primary (CTA) */
.btn-primary {
  background: linear-gradient(135deg, #4fc3f7, #7c4dff, #ff4081);
  color: #ffffff;
  border: none;
  border-radius: 20px;
  font-weight: 500;
  box-shadow: 0 4px 16px rgba(120, 80, 255, .2);
}

/* Ghost */
.btn-ghost {
  background: transparent;
  color: rgba(255,255,255,.3);
  border: 1px solid rgba(100,140,255,.1);
  border-radius: 20px;
}

/* Accept (초대장) */
.btn-accept {
  background: rgba(100,180,255,.04);
  color: rgba(255,255,255,.5);
  border: 1px solid rgba(100,180,255,.15);
  border-radius: 20px;
}
```

---

## 📝 폼 필드 사양

### 필드 목록

| # | 필드명 | key | type | 필수 | 검증 | placeholder |
|---|--------|-----|------|------|------|-------------|
| 1 | 학번 | studentId | text | ✅ | 4자리+ 숫자 | 20251234 |
| 2 | 학부, 전공 | major | text | ✅ | 2자+ | 소프트웨어학부 |
| 3 | 연락처 | phone | tel | ✅ | 010-XXXX-XXXX | 010-0000-0000 |
| 4 | 생년월일 | birthday | text | ✅ | 6자리 숫자 | 030415 |
| 5 | 운전 가능 여부 | canDrive | radio | ✅ | 하나 선택 | 가능 / 불가능 |
| 6 | 입금자 명 | depositor | text | ✅ | 2자+ | 홍길동 |
| 7 | 기타 희망 활동 | wishActivity | textarea | ❌ | - | 자유 작성 |

### 연락처 자동 포매팅

```javascript
function formatPhone(val) {
  const nums = val.replace(/\D/g, '');
  if (nums.length <= 3) return nums;
  if (nums.length <= 7) return nums.slice(0, 3) + '-' + nums.slice(3);
  return nums.slice(0, 3) + '-' + nums.slice(3, 7) + '-' + nums.slice(7, 11);
}
```

### 유효성 검사

```javascript
function validateForm(data) {
  const errors = [];
  if (!/^\d{4,}$/.test(data.studentId))
    errors.push({ field: 'studentId', msg: '학번을 입력해주세요' });
  if (!data.major || data.major.length < 2)
    errors.push({ field: 'major', msg: '학부/전공을 입력해주세요' });
  if (!/^010-\d{4}-\d{4}$/.test(data.phone))
    errors.push({ field: 'phone', msg: '올바른 연락처를 입력해주세요' });
  if (!/^\d{6}$/.test(data.birthday))
    errors.push({ field: 'birthday', msg: '생년월일 6자리를 입력해주세요' });
  if (!data.canDrive)
    errors.push({ field: 'canDrive', msg: '선택해주세요' });
  if (!data.depositor || data.depositor.length < 2)
    errors.push({ field: 'depositor', msg: '입금자 명을 입력해주세요' });
  return errors;
}
```

---

## ⭐ 별 유형 테스트 — 완전 데이터

### 4가지 유형

```javascript
const STAR_TYPES = {
  first: {
    icon: '🌙',
    name: '첫별',
    subtitle: '별을 처음 만나는 당신',
    description: '아직 별을 자세히 본 적은 없지만,\n밤하늘을 올려다보는 순간의 설렘을\n누구보다 순수하게 느끼는 사람.\n잔별이 당신의 첫 번째 별이 되어줄게요.',
    badge: '🌙 첫별 · 새로운 시작'
  },
  yard: {
    icon: '🏡',
    name: '마당별',
    subtitle: '편하게 별을 즐기는 당신',
    description: '거창한 장비 없이도\n일상 속에서 하늘을 올려다보는 여유.\n함께하는 사람들과의 시간이\n별보다 빛나는 걸 아는 사람.',
    badge: '🏡 마당별 · 함께하는 밤하늘'
  },
  explorer: {
    icon: '🚗',
    name: '탐별러',
    subtitle: '별을 찾아 떠나는 당신',
    description: '좋은 관측지를 찾아 차를 몰고,\n광해 없는 깊은 산속까지 찾아가는 열정.\n당신에겐 별이 여행의 이유이자\n목적지입니다.',
    badge: '🚗 탐별러 · 별을 찾아 떠나는 자'
  },
  obsessed: {
    icon: '✨',
    name: '별에 미친 사람',
    subtitle: '별이 인생인 당신',
    description: '장비 스펙을 외우고,\n천체 카탈로그를 읽으며,\nISO와 노출 시간을 계산하는 당신.\n잔별은 당신 같은 사람을 기다렸어요.',
    badge: '✨ 별에 미친 사람 · 이 길의 끝'
  }
};
```

### 6문항 전체 데이터

```javascript
const QUIZ_DATA = [
  {
    id: 1,
    question: '밤에 하늘을 올려다본 적 있나요?',
    options: [
      { text: '솔직히 별로 올려다본 적 없어요', type: 'first' },
      { text: '가끔 달이 예쁠 때?', type: 'yard' },
      { text: '맑은 날이면 습관처럼 올려다봐요', type: 'explorer' },
      { text: '오늘 밤 투명도 몇인지 이미 확인했어요', type: 'obsessed' }
    ]
  },
  {
    id: 2,
    question: '친구가 "별 보러 가자" 하면?',
    options: [
      { text: '별 보러 간다는 게 뭔데? 재밌겠다!', type: 'first' },
      { text: '좋지~ 돗자리 깔고 치킨 시키자', type: 'yard' },
      { text: '어디로 갈지 내가 알아볼게, 광해지도 켜봐', type: 'explorer' },
      { text: '장비 뭐 가져갈지 리스트 보내줄게', type: 'obsessed' }
    ]
  },
  {
    id: 3,
    question: '"별자리 앱" 하면 떠오르는 생각은?',
    options: [
      { text: '별자리 앱이 있어? 깔아봐야지', type: 'first' },
      { text: '가끔 하늘에 폰 들이대면 재밌더라', type: 'yard' },
      { text: '관측 전 미리 뭐가 보일지 확인하는 용도', type: 'explorer' },
      { text: '이미 3개 이상 깔려있는데?', type: 'obsessed' }
    ]
  },
  {
    id: 4,
    question: '이런 장비, 들어본 적 있나요? "적도의"',
    options: [
      { text: '적도의? 적도 근처에서 쓰는 건가?', type: 'first' },
      { text: '들어본 것 같긴 한데... 망원경 관련?', type: 'yard' },
      { text: '알죠, 천체 추적할 때 쓰는 거', type: 'explorer' },
      { text: 'EQ6 쓰는데 가이드 캘리 좀 알려줄까?', type: 'obsessed' }
    ]
  },
  {
    id: 5,
    question: '가장 끌리는 동아리 활동은?',
    options: [
      { text: '별 보면서 이야기하는 거 자체가 좋을 것 같아요', type: 'first' },
      { text: 'MT나 번개 관측이요! 분위기가 좋을 것 같아', type: 'yard' },
      { text: '관측 원정이요. 먼 곳에서 보는 별이 진짜잖아요', type: 'explorer' },
      { text: '학술회요. 천체물리 토론 하고 싶어요', type: 'obsessed' }
    ]
  },
  {
    id: 6,
    question: '밤하늘에서 가장 보고 싶은 건?',
    options: [
      { text: '별똥별! 소원 빌고 싶어요', type: 'first' },
      { text: '보름달이나 예쁜 별자리', type: 'yard' },
      { text: '은하수. 직접 눈으로 보고 싶어요', type: 'explorer' },
      { text: '안드로메다 은하 M31의 나선팔 구조', type: 'obsessed' }
    ]
  }
];
```

### 점수 계산

```javascript
const scores = { first: 0, yard: 0, explorer: 0, obsessed: 0 };
const answers = []; // 각 문항 선택한 type 기록

function onAnswer(questionIndex, selectedType) {
  scores[selectedType] += 1;
  answers.push(selectedType);
}

function getResult() {
  const sorted = Object.entries(scores).sort((a, b) => b[1] - a[1]);

  // 동점 처리: 마지막 답변 유형 우선
  if (sorted[0][1] === sorted[1][1]) {
    const lastAnswer = answers[answers.length - 1];
    const tied = sorted.filter(s => s[1] === sorted[0][1]);
    const found = tied.find(s => s[0] === lastAnswer);
    if (found) return found[0];
  }

  return sorted[0][0];
}
```

### 선택지 셔플

```javascript
function shuffleOptions(options) {
  const shuffled = [...options];
  for (let i = shuffled.length - 1; i > 0; i--) {
    const j = Math.floor(Math.random() * (i + 1));
    [shuffled[i], shuffled[j]] = [shuffled[j], shuffled[i]];
  }
  return shuffled;
}
```

---

## 🗄️ 데이터 저장 — Google Sheets

### 전체 흐름

```
[브라우저] formData + quizResult
    │
    ▼  fetch POST (JSON, mode: 'no-cors')
    │
[Google Apps Script] doPost(e)
    │
    ▼  sheet.appendRow()
    │
[Google Sheets] "지원자" 시트에 행 추가
    │
    ▼
[동아리 임원] 시트에서 확인
```

### 시트 컬럼 (A~K)

| 컬럼 | 필드 | 예시 |
|------|------|------|
| A | 타임스탬프 | 2026-03-05 14:23:01 |
| B | 학번 | 20251234 |
| C | 학부_전공 | 소프트웨어학부 |
| D | 연락처 | 010-1234-5678 |
| E | 생년월일 | 030415 |
| F | 운전가능 | 가능 |
| G | 입금자명 | 홍길동 |
| H | 희망활동 | 사진촬영도 하고 싶어요 |
| I | 별유형 | 탐별러 |
| J | 유형점수 | first:1,yard:1,explorer:3,obsessed:1 |
| K | 퀴즈답변 | first,yard,explorer,explorer,explorer,obsessed |

### Google Apps Script 코드

```javascript
function doPost(e) {
  try {
    const sheet = SpreadsheetApp.getActiveSpreadsheet()
                   .getSheetByName('지원자');
    const data = JSON.parse(e.postData.contents);

    sheet.appendRow([
      new Date(),
      data.studentId,
      data.major,
      data.phone,
      data.birthday,
      data.canDrive,
      data.depositor,
      data.wishActivity || '',
      data.starType,
      data.typeScores,
      data.quizAnswers
    ]);

    return ContentService
      .createTextOutput(JSON.stringify({ result: 'success' }))
      .setMimeType(ContentService.MimeType.JSON);
  } catch (error) {
    return ContentService
      .createTextOutput(JSON.stringify({ result: 'error', message: error.toString() }))
      .setMimeType(ContentService.MimeType.JSON);
  }
}
```

### 프론트엔드 전송 코드

```javascript
async function submitToSheets(formData, quizResult) {
  const SCRIPT_URL = '{{APPS_SCRIPT_URL}}'; // 배포 후 교체

  const payload = {
    studentId:    formData.studentId,
    major:        formData.major,
    phone:        formData.phone,
    birthday:     formData.birthday,
    canDrive:     formData.canDrive,
    depositor:    formData.depositor,
    wishActivity: formData.wishActivity,
    starType:     quizResult.typeName,
    typeScores:   Object.entries(quizResult.scores).map(([k,v]) => `${k}:${v}`).join(','),
    quizAnswers:  quizResult.answers.join(',')
  };

  try {
    await fetch(SCRIPT_URL, {
      method: 'POST',
      mode: 'no-cors',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify(payload)
    });
  } catch (err) {
    console.error('Submit error:', err);
  }
}
```

### 전송 타이밍

```
SCENE 4: 폼 작성 → formData를 전역 변수에 저장
SCENE 5: 퀴즈 → scores/answers를 전역 변수에 저장
SCENE 5.5: 로딩 화면 진입 시 → formData + quizResult 합쳐서 POST 전송
SCENE 6: 결과 표시 (이미 전송 완료)
```

---

## 🎼 에이전트 오케스트라 (개발 모듈 구조)

Single HTML이지만, 코드를 논리적 모듈로 분리하여 개발합니다.

| 파트 | 모듈 | 담당 영역 |
|------|------|-----------|
| 🎻 1st Violin | `StarEngine` | Canvas 별 렌더링 (다색, ✦ 스파클, blob 성운, twinkle) |
| 🎻 2nd Violin | `PrologueSequence` | 은하 탄생 / 별의 여행 / 도착 — 3개 Canvas 씬 |
| 🎵 Viola | `SceneManager` | 10개 씬 전환 (자동/수동/스크롤), IntersectionObserver |
| 🎵 Cello | `FormHandler` | 폼 렌더링, 유효성 검사, 연락처 포매팅, formData 수집 |
| 🎺 Trumpet | `QuizEngine` | 6문항 로직, 카드 전환, 점수 계산, 셔플 |
| 🎺 Horn | `ResultRenderer` | 로딩 애니메이션 → 결과 유형 렌더링 |
| 🥁 Percussion | `DataPipeline` | fetch POST → Google Apps Script |
| 🎹 Piano | CSS Variables | 디자인 시스템, 컴포넌트, 반응형 |
| 🎼 Conductor | `App.init()` | 전체 초기화, 이벤트 흐름, 전역 상태 |

### 전역 상태

```javascript
const APP_STATE = {
  currentScene: 0,        // 0~9 (프롤로그 0~2, 본편 3~9)
  formData: null,          // SCENE 4에서 수집
  quizScores: { first: 0, yard: 0, explorer: 0, obsessed: 0 },
  quizAnswers: [],         // 각 문항 선택 type
  quizCurrentQ: 0,         // 0~5
  resultType: null,        // 'first'|'yard'|'explorer'|'obsessed'
  submitted: false         // 중복 제출 방지
};
```

---

## 📁 최종 파일 구조

```
/project-root/
├── index.html              ← 전체 통합 (HTML + CSS + JS)
├── KOTRA_LEAP.otf          ← 커스텀 폰트
├── KOTRA_LEAP.ttf          ← 커스텀 폰트 (호환)
├── design-scenes-CONFIRMED.html  ← 디자인 시안 (개발 참고용)
├── reference-images/       ← 레퍼런스 (개발 참고용)
│   ├── ref-01 ~ ref-11.png
└── claude.md               ← 이 문서 (프로젝트 기준)
```

배포 시 업로드: `index.html` + `KOTRA_LEAP.otf` + `KOTRA_LEAP.ttf` (3개 파일만)

---

## 🚀 배포 체크리스트

- [ ] KOTRA_LEAP.otf/ttf index.html과 같은 폴더
- [ ] Google Sheets 생성 + "지원자" 시트 이름 확인
- [ ] Apps Script 배포 → URL을 index.html의 `SCRIPT_URL`에 입력
- [ ] OG 메타태그 (카카오톡/인스타 공유 시 미리보기)
- [ ] favicon
- [ ] 모바일 Safari/Chrome 테스트
- [ ] 데스크톱 Chrome 테스트
- [ ] 폼 제출 → Sheets 수신 확인
- [ ] 프롤로그 스킵 동작 확인
- [ ] HTTPS 확인

---

## ⚠️ 개발 시 주의사항

1. **모바일 우선**: 모든 CSS는 mobile-first, min-width 360px 기준
2. **Canvas 성능**: 모바일 별 150개 이하, `window.innerWidth < 768` 분기
3. **프롤로그 스킵**: 터치/클릭 시 즉시 Scene 1로 이동 가능하게
4. **자동 스크롤**: `scrollIntoView({ behavior: 'smooth' })`, iOS Safari 확인
5. **backdrop-filter**: `@supports`로 fallback 배경색 처리
6. **폰트 로딩**: `font-display: swap` (FOUT 허용)
7. **폼 중복 제출**: `submitBtn.disabled = true` + `APP_STATE.submitted` 플래그
8. **overscroll**: `overscroll-behavior: none` (당김 방지)
9. **XSS**: 모든 입력값 `textContent`로 렌더링 (innerHTML 금지)
10. **no-cors**: Apps Script 응답 읽기 불가 → 전송 후 무조건 성공 처리
