# DeepSeek 분석 — IA · User Flow · Wireframe

> **분석 대상**: DeepSeek — 데스크톱(chat.deepseek.com) · 모바일 · 2026년 8월 기준
> 화면을 만들기 전에 정하는 세 가지를, 순서대로 DeepSeek에 적용해 분석했습니다.

| 순서 | 이름 | 우리말 | 답하는 질문 |
|---|---|---|---|
| 1 | IA (Information Architecture) | 화면·메뉴 구조 | 화면이 몇 개이고 무엇이 어디에 있는가 |
| 2 | User Flow | 사용자 흐름 | 사용자가 어떤 순서로 움직이는가 |
| 3 | Wireframe | 화면 뼈대 | 각 화면에 무엇이 어디에 놓이는가 |

---

## 1. IA — 화면과 메뉴 구조

### 데스크톱 — 컴퓨터로 볼 때

셋 중 가장 단순합니다. 오른쪽 패널이 없어서 **화면 하나에 영역이 둘**뿐입니다.

```
DeepSeek (chat.deepseek.com) — 화면 하나, 영역 둘
├── 왼쪽 (사이드바 — 항상 보임)
│   ├── 새 채팅 (큰 버튼)
│   ├── 대화 기록 (오늘 / 어제 / 지난 7일)
│   └── 프로필 → 설정
└── 가운데 (대화 본문)
    ├── 주고받은 내용 (사고 과정 상자 + 답변)
    └── 입력창 (DeepThink R1 · 웹 검색 토글 · + 첨부 · 전송)
```

### 모바일 — 폰으로 볼 때

모바일도 화면이 4개뿐입니다. 음성 모드도, 프로젝트도 없습니다.

```
DeepSeek 앱
├── S0. 온보딩·로그인 (첫 실행에만 잠깐)
├── S1. 채팅 화면 ★ 기본 화면 — 앱의 중심
│   ├── 상단 바 (≡ 사이드바 · ✎ 새 채팅)
│   ├── 대화 영역 (내 질문 오른쪽 · 사고 과정 상자 + 답변 왼쪽 전체 폭)
│   └── 입력바 (DeepThink R1 · 웹 검색 토글 · + 첨부 · 전송)
├── S2. 사이드바 — 서랍 (새 채팅 · 대화 기록 · 프로필)
└── S3. 설정 (계정 · 앱 환경 · 데이터)
```

기능을 늘리는 대신 **"생각하는 과정을 보여주기" 하나에 집중**한 IA입니다. 모델 선택 메뉴도 없이, 입력바의 DeepThink 토글이 그 역할을 대신합니다.

---

## 2. User Flow — 사용자 흐름

### 데스크톱 — 컴퓨터로 볼 때

**Flow A. 처음 쓰는 사람 — 접속부터 첫 답변까지**

```mermaid
flowchart TD
    KA1(["브라우저에서 chat.deepseek.com 접속"]) --> KA2["로그인<br/>Google / 이메일"]
    KA2 --> KA3["시작 화면<br/>입력창이 화면 한가운데"]
    KA3 --> KA4["첫 질문 입력 — Enter로 전송"]
    KA4 --> KA5["첫 답변 받음<br/>입력창은 하단으로 내려감"]
    KA5 --> KA6{"이어서 물어볼까?"}
    KA6 -->|"예"| KA4
    KA6 -->|"아니요"| KA7(["탭 닫기 — 다음에 다시"])
```

**Flow B. 매일의 핵심 루프 — 질문 ↔ 답변**

```mermaid
flowchart TD
    KB1(["chat.deepseek.com 접속"]) --> KB2["시작 화면<br/>로그인 유지 — 바로 도착"]
    KB2 --> KB3["질문 입력 · Enter"]
    KB3 --> KB4["답변이 실시간으로 출력됨<br/>— 스트리밍"]
    KB4 --> KB5{"다음 행동은?"}
    KB5 -->|"꼬리 질문"| KB3
    KB5 -->|"새 주제"| KB6["새 채팅 버튼"]
    KB6 --> KB3
    KB5 -->|"용무 끝"| KB7(["탭 닫기"])

    classDef hot fill:#dbeafe,stroke:#2563eb,color:#1e3a8a;
    class KB3,KB4 hot;
```

**Flow C. 지난 대화 이어가기 — 클릭 한 번**

```mermaid
flowchart LR
    KC1["사이드바가 항상 보임<br/>서랍 여는 단계가 없음"] --> KC2["대화 기록에서 스크롤로 찾기<br/>오늘 / 어제 / 지난 7일"]
    KC2 --> KC3["클릭 — 대화가 가운데 열림"]
    KC3 --> KC4["이어서 질문"]
```

**Flow D. 심층 사고(DeepThink) — DeepSeek만의 흐름**

```mermaid
flowchart TD
    KD1["입력바에서 DeepThink R1 켬"] --> KD2["질문 전송"]
    KD2 --> KD3["회색 상자에 사고 과정이<br/>먼저 흘러나옴"]
    KD3 --> KD4["이어서 최종 답변 출력"]
    KD4 --> KD5{"사고 과정이 궁금하면"}
    KD5 -->|"펼쳐서 읽기"| KD6["어떻게 이 답이 나왔는지 확인"]
    KD5 -->|"접어 두기"| KD7(["답변만 사용"])
    KD6 --> KD7

    classDef panel fill:#dbeafe,stroke:#2563eb,color:#1e3a8a;
    class KD3,KD6 panel;
```

### 모바일 — 폰으로 볼 때

**Flow A. 처음 쓰는 사람 — 설치부터 첫 답변까지**

```mermaid
flowchart TD
    NA1(["앱 첫 실행"]) --> NA2["S0. 온보딩·로그인<br/>Google / 이메일"]
    NA2 --> NA3["S1. 빈 채팅 화면<br/>'안녕하세요! 무엇을 도와드릴까요?'"]
    NA3 --> NA4["입력창에 첫 질문 입력"]
    NA4 --> NA5["첫 답변 받음"]
    NA5 --> NA6{"이어서 물어볼까?"}
    NA6 -->|"예"| NA4
    NA6 -->|"아니요"| NA7(["앱 종료 — 다음에 다시"])
```

**Flow B. 매일의 핵심 루프 — 질문 ↔ 답변**

```mermaid
flowchart TD
    NB1(["앱 실행"]) --> NB2["S1. 채팅 화면<br/>로그인 과정 없이 바로 도착"]
    NB2 --> NB3["질문 입력 · 전송"]
    NB3 --> NB4["답변이 실시간으로 출력됨<br/>— 스트리밍"]
    NB4 --> NB5{"다음 행동은?"}
    NB5 -->|"꼬리 질문"| NB3
    NB5 -->|"새 주제"| NB6["새 채팅 시작 ✎"]
    NB6 --> NB3
    NB5 -->|"용무 끝"| NB7(["앱 종료"])

    classDef hot fill:#dbeafe,stroke:#2563eb,color:#1e3a8a;
    class NB3,NB4 hot;
```

**Flow C. 지난 대화 이어가기 — 서랍을 열고 찾기**

```mermaid
flowchart LR
    NC1["S1. 채팅 화면"] -->|"≡ 누름"| NC2["S2. 사이드바 열림"]
    NC2 --> NC3["대화 기록에서 스크롤로 찾기<br/>오늘 / 어제 / 지난 7일"]
    NC3 --> NC4["대화 선택"]
    NC4 --> NC5["그 대화가 S1에 열림<br/>→ 이어서 질문"]
```

---

## 3. Wireframe — 화면 뼈대

그림 속 파란 번호(①②③…)와 설명이 짝을 이룹니다.

### 데스크톱 — 컴퓨터로 볼 때

<p align="center"><img src="./wireframes/pc-01-home.svg" width="780" alt="D1 시작 화면(데스크톱) 와이어프레임"></p>

<p align="center"><img src="./wireframes/pc-02-chatting.svg" width="780" alt="D2 대화 중(데스크톱) 와이어프레임"></p>

<p align="center"><img src="./wireframes/pc-03-thinking.svg" width="780" alt="D3 사고 과정 화면(데스크톱) 와이어프레임"></p>

### 모바일 — 폰으로 볼 때

<p align="center"><img src="./wireframes/01-home.svg" width="780" alt="W1 채팅 화면(빈 상태) 와이어프레임"></p>

<p align="center"><img src="./wireframes/02-chatting.svg" width="780" alt="W2 채팅 화면(대화 중) 와이어프레임"></p>

<p align="center"><img src="./wireframes/03-sidebar.svg" width="780" alt="W3 사이드바 와이어프레임"></p>

<p align="center"><img src="./wireframes/04-settings.svg" width="780" alt="W4 설정 화면 와이어프레임"></p>

---

화면·기능은 2026년 8월 DeepSeek(데스크톱·모바일) 기준이며, 업데이트에 따라 세부 모습은 조금씩 달라질 수 있습니다.
