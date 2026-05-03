# 🐧 Linux System Programming Suite

운영체제의 핵심 메커니즘(프로세스, 메모리, 파일 시스템, IPC)을 깊이 이해하고 제어하기 위해 POSIX API와 C 언어를 활용하여 직접 개발한 **3종의 로컬 시스템 유틸리티 컬렉션**입니다.

단순히 상위 계층의 라이브러리를 사용하는 것을 넘어, 리눅스 커널과 맞닿은 로우레벨 영역에서 발생할 수 있는 병목과 메모리 누수, 프로세스 생명주기를 치열하게 고민하며 구현했습니다.

## 🛠 Tech Stack
- **Language:** C (C99/C11)
- **Environment:** Linux (Ubuntu), GCC
- **Core Focus:** Process Control(`fork`, `exec`), File I/O, IPC(`SIGUSR1`), Dynamic Memory Allocation

---

## 📦 Projects Overview

### 1. [Local VCS (경량 버전 관리 시스템)](여기에_Local_VCS_레포_링크_삽입)
Git의 핵심 동작 원리(Snapshot 및 Diff)를 로컬 환경에 바닥부터 구현한 프로젝트입니다.
- **Key Features:**
  - `fork()`와 `execvp()`를 활용한 다중 명령어 라우팅 아키텍처
  - 자체 구현한 LCS 알고리즘 기반의 정밀한 라인 단위 Diff 추출
  - 대용량 소스 파일 파싱 시 `realloc`을 활용한 동적 메모리 스케일링으로 메모리 오버헤드 최소화

### 2. [Sync Daemon (백그라운드 디렉토리 동기화 데몬)](여기에_Sync_Daemon_레포_링크_삽입)
터미널 세션과 완전히 분리되어 백그라운드에서 실시간으로 파일 변경을 추적하고 동기화하는 데몬(Daemon) 유틸리티입니다.
- **Key Features:**
  - 폴링(Polling) 기법과 OpenSSL MD5 해싱을 결합한 파일 변경점 감지
  - 터미널 종료 후에도 안전하게 동작하도록 프로세스 생명주기 분리
  - IPC(`SIGUSR1`) 시그널 처리를 통한 안전한 데몬 종료(Graceful Shutdown) 제어

### 3. [Backup & Recovery System (스토리지 최적화 백업 툴)](여기에_Backup_System_레포_링크_삽입)
데이터 무결성을 보장하며, 중복 저장을 방지하여 스토리지 효율성을 극대화한 백업 및 복구 시스템입니다.
- **Key Features:**
  - `scandir`을 이용한 재귀적 디렉토리 탐색 구조 구현
  - MD5 해시 비교를 통해 동일 파일의 중복 백업 원천 차단
  - 연결 리스트(Linked List) 기반의 안전한 백업 로그 메모리 관리

---

## 🎯 What I Learned
이 스위트를 개발하며 멀티스레딩/멀티프로세스 환경에서의 동시성 제어, 좀비 프로세스 방지를 위한 `wait` 처리, 그리고 포인터와 메모리 누수(Memory Leak)를 다루는 로우레벨 디버깅 역량을 크게 향상시킬 수 있었습니다.
