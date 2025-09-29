# 디자인 의도 설명서
## "추억의 재구성" 성률 작가 개인전 온라인 전시회

---

## 1. 공간 연출 (레이아웃)

### 관람객이 작품에 온전히 집중할 수 있는 공간 연출

**1. 자동 순환 캐러셀을 통한 시각적 임팩트**

최상단에 배치한 **5개 작품 자동 순환 캐러셀**을 통해 강력한 첫인상을 제공합니다.

- **중앙-좌우-숨김 구조의 3단계 레이어링**: 중앙 이미지는 100% opacity와 scale(1), 좌우 이미지는 60% opacity와 scale(0.8), 가장 외곽 이미지는 30% opacity와 scale(0.6)으로 자연스러운 깊이감과 공간감을 연출
- **4초 간격 자동 순환**: 각 작품이 충분히 감상될 수 있도록 4초씩 머무르며, 20초 주기로 부드럽게 순환
- **원근감 표현**: `perspective: 1200px`와 `transform3d`를 활용하여 이미지들이 실제 공간에 떠있는 듯한 입체적 느낌 구현

**2. 5가지 독창적 레이아웃으로 다양한 관람 경험 제공**

각 작품마다 고유한 레이아웃을 적용하여 단조로움을 피하고 시각적 흥미를 유지합니다:

```css
/* 1번 작품: 좌우 분할 */
.artwork:nth-child(1) figure {
    display: grid;
    grid-template-columns: 45% 55%; /* 이미지 왼쪽, 텍스트 오른쪽 */
}

/* 2번 작품: 컴팩트 카드 */
.artwork:nth-child(2) {
    max-width: 600px;
    margin-left: auto; /* 우측 정렬로 시각적 리듬 */
}

/* 3번 작품: 역순 분할 */
.artwork:nth-child(3) figure {
    grid-template-columns: 55% 45%; /* 텍스트 왼쪽, 이미지 오른쪽 */
}

/* 4번 작품: 오버레이 */
.artwork:nth-child(4) figcaption {
    position: absolute;
    background: linear-gradient(transparent, rgba(0,0,0,0.7)); /* 그라데이션 오버레이 */
}

/* 5번 작품: 중앙 원형 */
.artwork:nth-child(5) {
    display: flex;
    flex-direction: column;
    align-items: center; /* 원형 이미지 중앙 배치 */
}
```

**3. 반응형 디자인 고려사항**

**4단계 적응형 구조**:
- **Desktop (1200px+)**: 캐러셀 500px × 500px, 다양한 레이아웃 완전 구현
- **Tablet (768px-1199px)**: 캐러셀 400px × 400px, 레이아웃 비율 조정
- **Mobile (767px 이하)**: 모든 작품을 세로 레이아웃으로 통일, 캐러셀 280px × 280px
- **Large Desktop (1600px+)**: 캐러셀 600px × 600px로 확장

**집중도 우선 설계**: 작은 화면일수록 불필요한 요소를 제거하여 핵심 콘텐츠에 집중

---

## 2. 전시의 무드 (스타일)

### 선택한 색상 팔레트와 의도

**"그늘과 햇빛"을 테마로 한 따뜻한 수채화 팔레트**:

```css
:root {
  /* 따뜻한 베이지/크림 계열 - 햇살의 온기 */
  --warm-cream: #FFF8F0;
  --soft-beige: #F5EFE7;
  --light-peach: #FAF0E6;

  /* 부드러운 브라운 계열 - 그늘의 편안함 */
  --soft-brown: #A8937F;
  --medium-brown: #8B7355;
  --deep-brown: #6B5D52;

  /* 포인트 컬러 - 추억의 온기 */
  --warm-terracotta: #D4A373;
  --sunset-peach: #F4D5C3;
}
```

**의도**:
- **크림/베이지 베이스**: 작가의 "그늘 속 편안함" 철학을 반영한 부드럽고 안온한 배경
- **브라운 계열 텍스트**: "뜨겁지 않은 서늘함"을 표현하는 차분한 색조
- **테라코타/피치 액센트**: 추억 속 따뜻한 순간들을 상징하는 포인트 색상
- **수채화 효과**: 여러 색상의 radial-gradient 중첩으로 작가의 감성적 작품 세계를 디지털로 표현

### 글꼴 선택의 이유

**감성과 가독성을 모두 고려한 이중 폰트 시스템**:

```css
/* 제목과 작가명: 나눔명조 (전통적 감성) */
h1, h2, h3, .artist-name {
    font-family: 'Nanum Myeongjo', serif;
    font-weight: 700;
}

/* 본문: Noto Sans KR (현대적 가독성) */
body {
    font-family: 'Noto Sans KR', sans-serif;
    font-weight: 400;
}
```

**선택 이유**:
- **나눔명조**: 한국적 정서와 전통적 아름다움을 간직한 서체로, "추억의 재구성"이라는 주제와 완벽히 부합
- **작가명 강조**: `.artist-name` 클래스로 성률 작가의 이름을 명조체로 돋보이게 표현
- **Noto Sans KR**: 작품 설명과 작가 인용문의 가독성을 위한 선택
- **가중치 조절**: 제목 700, 본문 400, 부가정보 300으로 정보의 위계질서 명확화

### 여백과 간격을 통한 감정 전달

**"여유로운 사색"을 위한 공간 설계**:

```css
/* 섹션 간 충분한 호흡 공간 */
.carousel-section { padding: 5rem 2rem 4rem; }
.artwork { margin-bottom: 6rem; }

/* 내부 요소의 자연스러운 간격 */
.artist-name { margin: 1.5rem auto; }
.exhibition-description { line-height: 1.9; }
```

**감정 전달 전략**:
- **넉넉한 여백**: 작가의 "그늘 속 편안함" 철학을 공간 언어로 구현
- **자연스러운 행간**: 1.9-2.0의 행간으로 작가의 사색적 글귀를 천천히 음미할 수 있도록 설계
- **단계적 정보 공개**: 캐러셀에서 갤러리로 이어지는 점진적 몰입 구조

---

## 3. 관람 경험 (인터랙션)

### 추가한 Hover 효과와 인터랙션

**1. 캐러셀의 자동 순환과 수동 제어**

```css
/* 5개 슬라이드 자동 순환 */
#slide1 { animation: slide-auto 20s infinite; }
#slide2 { animation: slide-auto 20s 4s infinite; }
#slide3 { animation: slide-auto 20s 8s infinite; }
#slide4 { animation: slide-auto 20s 12s infinite; }
#slide5 { animation: slide-auto 20s 16s infinite; }

/* 부드러운 전환 효과 */
.carousel-item {
    transition: all 0.8s cubic-bezier(0.4, 0, 0.2, 1);
}
```

**특별한 경험**:
- **JavaScript 없는 순수 CSS 구현**: 안정성과 성능을 모두 확보
- **도트 네비게이션 애니메이션**: 내부에서 외부로 확장되는 원형 애니메이션
- **3D 변환 효과**: 작품들이 공간 속에서 자연스럽게 이동하는 깊이감

**2. 다양한 카드 인터랙션**

```css
/* 기본 호버 효과 */
.artwork:hover {
    transform: translateY(-8px);
    box-shadow: 0 25px 80px var(--shadow-medium);
}

/* 이미지별 특화된 효과 */
.artwork:nth-child(5):hover img {
    transform: scale(1.05) rotate(2deg); /* 원형 이미지 회전 */
}

/* 반짝이는 효과 */
.artwork:hover img::after {
    animation: shimmer 1.5s ease-in-out;
}
```

### 관람객의 시선 흐름 유도

**1. 작가 중심의 내러티브 구조**:
1. **Header**: 작가명과 전시 제목으로 정체성 명확화
2. **작가 인용문**: 개인전 "뜨거운 햇빛과 서늘한 그늘"의 철학적 배경 제시
3. **캐러셀**: 5개 작품의 시각적 미리보기
4. **갤러리**: 각 작품의 감성적 해석과 스토리텔링
5. **Footer**: 작가 소개와 연락처로 관계 형성

**2. 시각적 계층 구조**:
- **크기**: h1(3.2rem) → 작가명(1.5rem) → h2(2rem) → 본문(1.1rem)
- **색상 위계**: 진한 브라운(제목) → 중간 브라운(본문) → 연한 브라운(부가정보)
- **시각적 무게**: 작가명 → 작품 이미지 → 제목 → 설명

### 사용자 경험(UX)을 위한 특별 고려사항

**1. 작가 브랜딩 강화**:

```css
.artist-name {
    font-style: bold;
    color: var(--deep-brown);
    margin: 1.5rem auto;
    font-size: 1.5rem;
}
```

**2. 접근성과 성능 최적화**:
- **움직임 민감도 고려**: `prefers-reduced-motion` 미디어 쿼리 지원
- **명확한 포커스 상태**: 키보드 네비게이션 사용자를 위한 아웃라인 설정
- **의미론적 구조**: 스크린 리더 사용자를 위한 명확한 HTML 시맨틱

**3. 감성적 몰입도 향상**:
- **점진적 정보 공개**: 캐러셀(시각적 임팩트) → 갤러리(상세 감상)
- **자연스러운 애니메이션**: 0.8초의 여유로운 전환으로 성급하지 않은 관람 경험
- **작가 철학 반영**: "그늘의 편안함"을 색상과 여백으로 공간화

---

## 결론

이 "추억의 재구성" 전시회는 성률 작가의 개인적 철학인 **"그늘 속 편안함"**을 디지털 공간에서 구현한 온라인 갤러리입니다.

**핵심 디자인 철학**:
- **작가 중심성**: 성률 작가의 고유한 시각과 철학을 웹사이트 전체에 일관되게 반영
- **그늘의 미학**: 뜨겁지 않은 서늘함, 편안함, 사색의 공간을 색상과 레이아웃으로 구현
- **추억의 재구성**: 일상적 순간들을 5가지 다른 방식으로 재해석하여 각각의 기억을 특별하게 연출
- **기술적 완성도**: JavaScript 없는 순수 CSS로 구현된 안정적이고 접근 가능한 사용자 경험

관람객이 작가의 시선으로 일상을 바라보고, 각자의 추억을 재구성할 수 있는 **디지털 사색 공간**을 만들고자 했습니다.