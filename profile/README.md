<img width="1728" height="537" alt="image" src="https://github.com/user-attachments/assets/d1860d97-6bea-4aef-8f04-b9d082dafdef" />

<h1 align="center">Cking</h1>

<p align="center">
  <b>팬 활동을 응모권과 이벤트 참여로 연결하고,<br/>
  동시 응모부터 재현 가능한 추첨·재추첨까지 다루는 팬덤 참여 플랫폼</b>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Java-21-007396?logo=openjdk&logoColor=white" alt="Java 21" />
  <img src="https://img.shields.io/badge/Spring_Boot-4.1.1-6DB33F?logo=springboot&logoColor=white" alt="Spring Boot" />
  <img src="https://img.shields.io/badge/MySQL-8.4-4479A1?logo=mysql&logoColor=white" alt="MySQL" />
  <img src="https://img.shields.io/badge/Redis-7.2-DC382D?logo=redis&logoColor=white" alt="Redis" />
  <img src="https://img.shields.io/badge/React-Vite-61DAFB?logo=react&logoColor=111111" alt="React" />
  <img src="https://img.shields.io/badge/Docker-AWS-2496ED?logo=docker&logoColor=white" alt="Docker AWS" />
</p>

<p align="center">
  <a href="#1-프로젝트-소개">프로젝트 소개</a> ·
  <a href="#2-핵심-기술-과제">핵심 기술 과제</a> ·
  <a href="#3-아키텍처와-핵심-처리-흐름">아키텍처</a> ·
  <a href="#4-benchmark-driven-development">Benchmark</a> ·
  <a href="#7-팀원-소개">팀원</a> ·
  <a href="#8-mentoring--technical-review">Mentoring</a>
</p>

---

## 1. 프로젝트 소개

### 서비스 개요

**Cking**은 크리에이터와 팬의 활동을 하나의 서비스 흐름으로 연결하는 팬덤 참여 플랫폼이다.

팬은 크리에이터를 팔로우하고 출석·좋아요·공유·구독 인증 등의 활동을 수행해 응모권을 획득하며, 획득한 응모권으로 이벤트에 응모한다. 이벤트가 종료되면 서버가 마감 이전의 정상 응모를 확정한 뒤 공식 Snapshot을 생성하고, **Snapshot · Seed · Algorithm Version**을 기반으로 재현 가능한 추첨을 수행한다.

Creator에게는 Creator Space, 게시글·댓글, 일정 관리, 이벤트 생성·운영 기능을 제공한다. Admin에게는 Creator 승인, 이벤트 승인·마감, 추첨 결과 공개, Winner 운영, 재추첨과 같은 운영 기능을 제공한다.

| 항목 | 내용 |
| --- | --- |
| **프로젝트** | LG U+ URECA 최종 융합 프로젝트 |
| **기간** | **2026.09.09 ~ 2026.10.28** |
| **인원** | 8명 |
| **Backend** | Java 21 · Spring Boot 4.1.1 · MySQL 8.4 · Redis 7.2 · Flyway |
| **Frontend** | React · Vite · Tailwind CSS · PWA |
| **Infra** | Docker · AWS · GitHub Actions |

### 서비스 구성

Cking은 단순 이벤트 응모 기능만 제공하지 않고, 팬 활동부터 크리에이터 공간 운영, 이벤트 응모·추첨, AI 기능 검증까지 하나의 서비스로 구성한다.

| 영역 | 주요 기능 |
| --- | --- |
| **Fan Engagement** | OAuth 로그인 · 크리에이터 팔로우 · 출석/좋아요/공유 미션 · 응모권 · 개인 캘린더 |
| **Creator Space** | Creator Space · 커스텀 URL · 게시글 · 댓글 · 크리에이터 일정 · YouTube 채널 설정 |
| **Event & Raffle** | 이벤트 생성·승인 · 응모 · 실시간 응모 현황 · 안전한 마감 · Snapshot · 가중 추첨 · 결과 공개 · 재추첨 |
| **Operation** | Creator 승인 · Event 승인/거절 · 수동 마감 · Winner 관리 · 알림 · Dead Stream 운영 |
| **AI Features** | YouTube 구독 인증 VLM · AI Quiz · 크리에이터 추천 실험 · 댓글 필터링 실험 |

<p align="center"><sub><i>이미지 추가 예정 · 서비스 주요 화면</i></sub></p>

### 사용자 흐름

Cking은 팬의 활동부터 이벤트 참여, 추첨 결과 확인까지의 전체 흐름을 하나의 서비스 안에서 연결한다.

팬은 크리에이터를 팔로우하고 미션을 수행해 응모권을 획득하며, 획득한 응모권으로 이벤트에 참여한다. 이벤트 종료 후에는 안전한 마감과 공식 Snapshot 생성을 거쳐 추첨을 수행하고, 결과 공개 및 필요 시 재추첨까지 이어진다.

<p align="center">
  <a href="https://github.com/user-attachments/assets/c10c62d9-f9e2-43d8-9895-3a322831d488">
    <img src="https://github.com/user-attachments/assets/c10c62d9-f9e2-43d8-9895-3a322831d488" alt="Cking User Flow" width="100%" />
  </a>
</p>

<p align="center">
  <sub><i>이미지를 클릭하면 전체 사용자 흐름을 크게 확인할 수 있다.</i></sub>
</p>


### 역할별 주요 기능

| Fan | Creator | Admin |
| --- | --- | --- |
| OAuth 로그인 | Creator 권한 신청 | Creator 신청 승인·거절 |
| 크리에이터 팔로우 | Creator Space 운영 | Event 승인·거절 |
| 미션 수행 · 응모권 획득 | 게시글 · 댓글 · 일정 관리 | 수동 마감 · 마감 상태 확인 |
| Event 조회 · 응모 | Event 생성 · 수정 · 승인 요청 | 추첨 실행 · 결과 공개 |
| 응모 내역 · 당첨 결과 · 알림 확인 | YouTube 채널 · 미션 관리 | Winner 운영 · 재추첨 · 장애 데이터 관리 |

---

## 2. 핵심 기술 과제

Cking의 핵심은 단순한 Event CRUD가 아니라 **응모 → 마감 → 추첨 → 공개 → 재추첨** 전체 과정에서 데이터 정합성, 멱등성, 장애 복구 가능성, 추첨 재현성을 유지하는 데 있다.

| 기술 과제 | 해결 방식 |
| --- | --- |
| **동시 응모의 원자성** | Redis Lua에서 멱등성 · Gate · 잔액 검증 · 차감 · Stream 발행을 하나의 원자 연산으로 처리한다. |
| **비동기 영속화의 정합성** | Redis Stream Consumer가 Entry · Ledger · DB Balance를 동일 DB Transaction으로 반영하고 Commit 이후에만 XACK한다. |
| **안전한 이벤트 마감** | `OPEN → CLOSING → CLOSED` 상태를 분리하고 Gate 차단 · Barrier · `cutoffStreamId` · Drain으로 마감 경계를 고정한다. |
| **추첨 입력의 불변성** | CLOSED 이후 공식 Snapshot을 생성하고 정규화된 입력의 Hash를 저장한다. |
| **추첨 결과의 재현성** | Snapshot · Seed · Algorithm Version을 함께 보존해 동일 입력에서 동일 결과를 재현할 수 있도록 설계한다. |
| **Retry와 Redraw의 분리** | 기술 장애 복구는 동일 Drawing Retry로 처리하고, 결원 보충은 새로운 REDRAW Drawing으로 분리한다. |
| **Redis·DB 정합성 복구** | 잔액 정합성 배치 · 수동 재동기화 · Balance Key 복구 · PEL 회수 · Dead Stream replay 경로를 둔다. |
| **인증 경계 일원화** | Google/Kakao OAuth2, Login Code, Access JWT, Refresh Token Rotation을 통해 사용자·Creator·Admin API의 호출자 식별을 통일한다. |
| **AI 기능의 실험 기반 선정** | 특정 모델을 바로 도입하지 않고 독립 Benchmark Repository에서 평가 계약과 선택 근거를 관리한다. |
| **배포·운영 안전성** | Migration 순서 검사, CI 통과 커밋 배포, 배포 후 Smoke Test, GitHub Actions SHA 고정 등 운영 위험을 CI/CD 단계에서 줄인다. |

### 설계 원칙

- 동일 업무 요청이 재전송되어도 중복 처리하지 않는다.
- Redis와 DB를 하나의 Transaction으로 묶지 않는다.
- 비동기 처리 이후에도 최종 DB 상태를 검증할 수 있도록 한다.
- Event 마감 시점을 명확한 경계로 고정한다.
- 추첨 입력과 실제 추첨 실행을 분리한다.
- 공식 추첨 결과를 재현할 수 있도록 한다.
- 기술적 Retry와 업무상 Redraw를 구분한다.
- Event 상태 변경은 공통 상태 전이 경계를 통해 수행한다.
- AI 모델은 데모 결과가 아니라 동일 평가 계약과 검증 데이터에 기반해 비교한다.

---

## 3. 아키텍처와 핵심 처리 흐름

### 전체 아키텍처

<p align="center"><sub><i>이미지 추가 예정 · 전체 시스템 아키텍처</i></sub></p>

Cking Backend는 하나의 Spring Boot 애플리케이션 안에서 도메인 책임을 분리하고, Part 간 연동은 같은 애플리케이션 내부의 Service Method 호출을 기본으로 한다.

| Part | 주요 책임 | 담당 |
| --- | --- | --- |
| **Part 1 — 사용자 · 크리에이터 · 미션** | Member/Creator · Mission · 응모권 적립/조회 · Calendar | 김태연 · 정문구 |
| **Part 2 — 이벤트 · 응모 · Redis · 마감** | Event · Entry · Redis Lua · Stream · Consumer · 마감 · 정합성 복구 | 이성집 · 정자비 |
| **Part 3 — Snapshot · Drawing · Winner** | Snapshot · Hash · Seed · Drawing · Winner · Retry · 재현 검증 | 정윤희 · 조성원 |
| **Part 4 — 운영 · 공개 · 재추첨** | Creator/Event 운영 · 마감 요청 · 결과 공개 · Winner 운영 · RedrawRequest · Notification | 권혁준 |
| **공통 · Infra** | 프로젝트 기반 · 공통 예외 · Migration · Docker · CI/CD · AWS · 이미지 저장소 | 장근창 |

Part는 초기 핵심 업무의 책임 경계이며, 실제 개발에서는 인증, Creator Space, Calendar, AI 기능, Benchmark, Infra 등 교차 기능을 팀원별로 추가 담당한다.
<details>
<summary><b>아키텍처 핵심 설계 흐름 자세히 보기</b></summary>

<br/>

### Part 간 대표 흐름

각 Part는 하나의 Spring Boot 애플리케이션 안에서 역할을 분리하며, 필요한 기능은 명확한 서비스 계약을 통해 연동한다.

```text
Part 1
→ Part 2 Ticket EARN 처리

Part 2
→ CLOSED 확정
→ Part 3 공식 Snapshot 생성

Part 4
→ Part 2 수동 마감 요청

Part 4
→ Part 3 추첨 결과 조회 · 공개 · 재추첨 실행 연동
```

---

### Event Lifecycle

Event의 상태는 단순한 화면 표시용 값이 아니라 각 단계에서 허용되는 업무를 제한하는 **도메인 계약**으로 사용한다.

```text
DRAFT
→ PENDING_APPROVAL
→ SCHEDULED
→ OPEN
→ CLOSING
→ CLOSED
→ DRAW_COMPLETED
→ PUBLISHED

PENDING_APPROVAL → REJECTED
REJECTED → DRAFT
```

| 상태 | 의미 |
| --- | --- |
| `DRAFT` | Creator가 Event를 작성·수정하는 상태다. |
| `PENDING_APPROVAL` | Admin 승인을 기다리는 상태다. |
| `REJECTED` | Admin 승인이 거절된 상태다. |
| `SCHEDULED` | 승인이 완료되었으나 아직 시작 전인 상태다. |
| `OPEN` | 신규 응모가 가능한 상태다. |
| `CLOSING` | 신규 응모를 차단하고 기존 승인 응모를 DB에 확정하는 상태다. |
| `CLOSED` | 마감 이전 정상 응모가 모두 DB에 확정되어 Snapshot 생성이 가능한 상태다. |
| `DRAW_COMPLETED` | 최초 공식 추첨과 Winner 저장이 완료된 상태다. |
| `PUBLISHED` | 최초 공식 추첨 결과 공개가 완료된 상태다. |

Event 상태 변경은 개별 기능에서 직접 수행하지 않고 공통 `EventCommandService`를 **상태 전이의 단일 진입점**으로 사용한다.

---

### 응모와 비동기 영속화

동시 요청 상황에서도 **중복 차감 방지, 마감 이후 응모 차단, 잔액 검증, Stream 발행**이 서로 분리되지 않도록 Redis Lua를 사용한다.

```text
Client Request
↓
Redis Lua
├─ requestId 멱등성 확인
├─ Event Gate 확인
├─ Event 시간 확인
├─ request fingerprint 확인
├─ Balance 확인
├─ Balance 차감
├─ Entry Stream XADD
└─ 멱등 결과 저장
↓
SUCCESS / DUPLICATE_REPLAY 등 응답
↓
Redis Stream Consumer
↓
DB Transaction
├─ EventEntry INSERT
├─ TicketLedger(SPEND) INSERT
└─ DB Balance UPDATE
↓
COMMIT
↓
XACK
```

Redis Stream은 **at-least-once 전달**을 전제로 한다.

Consumer가 동일 메시지를 다시 처리할 가능성이 있으므로 DB Unique Constraint와 기존 데이터 검증으로 Consumer 멱등성을 보완하며, 처리 실패 메시지는 PEL 회수와 Dead Stream Replay를 통해 별도의 복구 경로를 제공한다.

---

### 이벤트 마감과 Snapshot 경계

Cking에서 `CLOSED`는 단순히 `endAt`이 지난 상태를 의미하지 않는다.

**마감 이전에 정상 승인된 응모가 모두 DB에 확정되어 공식 Snapshot을 생성해도 안전한 상태**를 의미한다.

```text
[Redis]

Gate CLOSED
+
EVENT_ENTRY_CLOSED Barrier XADD
+
최초 cutoffStreamId 확정 · 보존

        ↓

[DB Transaction 1]

OPEN → CLOSING
cutoffStreamId 저장
COMMIT

        ↓

[Transaction 밖]

awaitDrain(eventId, cutoffStreamId)

        ↓

[DB Transaction 2]

CLOSING → CLOSED
closedAt 기록
COMMIT
```

`cutoffStreamId`는 마감 전에 승인되어 반드시 DB에 반영되어야 하는 응모의 경계를 나타낸다.

Drain은 다음 조건이 모두 충족된 경우에만 완료한다.

```text
cutoff 범위의 정상 승인 응모가 모두 DB에 반영됨
+
해당 범위의 미처리 메시지 없음
+
해당 범위의 미ACK 메시지 없음
+
해당 범위의 미해결 Dead Stream 없음
```

마감 전체를 하나의 긴 DB Transaction으로 처리하지 않고, 상태 변경 Transaction과 Drain 대기를 분리해 **장시간 DB Lock과 Connection 점유를 방지한다.**

---

### 재현 가능한 추첨

Official Snapshot은 Event 마감 이후 **공식 추첨에 사용되는 입력 데이터를 고정한 불변 데이터**다.

```text
CLOSED
↓
EventEntry를 Member별로 합산
↓
Candidate 정렬
↓
Official Snapshot 생성
↓
입력 정규화
↓
Snapshot Hash 저장
```

Snapshot을 생성한 이후에는 동일 Event의 최초 추첨과 재추첨 모두 최초 공식 Snapshot을 기준으로 수행한다.

Drawing은 Snapshot을 기준으로 수행한 **실제 추첨 실행 한 번**을 의미한다.

```text
Snapshot
+
Seed
+
Algorithm Version
+
winnerCount
+
Exclusion List
↓
DrawingEngine
↓
Winner
↓
Result Hash
```

다음 입력이 동일하면 동일한 추첨 결과를 재현할 수 있도록 설계한다.

```text
동일 Snapshot
+
동일 Seed
+
동일 Algorithm Version
+
동일 Exclusion List
+
동일 winnerCount
=
동일 Drawing Result
```

Snapshot Hash와 Result Hash를 통해 추첨 전 입력의 무결성과 추첨 후 결과의 재현 가능성을 검증한다.

---

### Retry와 Redraw의 분리

기술적인 실행 실패를 복구하는 **Retry**와 당첨자 결원으로 새로운 추첨을 수행하는 **Redraw**를 서로 다른 개념으로 관리한다.

| 구분 | Retry | Redraw |
| --- | --- | --- |
| **목적** | 시스템 오류·서버 장애 등 기술적 실행 실패 복구 | 당첨 포기·자격 상실로 발생한 결원 보충 |
| **Drawing** | 기존 Drawing 재사용 | 새로운 `REDRAW` Drawing 생성 |
| **Snapshot** | 기존 Snapshot 유지 | 최초 공식 Snapshot 재사용 |
| **Seed** | 기존 Seed 유지 | 새로운 Seed 생성 |
| **Algorithm Version** | 기존 Version 유지 | 최초 Drawing과 동일한 Version 사용 |
| **후보** | 기존 추첨 입력 유지 | 해당 Event에서 이미 Winner로 선정된 사용자 전체 제외 |

Retry에서는 기존 Drawing의 입력을 그대로 유지해 동일 실행을 복구한다.

Redraw에서는 최초 Snapshot을 변경하지 않고 기존 Winner를 후보에서 제외한 뒤 새로운 Seed로 별도의 Drawing을 생성한다.

이를 통해 **기술적인 재시도와 새로운 업무상 추첨을 하나의 개념으로 혼합하지 않는다.**

</details>

---

## 4. Benchmark Driven Development

Cking의 AI 기능은 모델 이름이나 단일 데모 결과만으로 선택하지 않는다. 서비스 코드와 분리된 Benchmark Repository에서 **평가 데이터 · Ground Truth · 실행 조건 · 실패 사례 · 선택 근거**를 관리한다.

```text
문제 정의
→ 후보 모델 · 방식 정의
→ 평가 계약 작성
→ 데이터 · Ground Truth 고정
→ 동일 조건 실행
→ 정량 평가
→ 실패 사례 분석
→ 선택 근거 기록
→ 서비스 연동
```

### 평가 원칙

- 후보마다 가능한 동일한 입력과 평가 조건을 사용한다.
- 모델 출력 형식이 맞는 것과 실제 정답 여부를 구분한다.
- API 성공률과 품질 정확도를 구분한다.
- 오탐과 미탐의 비용이 다르면 별도로 집계한다.
- 사람이 확인해야 하는 Ground Truth는 검수 상태를 명시한다.
- 모델 ID, Prompt, Dataset, Parameter 등 재현 조건을 기록한다.
- latency, token, cost 같은 운영 지표와 품질 지표를 함께 확인한다.
- 선택하지 않은 후보도 제외 이유와 실패 사례를 기록한다.

### Benchmark Repository

| Benchmark | 주요 담당 | 검증 대상 | 측정 결과 · 선택 근거 |
| --- | --- | --- | --- |
| **LLM Benchmark** | **이성집** | 크리에이터 추천을 위한 Embedding · 추천 방식 · LLM 보정 · 사람/자동 평가 | [Cking-LLM-Benchmark](https://github.com/URECA-Cking/Cking-LLM-Benchmark) · [현재 결과 및 선택 근거](https://github.com/URECA-Cking/Cking-LLM-Benchmark/blob/develop/docs/results/recommendation-decision.md) |
| **VLM Benchmark** | **권혁준** | YouTube 구독 인증 스크린샷의 채널 정보 · 구독 상태 판정 | [Cking-VLM-Benchmark](https://github.com/URECA-Cking/Cking-VLM-Benchmark) · [모델 비교](https://github.com/URECA-Cking/Cking-VLM-Benchmark/blob/main/docs/model-comparison.md) |
| **Filtering Benchmark** | **정자비** | 댓글 욕설 · 혐오 · 스팸 · 개인정보 필터링과 PASS/HOLD/BLOCK 정책 | [Cking-Filtering-Benchmark](https://github.com/URECA-Cking/Cking-Filtering-Benchmark) · [선정 기록](https://github.com/URECA-Cking/Cking-Filtering-Benchmark/blob/develop/docs/selection.md) |
| **Quiz Benchmark** | **김태연** | Video Grounding · Transcript 기반 Grounding · Quiz 생성 모델 및 조합 | [Cking-Quiz-Benchmark](https://github.com/URECA-Cking/Cking-Quiz-Benchmark) · [선정 기록](https://github.com/URECA-Cking/Cking-Quiz-Benchmark/blob/main/docs/selection.md) |

Accuracy, Precision, Recall, nDCG, Recall@K, latency, token, cost 등 **구체적인 수치와 비교표는 각 Benchmark Repository에서 관리한다.** 조직 README에는 실험 구조와 책임만 유지해 수치가 오래된 값으로 남는 문제를 방지한다.

---

## 5. 데이터와 코드 구조

### 데이터 설계 원칙

Cking은 현재 상태, 업무 사실, 추첨 입력, 실행 결과를 서로 다른 생명주기의 데이터로 구분한다.

| 분리 | 이유 |
| --- | --- |
| **UserTicketBalance ↔ TicketLedger** | 현재 잔액과 모든 증감 이력을 분리한다. |
| **Mission ↔ MissionCompletion** | 미션 정의와 실제 수행 사실을 분리한다. |
| **DrawSnapshot ↔ Drawing** | 공식 추첨 입력과 실제 추첨 실행을 분리한다. |
| **Winner ↔ WinnerManagement** | 변경하면 안 되는 추첨 결과와 이후 변경되는 운영 상태를 분리한다. |
| **Drawing Retry ↔ RedrawRequest** | 기술적 복구와 새로운 업무 실행을 분리한다. |

<p align="center"><sub><i>이미지 추가 예정 · ERD</i></sub></p>

### Backend Package Structure

최상위 패키지는 업무 도메인 단위로 분리하며, 각 도메인 내부는 `presentation → application → domain` 방향을 기본으로 한다.

<details>
<summary><b>패키지 구조 보기</b></summary>

<br/>

```text
📂 kr.co.cking
├── 📂 common                     공통 응답 · 예외 · 설정 · 이미지 처리
├── 📂 auth                       OAuth2 · JWT · Login Code · Refresh Token
├── 📂 member                     사용자
├── 📂 creator                    Creator · 승인 · Creator Space
├── 📂 follow                     크리에이터 팔로우
├── 📂 post                       게시글 · 댓글
├── 📂 calendar                   크리에이터 일정 · 개인 캘린더
├── 📂 mission                    출석 · 좋아요 · 공유 · 구독 미션
├── 📂 subscriptionverification   YouTube 구독 인증
├── 📂 quiz                       AI Quiz 생성
├── 📂 ticket                     Balance · Ledger · 적립 · 차감
├── 📂 event                      Event · Entry · 마감
├── 📂 snapshot                   공식 Snapshot 생성 · 검증
├── 📂 drawing                    추첨 · Seed · 재현 검증 · 공개
├── 📂 winner                     Winner · 운영 상태
├── 📂 redraw                     RedrawRequest · 재추첨 실행
├── 📂 notification               인앱 알림
├── 📂 stream                     Redis Stream · PEL · Dead Stream
└── 📂 support                    마스킹 등 공통 보조 기능
```

도메인 내부 기본 구조는 다음과 같다.

```text
📂 <domain>
├── 📂 presentation
├── 📂 application
├── 📂 domain
└── 📂 repository
```

주기 실행이 필요한 도메인에는 `scheduler`를 추가한다.

</details>

---

## 6. 기술 스택과 Repository

### 기술 스택

| 영역 | 기술 | 사용 목적 |
| --- | --- | --- |
| **Backend** | Java 21 · Spring Boot 4.1.1 · Gradle | 도메인 로직 · REST API · 비동기 처리 |
| **Database** | MySQL 8.4 · Flyway | 핵심 데이터 영속화 · Schema Versioning |
| **In-memory / Async** | Redis 7.2 · Redis Stream · Lua | 응모권 원자 처리 · 비동기 영속화 · 마감 경계 관리 |
| **Frontend** | React · Vite · Tailwind CSS · PWA | Fan · Creator · Admin Web Application |
| **Auth** | OAuth2 · Access JWT · Refresh Token | Google/Kakao 로그인 · 사용자 식별 · 권한 분리 |
| **AI** | LLM · VLM · Embedding API | 추천 · 구독 인증 · Quiz · Filtering 실험 및 연동 |
| **Storage** | S3 · S3Mock | 이미지 저장 · 로컬 개발 환경 호환 |
| **Infra** | Docker · AWS · GitHub Actions | 개발 환경 표준화 · CI/CD · 개발 서버 배포 |
| **Collaboration** | GitHub · Notion · Slack | Issue · PR · 문서 · 의사결정 관리 |

### Repository

| Repository | 역할 |
| --- | --- |
| [**Cking-BE**](https://github.com/URECA-Cking/Cking-BE) | Spring Boot Backend · Domain · Auth · Redis Stream · Event · Drawing · Creator Space · AI 연동 |
| [**Cking-FE**](https://github.com/URECA-Cking/Cking-FE) | React Web/PWA · Fan · Creator · Admin UI · OAuth 연동 |
| [**Cking-LLM-Benchmark**](https://github.com/URECA-Cking/Cking-LLM-Benchmark) | 크리에이터 추천 모델 · 추천 방식 비교 |
| [**Cking-VLM-Benchmark**](https://github.com/URECA-Cking/Cking-VLM-Benchmark) | 구독 인증 VLM 비교 |
| [**Cking-Filtering-Benchmark**](https://github.com/URECA-Cking/Cking-Filtering-Benchmark) | 댓글 필터링 방식 · 정책 비교 |
| [**Cking-Quiz-Benchmark**](https://github.com/URECA-Cking/Cking-Quiz-Benchmark) | 영상 Grounding · Quiz 생성 방식 비교 |
| [**.github**](https://github.com/URECA-Cking/.github) | 조직 README · 공통 GitHub Template · 협업 규칙 |

---

## 7. 팀원 소개

역할은 초기 Part 분담만이 아니라 현재 조직의 Backend, Frontend, Infra, AI Benchmark Repository에서 실제 구현한 책임 범위를 함께 정리한다.

| GitHub | 이름 | 핵심 담당 | Backend · Domain | Frontend · Infra | AI · Benchmark |
| --- | --- | --- | --- | --- | --- |
| <a href="https://github.com/hyuckjoon9"><img src="https://github.com/hyuckjoon9.png?size=90" width="72"/><br/>@hyuckjoon9</a> | **권혁준** | **팀장 · Part 4 운영/결과 공개** | Creator/Event 운영 · 수동 마감 연동 · Drawing 공개 · Winner 운영 · Notification · RedrawRequest · OAuth2/Spring Security · Login Code · Access JWT · Refresh Token Rotation · USER/ADMIN 인증 전환 · Creator Space 공유 미션 | 팀 일정·협업 조율 · 공통 API 규약/문서 정리 | **VLM Benchmark 설계·실행** · 구독 인증 VLM Adapter · 비동기 Executor · 이미지 재사용 탐지 · 비정상 행동 탐지 기준 설계 |
| <a href="https://github.com/taeyeonon"><img src="https://github.com/taeyeonon.png?size=90" width="72"/><br/>@taeyeonon</a> | **김태연** | **Part 1 · Member/Creator · AI Quiz** | 공통 Member/Creator Entity · 사용자 조회 · Ticket Balance/Ledger 조회 · 공용 출석 정책 · AI Quiz Core Engine · Gemini Provider Adapter | - | **Quiz Benchmark** · Pilot 데이터/평가 구조 · Ground Truth 검수 · Provider Adapter |
| <a href="https://github.com/rien00"><img src="https://github.com/rien00.png?size=90" width="72"/><br/>@rien00</a> | **이성집** | **Part 2 · Event/Entry/Closing · Recommendation** | Event 조회 · Entry API · EARN/SPEND Stream Consumer · PEL/Dead Stream · Event Closing · Redis/DB 응모권 정합성 · Balance 복구 · 공용 응모권 · 실시간 응모 현황 · Event 캐시 · 동시성 부하 테스트 | - | **LLM Benchmark 전담** · Embedding/추천 방식 비교 · LLM 태그 보정 · 자동/사람 평가 · 실제 데이터 검증 · 추천 방식 선정 |
| <a href="https://github.com/rmsckd1640"><img src="https://github.com/rmsckd1640.png?size=90" width="72"/><br/>@rmsckd1640</a> | **장근창** | **Platform · Infra · CI/CD** | 프로젝트 초기 세팅 · 초기 Migration · 공통 패키지/응답/예외 · 이미지 저장소 인터페이스 · S3 구현 | Docker · 개발 서버 배포 · S3/CloudFront · HTTPS · 환경변수 · Swagger · S3Mock · Smoke Test · Migration CI 검사 · GitHub Actions SHA 고정 · 이미지 처리 동시성 제한 | - |
| <a href="https://github.com/Jmg9808"><img src="https://github.com/Jmg9808.png?size=90" width="72"/><br/>@Jmg9808</a> | **정문구** | **Part 1 · Mission · Calendar** | Mission 완료 API · 출석/좋아요 정책 · Creator 기본 Mission 초기화 · 공용 응모권 도입 · Creator Calendar · 사용자 개인 Calendar | - | - |
| <a href="https://github.com/uniofficial"><img src="https://github.com/uniofficial.png?size=90" width="72"/><br/>@uniofficial</a> | **정윤희** | **Part 3 · Snapshot/Drawing · Subscription Verification** | Official Snapshot · Snapshot Hash · Drawing/Winner 도메인 · INITIAL Drawing · 결과 원자 저장 · Snapshot 누락 복구 · REDRAW 실패 복구 · OAuth 계정/사용자 매핑 · YouTube 구독 인증 도메인/영속성 · 이미지 제출 · Vision Port · Processing Claim · 판정/보상 오케스트레이션 · Recovery Scheduler · 구독 인증 E2E | - | Benchmark 결과 기반 구독 인증 모델 전환 및 서비스 연동 |
| <a href="https://github.com/mercy0704"><img src="https://github.com/mercy0704.png?size=90" width="72"/><br/>@mercy0704</a> | **정자비** | **Part 2 · Redis Atomic · Frontend · Creator Space** | Redis Lua EARN/SPEND 원자 처리 · 멱등성/잔액 동시성 보완 · Creator Space · 커스텀 slug · Follow · Post · Comment · 이미지 정규화 공통 모듈 | **Frontend 주요 구현/연동** · Router/Layout · 공통 HTTP Client · OAuth/JWT 전환 · Creator Space · Follow · Post/Comment · 반응형 UI · PWA/API 연동 | **Filtering Benchmark 전담** · 필터링 기준/데이터 계약 · 모델 후보 · 소량 호출 · 한국어 경계 사례 검증 |
| <a href="https://github.com/ch0rca"><img src="https://github.com/ch0rca.png?size=90" width="72"/><br/>@ch0rca</a> | **조성원** | **Part 3 · Drawing Engine** | Seed 기반 결정적 난수 · WEIGHTED_V1 가중 추첨 · DrawInput/DrawOutput 정규화 · Input/Result Hash · Drawing 성능 테스트 · Drawing Retry/실패 복구 · 상품 등급 가중치 추첨 · 추첨 알고리즘 조합 선택 | - | 추첨 알고리즘 성능·재현성 검증 |

---

## 8. Development Workflow

```text
Issue 생성
→ develop 최신화
→ 작업 Branch 생성
→ 구현
→ Pull Request
→ CI
→ Code Review
→ Squash and Merge
```

- `main`, `develop` 브랜치에는 직접 Push하지 않는다.
- 작업 단위는 Issue를 기준으로 관리한다.
- PR은 1명 이상의 Reviewer 승인 후 Merge한다.
- 자동화할 수 있는 검증은 가능한 CI로 이동한다.
- 상세 Branch · Issue · Commit · PR · Review 규칙은 [CONTRIBUTING.md](https://github.com/URECA-Cking/.github/blob/main/CONTRIBUTING.md)를 기준으로 한다.

---

## 9. Mentoring & Technical Review

<details>
<summary><b>외부 멘토링 (26-10-02)</b></summary>
<br/>

**1. AI / LLM 품질 평가 및 배포 기준**

현재 프로젝트에서는 동일한 영상 내용을 기반으로 Gemini와 GPT가 생성한 퀴즈를 비교하고 있으며, 정답 정확성, 영상 내용과의 일치 여부 등도 직접 검증하고 있습니다.
실제 서비스에서 LLM 기능을 도입할 때는 다음이 궁금합니다.

- 어떤 기준으로 LLM 품질을 평가하는가?
- 어느 수준까지 검증되어야 실제 서비스에 배포할 수 있다고 판단하는가?
- 정확도 외에 운영 단계에서 함께 확인해야 하는 주요 지표나 기준이 있는가?

**2. 신입 개발자에게 요구되는 역량**

요즘 회사에서 신입 개발자를 채용할 때 중요하게 보는 역량이나 기술, 경험이 무엇인지 궁금합니다.

- 신입에게 중요하게 보는 기술적 역량은 무엇인가?
- 프로젝트 경험에서는 어떤 부분을 중점적으로 보는가?
- 멘토님이 속한 팀에서는 어떤 역량이나 업무 태도를 가진 신입을 선호하는가?
- 기술 외에 특별히 중요하게 보는 조건이 있는가?

**3. 신입 개발자가 미리 준비하면 좋은 것**

멘토링을 진행하면서 신입 개발자나 취업 준비생에게 가장 많이 받아온 질문이 무엇인지 궁금합니다.
또한 실제 회사에 입사하기 전에 미리 알고 있으면 도움이 되는 내용을 듣고 싶습니다.

- 입사 전 반드시 알고 있으면 좋은 지식이나 기술은 무엇인가?
- 학교나 부트캠프에서 놓치기 쉬운 실무 지식은 무엇인가?
- 신입 개발자가 미리 만들어두면 좋은 개발 습관이 있는가?


**4. 어뷰징 탐지 기준과 Threshold 설정**

실제 사용자 데이터가 충분하지 않은 초기 서비스에서는 어뷰징 탐지를 위한 Rule과 Threshold를 설정하기 어려운데 다음 기준이 궁금합니다.

- 초기 Rule과 Threshold는 어떤 근거로 설정하는가?
- 실제 데이터가 없는 상황에서는 어떤 방식으로 기준값을 정하는가?
- 서비스 운영 후 데이터가 쌓이면 어떤 지표를 보고 Threshold를 보정하는가?
- 오탐과 미탐 사이의 기준은 실무에서 어떻게 조정하는가?

</details>
