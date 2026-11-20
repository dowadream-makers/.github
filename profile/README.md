<div align="center">

<img src="./assets/banner.png" alt="도와드림 — 가까운 병원과 대기 인원까지 도와드릴게요" width="100%" />

<br/>

<img src="https://img.shields.io/badge/서울_노원구-어르신_병원_안내-F5548C?style=for-the-badge&labelColor=1F1F1F" alt="서울 노원구 어르신 병원 안내" />
<img src="https://img.shields.io/badge/인덕대학교-2026_지역문제해결_메이커톤-00A7B7?style=for-the-badge&labelColor=1F1F1F" alt="인덕대학교 2026 지역문제해결 메이커톤" />
<img src="https://img.shields.io/badge/상태-시제품_개발_중-FCE4ED?style=for-the-badge&labelColor=1F1F1F" alt="시제품 개발 중" />

</div>

<br/>

## 💗 도와드림은요

동네 의원에 가면 **얼마나 기다려야 하는지** 알 수 없고, 어디가 아플 때 **어느 진료과로 가야 하는지**도 헷갈립니다.
작은 글씨와 복잡한 화면은 어르신에게 또 하나의 벽이 되고요.

**도와드림**은 서울 노원구 어르신이 휴대폰으로 쉽게 병원을 찾도록 돕는 모바일 웹앱입니다.
증상을 고르면 맞는 진료과를 안내하고, 가까운 병원과 **진료실 앞 실시간 대기 인원**을 큰 글씨로 보여드려요.
대기 인원은 진료실 문 위에 단 **60GHz 레이더 장치**가 직접 셉니다.

<table>
  <tr>
    <td width="33%" valign="top">
      <h3>🩺 증상으로 찾기</h3>
      "무릎이 아파요", "어지러워요"처럼 큰 버튼을 누르면 맞는 진료과를 알려드려요. 진단이 아닌 안내이고, 응급 증상은 <b>119를 먼저</b> 안내합니다.
    </td>
    <td width="33%" valign="top">
      <h3>🏥 가까운 병원과 대기 인원</h3>
      노원구 병·의원 공공데이터로 주변 병원을 찾고, <b>"4명 대기 중 · 약 25분"</b>처럼 기다림을 미리 보여드려요.
    </td>
    <td width="33%" valign="top">
      <h3>📞 전화 한 번, 길찾기 한 번</h3>
      병원 카드에서 바로 전화를 걸거나 길을 찾아요. 전화할 때 <b>무엇을 물어보면 되는지</b>도 예시로 알려드려요.
    </td>
  </tr>
</table>

> **어르신 기준으로 만듭니다.** 본문 17px 이상, 버튼 글자 20px 이상, 화면마다 할 일은 하나. 필요 없는 정보는 과감히 뺍니다.

<br/>

## 📡 어떻게 동작하나요

<img src="./assets/how-it-works.png" alt="레이더 장치 → 도와드림 서버 → 어르신 앱" width="100%" />

```mermaid
flowchart LR
    R["📡 레이더 장치<br/>ESP32-S3 + HLK-LD6001A"] -- "Wi-Fi · 1분마다 대기 인원" --> S["🖥️ 도와드림 서버<br/>Spring Boot + Kotlin"]
    P["🏛️ 공공데이터<br/>심평원 · 국립중앙의료원"] -- "하루 1번 동기화" --> S
    S <--> D[("🗄️ Supabase<br/>PostgreSQL")]
    S -- "병원 · 대기 인원 · 예상 시간" --> A["📱 어르신 앱<br/>React + Vite"]

    style R fill:#1F1F1F,color:#fff,stroke:#1F1F1F
    style S fill:#00A7B7,color:#fff,stroke:#00A7B7
    style A fill:#F5548C,color:#fff,stroke:#F5548C
    style P fill:#FFFBF6,color:#1F1F1F,stroke:#F1E1E7
    style D fill:#FFFBF6,color:#1F1F1F,stroke:#F1E1E7
```

- 레이더는 **카메라가 아니어서** 얼굴이나 모습을 찍지 않고, 사람의 위치 좌표만 읽습니다.
- 대기 구역 안에 **30초 이상 머문 사람**만 대기 인원으로 세서, 지나가는 사람은 빠집니다.
- 문으로 들어온 인원이 아니라 **진료실 앞에 실제로 앉아 기다리는 인원**을 셉니다.

<br/>

## 📱 화면 미리보기

<img src="./assets/screens-1.png" alt="홈 · 지역 변경 · 증상 선택 · 증상 더 보기 · 확인 안내" width="100%" />
<img src="./assets/screens-2.png" alt="병원 목록 · 관심 병원 · 병원 정보 · 전화 연결 · 길찾기" width="100%" />

<br/>

## 🗂️ 저장소

| 저장소 | 하는 일 | 기술 |
|---|---|---|
| [**dowadream-FE**](https://github.com/dowadream-makers/dowadream-FE) | 어르신용 모바일 웹앱 화면 | ![React](https://img.shields.io/badge/React-1F1F1F?style=flat-square&logo=react&logoColor=61DAFB) ![Vite](https://img.shields.io/badge/Vite-1F1F1F?style=flat-square&logo=vite&logoColor=FFD62E) ![TypeScript](https://img.shields.io/badge/TypeScript-1F1F1F?style=flat-square&logo=typescript&logoColor=3178C6) ![Vercel](https://img.shields.io/badge/Vercel-1F1F1F?style=flat-square&logo=vercel&logoColor=white) |
| [**dowadream-BE**](https://github.com/dowadream-makers/dowadream-BE) | 병원 정보·대기시간 API, 장치 보고 수신, 공공데이터 동기화 | ![Spring Boot](https://img.shields.io/badge/Spring_Boot_4-1F1F1F?style=flat-square&logo=springboot&logoColor=6DB33F) ![Kotlin](https://img.shields.io/badge/Kotlin-1F1F1F?style=flat-square&logo=kotlin&logoColor=7F52FF) ![Supabase](https://img.shields.io/badge/Supabase-1F1F1F?style=flat-square&logo=supabase&logoColor=3FCF8E) ![Render](https://img.shields.io/badge/Render-1F1F1F?style=flat-square&logo=render&logoColor=white) |
| [**dowadream-arduino**](https://github.com/dowadream-makers/dowadream-arduino) | 진료실 앞 대기 인원 측정 장치 펌웨어와 실시간 모니터 | ![ESP32](https://img.shields.io/badge/ESP32--S3-1F1F1F?style=flat-square&logo=espressif&logoColor=E7352C) ![Arduino](https://img.shields.io/badge/Arduino-1F1F1F?style=flat-square&logo=arduino&logoColor=00979D) ![Radar](https://img.shields.io/badge/HLK--LD6001A_60GHz-1F1F1F?style=flat-square) |

<br/>

## 🗓️ 진행 상황

| 단계 | 기간 | 내용 | |
|---|---|---|:-:|
| 기획·설계 | 2026.10 ~ 11 | 계획서, 와이어프레임, 기술 스택, 부품 구매 | ✅ |
| 디자인 | 2026.11 | 피그마 시안, 전문가 자문 반영, 최종 화면 18장 | ✅ |
| 앱·서버 | 2026.11 ~ 12 | 증상 안내, 병원 검색, 대기시간 계산, 공공데이터 연동 | 🔄 |
| 레이더 장치 | 2026.11 ~ 12 | 좌표 모드 펌웨어, 대기 구역 판별, Wi-Fi 전송 | 🔄 |
| 통합·시연 | 2026.12 | 앱–장치 연동, 3D 프린팅 케이스, 시연 모형 | ⏳ |
| 마무리 | 2027.01 | 사용자 시나리오 테스트, 최종 발표·경진대회 | ⏳ |

<br/>

## 👥 팀 도와드림

**인덕대학교** 컴퓨터소프트웨어학과 × 정보통신공학과가 함께 만듭니다.

| 컴퓨터소프트웨어학과 | 정보통신공학과 |
|---|---|
| 화면(UI), 증상 분류, 병원 검색·대기시간, 지도, 서버·DB | ESP32·레이더 하드웨어, 대기 인원 판별, Wi-Fi 통신, 3D 케이스 |

<br/>

<div align="center">
  <img src="./assets/logo.svg" width="44" alt="도와드림 로고" />
  <br/>
  <sub><b>도와드림</b> · 어르신의 병원 가는 길을 도와드립니다</sub>
  <br/>
  <sub>인덕대학교 2026학년도 지역문제해결 메이커톤</sub>
</div>
