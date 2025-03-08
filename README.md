# 바닐라 JS 프로젝트 성능 개선

-   url: https://d3895ewzxkx7pt.cloudfront.net

## 성능 개선 보고서

### 기존 성능 측정 결과

#### 🎯 Lighthouse 점수

| 카테고리       | 점수 | 상태 |
| -------------- | ---- | ---- |
| Performance    | 72%  | 🟠   |
| Accessibility  | 82%  | 🟠   |
| Best Practices | 75%  | 🟠   |
| SEO            | 82%  | 🟠   |
| PWA            | 0%   | 🔴   |

#### 📊 Core Web Vitals (2024)

| 메트릭 | 설명                      | 측정값 | 상태 |
| ------ | ------------------------- | ------ | ---- |
| LCP    | Largest Contentful Paint  | 14.56s | 🔴   |
| INP    | Interaction to Next Paint | N/A    | 🟢   |
| CLS    | Cumulative Layout Shift   | 0.011  | 🟢   |

### 성능 개선 방법

| 개선 항목     | 상세                                                                                         |
| ------------- | -------------------------------------------------------------------------------------------- |
| 접근성        | 1. `meta` 태그 추가 <br> 2. 대체 텍스트 작성                                                 |
| 쿠키 스크립트 | 1. `defer` 키워드 추가 <br> 2. 쿠키동의 배너 설정 수정                                       |
| 폰트 최적화   | 1. 프리커넥트 사용 <br> 2. 미디어 속성과 onload 활용 <br> 3. `noscript` 태그 추가            |
| 이미지 최적화 | 1. 이미지 포맷 변경(webp) <br> 2. `<picture>` 태그 사용 <br> 3. `img`태그의 lazy 속성으로 추가 |

#### 접근 이유 및 배경 지식 

- 웹 리소스 최적화

  1. CSS 최적화<br>
CSS는 랜더링 차단 리소스이다. media 속성을 사용하면 CSS 파일이 어떤 시점에 적용될지 결정할 수 있다. 예를 들어 `<link href='print.cc' rel='stylesheet' media='print'>`로 작성하면 프린트 시점에서 CSS 파일이 적용된다. 

  2. 폰트 최적화 <br>
  - preload: 현재 페이지에서 확실히 사용할 리소스는 `preload`를 사용해 미리 가져옴, 반드시 as 속성으로 브라우저에 리소스 유형을 알려줘야함 
 
  - preconnect: 외부 도메인의 리소스를 참고할때, 브라우저가 미리 외부 도메인과 연결할 수 있도록 함. 현재 폰트 리소스를 위해 미리 연결했음.<br>
    ```
    <link rel="preconnect" href="https://fonts.googleapis.com" />
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
    ```
    
- 접근성
  1. `<meta>` 태그:
 
  2. 레이아웃 요소
| 태그 | 설명|  
| -------------- | ---- | 
| `<header>`|  상단 영역| 
| `<nav>`  | 메뉴 내비엑이션 |
| `<main>` | 메인 콘텐츠  | 
| `<section>` |        |  
| `<article>` |        |
|    `<aside>` |        |  
| `<footer>` |        |  
 
  3. 그 외<br>
  `<br>` vs `<strong>`와  `<i>` vs `<em>`: 생긴 건 똑같지만 `<strong>`과 `<em>`가 더 강조의 의미를 포함<br>
  `<small>`: 텍스트를 작게 표시<br>
  `<mark>`: 하이라이트<br>
  `<ins>`: 밑줄<br>
  `<sub> <sup>`: 아래 첨자, 위 첨자<br>
  `<blockquote>`: 인용<br>
  `<cite>`: 책, 노래, 영화, 미술품 등 작품에 대한 타이틀<br>

  
- 스크립트 최적화  

- 이미지 최적화

1) 왜 이미지 포맷을 바꾸었는가?

2) 왜 `picture`태그를 사용했는가?

3) 지연로딩이란?

### 최종 성능 측정 결과

#### 🎯 Lighthouse 점수

| 카테고리       | 점수 | 상태 |
| -------------- | ---- | ---- |
| Performance    | 99%  | 🟢   |
| Accessibility  | 95%  | 🟢   |
| Best Practices | 75%  | 🟠   |
| SEO            | 100% | 🟢   |
| PWA            | 0%   | 🔴   |

#### 📊 Core Web Vitals (2024)

| 메트릭 | 설명                      | 측정값 | 상태 |
| ------ | ------------------------- | ------ | ---- |
| LCP    | Largest Contentful Paint  | 2.03s  | 🟢   |
| INP    | Interaction to Next Paint | N/A    | 🟢   |
| CLS    | Cumulative Layout Shift   | 0.011  | 🟢   |

### 참고

- Core Web Vitals

Google이 제시한 웹 페이지 품질을 측정하는 핵심 지표

1) LCP : 페이지 로딩 성능을 측정. 주요 콘텐츠가 화면에 표시되는 시간을 의미.

2) INP : 상호작용성을 측정, 사용자가 페이지와 처음 상호작용할 때(예: 링크 클릭, 버튼 탭 등)부터 브라우저가 상호작용에 응답할 수 있을 때까지의 시간을 측정.

3) CLS : 시각적 안정성을 측정, 페이지 로딩 중 예기치 않게 레이아웃이 변경되는 정도를 수치화
