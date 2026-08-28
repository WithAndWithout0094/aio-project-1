# Claude 분석 — IA · User Flow · Wireframe

> **분석 대상**: Claude 앱 (Anthropic) — 데스크톱(claude.ai) · 모바일 · 2026년 8월 기준
> 화면을 만들기 전에 정하는 세 가지를, 순서대로 Claude에 적용해 분석했습니다.

| 순서 | 이름 | 우리말 | 답하는 질문 |
|---|---|---|---|
| 1 | IA (Information Architecture) | 화면·메뉴 구조 | 화면이 몇 개이고 무엇이 어디에 있는가 |
| 2 | User Flow | 사용자 흐름 | 사용자가 어떤 순서로 움직이는가 |
| 3 | Wireframe | 화면 뼈대 | 각 화면에 무엇이 어디에 놓이는가 |

---

## 1. IA — 화면과 메뉴 구조

화면은 사실상 5개뿐이고, 중심은 **채팅 화면(S1) 하나**입니다.

```
Claude 앱
├── S0. 온보딩·로그인 (첫 실행에만 잠깐)
├── S1. 채팅 화면 ★ 기본 화면 — 앱의 중심
│   ├── 상단 바 (≡ 사이드바 · 대화 제목 · ✎ 새 채팅)
│   ├── 대화 영역 (내 질문 오른쪽 · Claude 답변 왼쪽 전체 폭)
│   └── 입력바 (+ 첨부 · 입력창 · 모델 선택 ⌄ · 음성 모드)
├── S2. 사이드바 — 서랍 (S1에서 ≡ 또는 스와이프)
│   ├── 검색
│   ├── 새 채팅
│   ├── 채팅 · 프로젝트
│   ├── 최근 항목 (최근 대화 목록)
│   └── 프로필 → S4. 설정 입구
├── S3. 음성 모드 (S1 입력바 오른쪽 버튼)
└── S4. 설정 (S2 프로필에서 진입)
    ├── 계정 · 구독 (Free / Pro / Max)
    ├── 개인 맞춤 (응답 스타일 · 메모리)
    └── 앱 환경 · 데이터 관리
```

---

## 2. User Flow — 사용자 흐름

**Flow A. 처음 쓰는 사람 — 설치부터 첫 답변까지**

```mermaid
flowchart TD
    A1(["앱 첫 실행"]) --> A2["S0. 온보딩·로그인<br/>Google / Apple / 이메일"]
    A2 --> A3["S1. 빈 채팅 화면<br/>'좋은 아침이에요, 사용자님'"]
    A3 --> A4["입력창에 첫 질문 입력"]
    A4 --> A5["첫 답변 받음"]
    A5 --> A6{"이어서 물어볼까?"}
    A6 -->|"예"| A4
    A6 -->|"아니요"| A7(["앱 종료 — 다음에 다시"])
```

**Flow B. 매일의 핵심 루프 — 질문 ↔ 답변**

```mermaid
flowchart TD
    B1(["앱 실행"]) --> B2["S1. 채팅 화면<br/>로그인 과정 없이 바로 도착"]
    B2 --> B3["질문 입력 · 전송"]
    B3 --> B4["답변이 실시간으로 출력됨<br/>— 스트리밍"]
    B4 --> B5{"다음 행동은?"}
    B5 -->|"꼬리 질문"| B3
    B5 -->|"새 주제"| B6["새 채팅 시작 ✎"]
    B6 --> B3
    B5 -->|"용무 끝"| B7(["앱 종료"])

    classDef hot fill:#dbeafe,stroke:#2563eb,color:#1e3a8a;
    class B3,B4 hot;
```

**Flow C. 지난 대화 이어가기**

```mermaid
flowchart LR
    C1["S1. 채팅 화면"] -->|"≡ 누름"| C2["S2. 사이드바 열림"]
    C2 --> C3{"찾는 방법"}
    C3 -->|"검색"| C4["검색어 입력"]
    C3 -->|"스크롤"| C5["최근 항목 목록"]
    C4 --> C6["대화 선택"]
    C5 --> C6
    C6 --> C7["그 대화가 S1에 열림<br/>→ 이어서 질문"]
```

---

## 3. Wireframe — 화면 뼈대

그림 속 파란 번호(①②③…)와 설명이 짝을 이룹니다.

### 데스크톱 — 컴퓨터로 볼 때

<p align="center"><img src="./wireframes/pc-01-home.svg" width="780" alt="D1 시작 화면(데스크톱) 와이어프레임"></p>

<p align="center"><img src="./wireframes/pc-02-chatting.svg" width="780" alt="D2 대화 중(데스크톱) 와이어프레임"></p>

<p align="center"><img src="./wireframes/pc-03-artifact.svg" width="780" alt="D3 아티팩트 분할 화면(데스크톱) 와이어프레임"></p>

### 모바일 — 폰으로 볼 때

<p align="center"><img src="./wireframes/01-home.svg" width="780" alt="W1 채팅 화면(빈 상태) 와이어프레임"></p>

<p align="center"><img src="./wireframes/02-chatting.svg" width="780" alt="W2 채팅 화면(대화 중) 와이어프레임"></p>

<p align="center"><img src="./wireframes/03-sidebar.svg" width="780" alt="W3 사이드바 와이어프레임"></p>

<p align="center"><img src="./wireframes/04-settings.svg" width="780" alt="W4 설정 화면 와이어프레임"></p>

---

화면·기능은 2026년 8월 Claude 앱(데스크톱·모바일) 기준이며, 업데이트에 따라 세부 모습은 조금씩 달라질 수 있습니다.
