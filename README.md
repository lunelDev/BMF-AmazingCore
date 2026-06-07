<div align="center">

# 💪 보자마자 피트니스 — 어메이징 코어 (Amazing Core)

**BLE 센서로 코어 운동을 인식해 트레이닝·게임·3D 자세뷰어로 즐기는 홈 피트니스 앱**
*A home-fitness app that reads your core-exercise motion via a BLE sensor and turns it into training routines, mini-games, and a 3D pose viewer.*

<img src="Screenshots/캡처.PNG" width="720"/>

**[🇰🇷 한국어](#-한국어)** · **[🇺🇸 English](#-english)**

`Unity3D (C#)` · `ESP32 BLE` · `Cinemachine` · `Unity Localization` · `DOTween` · `홈 피트니스 / Exergame`

[📺 시연 영상 (YouTube)](https://www.youtube.com/watch?v=Un5JtJjEnXU) · [📲 Google Play](https://play.google.com/store/apps/details?id=com.gateways.amazingcore&hl=ko-KR)

</div>

---

## 🇰🇷 한국어

### 📘 프로젝트 소개

‘어메이징 코어’는 Unity 기반의 **홈 피트니스 운동 콘텐츠 앱**입니다. 사용자가 **BLE 센서**를 착용하고 실제 코어 운동을 수행하면, 실시간 동작 데이터에 따라 **트레이닝 모드 · 게임 모드 · 3D 자세 뷰어**가 동작합니다.

**게임 요소(Gamification)** 와 **운동 루틴(Training System)** 을 결합해 운동의 몰입도와 지속성을 높이는 것을 목표로 개발했으며, 기획부터 설계·개발까지 전 과정에 참여해 **실전 프로젝트 수준의 시스템 구축 경험**을 쌓았습니다.

> 게임처럼 재미있고, 콘텐츠처럼 꾸준히 — 운동을 이어가게 만드는 홈 피트니스 솔루션.

### 📊 개발 개요

| 구분 | 내용 |
| --- | --- |
| **개발 기간 / 역할** | **2022.10 ~ 2023.03 (총 6개월)** · 핵심 기능 개발 ~2개월(트레이닝·게임·3D뷰어) + 기능 확장/현지화/QA ~4개월<br>기획 1 · 디자인 1 · 개발 1 협업 중 **개발 총괄 100% 담당** |
| **플랫폼** | Android (Google Play 출시) · 전용 BLE 센서 연동 |
| **기술 스택** | Unity3D (C#) · **VideoPlayer / RenderTexture**(운동·튜토리얼 영상) · **BLE(ESP32)**(코어 자세/움직임 인식) · **Unity UI + DOTween**(인터랙션) · **PlayerPrefs**(운동 이력/프로필) · **Unity Localization**(한/영) · **Cinemachine**(3D 뷰어·카메라) |
| **주요 기여** | 전체 UI/UX 설계·구현 · 트레이닝 루틴(7종 × 3단계) · 미니게임 3종 · 3D 자세 뷰어(Pinch/Zoom) · BLE 연동·로컬 데이터·다국어 |

### ✨ 핵심 기능

- 🏃 **BLE 센서 기반 코어 운동 인식** — ESP32 센서로 자세·중심 이동을 실시간 인식해 운동/게임 판정에 활용 (`Sensor/SensorManager`, `Protractor`, `OnConnect`, `AccelerationManager`)
- 🧠 **트레이닝 루틴 (7종 × 3단계)** — 초/중/고급 난이도, **영상 설명 → 튜토리얼 → 본 운동 → 결과 요약** 흐름 (`Training_AppManager`, `Training_UIManager`, `Training_DataManager`)
- 🎮 **미니게임 3종** — Tower Maker(블록 쌓기)·Delivery Man(중심 유지)·Wire Walking(줄타기), 클리어 시 퍼즐 보상 해금 (`Game_AppManager`, `Game_UIManager`, `Game_DataManager`)
- 📦 **3D 자세 뷰어** — 운동 자세 3D 모델을 프레임 단위로 재생, **Pinch/Zoom·회전** 제스처 (`3DViewMode/MediaPlayer`, `ExerciseDataSet`, `PinchDetection`, `ObjectZoomControls`, `CameraControls`)
- 🌍 **한/영 현지화** — Unity Localization으로 즉시 전환 (`LocaleSelectors`, `LocalizeStringEventManager`)
- 📈 **프로필·운동 이력** — PlayerPrefs 기반 자동 로그인 및 기록/뱃지/누적 시간 (`GameManager`, `Login_UIManager`)
- ▶️ **영상 가이드** — VideoPlayer/RenderTexture로 운동·튜토리얼 영상 재생 (`VideoHandle`, `MediaPlayer`)

### 🛠️ 기술 구현 하이라이트

- **트레이닝 흐름 제어** — Coroutine 기반으로 설명→튜토리얼→본 운동→결과 팝업을 단계 제어, 타이머·음성 카운트·버튼 UI 동기화.

  ```csharp
  public void StartTrainingRoutine()
  {
      ShowDescriptionUI();
      PlayTutorialClip();
      PlayMainWorkout();
      ShowClearPopup();
  }
  ```
- **3D 자세 뷰어** — `ExerciseDataSet`(ScriptableObject) 프리셋으로 프레임별 3D 오브젝트를 순차 생성, 터치 제스처로 확대/회전.

  ```csharp
  foreach (var frame in dataSet.objPerFrame)
  {
      Instantiate(frame, parent);
  }
  ```
- **센서 연동 가드** — BLE 상태 확인 → 미연결 시 경고·버튼 비활성화 (`ConnectAlarm`, `SensorManager`).
- **인터랙션 연출** — DOTween으로 버튼 강조·슬라이더 증가 등 자연스러운 UI 모션.
- **데이터 영속** — PlayerPrefs로 자동 로그인·운동 이력 유지, 게임 클리어 기록 → 보상 해금.

### 🎮 미니게임 (3종)

| 게임명 | 컨셉 | 핵심 로직 |
| --- | --- | --- |
| **Tower Maker** | 블록 쌓기 | 높이에 따른 카메라 위치 계산, 블록 Y축 이동 |
| **Delivery Man** | 중심 유지 | 좌우 기울기 판단, 도착 지점 도달 시 성공 |
| **Wire Walking** | 줄타기 | 일정 범위 이상 벗어나면 실패 처리 |

### ✅ 성과 요약

| 항목 | 내용 |
| --- | --- |
| **개발 기간** | 총 6개월 (핵심 개발 2개월 + 기능 확장/QA 4개월) |
| **기여도** | 전체 기능 개발 100% |
| **트레이닝** | 7종 × 3단계 루틴 |
| **게임** | Tower Maker · Delivery Man · Wire Walking |
| **BLE 연동** | 실시간 중심/자세 인식 |
| **다국어** | 한국어 / 영어 |
| **UI 구현** | 약 30개 화면·팝업 |
| **특징** | 실시간 운동 피드백 · 반복 학습 루틴 · 3D 자세 뷰어 · 다국어 |

### 🔁 전체 흐름

```
▶ 로그인 → 모드 선택
   ├ 트레이닝 모드 : 설명 → 튜토리얼 → 본 운동 → Clear 팝업 → 데이터 저장
   ├ 게임 모드     : 게임 선택 → 진행 → 성공/실패 → 퍼즐 보상 획득
   └ 자세 뷰어 모드 : 프레임 기반 자세 재생, 확대/회전
▶ 프로필 관리 / 기록 확인 / 언어 전환
```

### 🧱 시스템 / 스크립트 구조

| 영역 | 핵심 스크립트 | 역할 |
| --- | --- | --- |
| **앱/모드** | `GameManager`, `ChooseMode_UIManager`, `TitleManager`, `Login_UIManager` | 전역 상태·모드 선택·타이틀·로그인 |
| **센서(BLE)** | `Sensor/SensorManager`, `Protractor`, `OnConnect`, `ConnectAlarm`, `AccelerationManager` | ESP32 연결·각도/중심 계산·연결 경고 |
| **트레이닝** | `Training_AppManager`, `Training_UIManager`, `Training_DataManager` | 루틴 흐름·타이머·기록 |
| **게임** | `Game_AppManager`, `Game_UIManager`, `Game_DataManager` | 게임 진행·판정·보상 |
| **3D 뷰어** | `3DViewMode/MediaPlayer`, `ExerciseDataSet`, `PinchDetection`, `ObjectZoomControls`, `CameraControls`, `ViewTrainingManager` | 프레임 재생·제스처·카메라 |
| **현지화** | `LocaleSelectors`, `LocalizeStringEventManager`, `CSVReader` | 한/영 전환·문자열 관리 |
| **영상/사운드** | `VideoHandle`, `SoundManager`, `SoundCtrl` | 운동 영상·사운드 |
| **플랫폼** | `GooglePlayManager`, `LoadingSceneManager` | Google Play·씬 로딩 |

### 📸 주요 화면

| 화면 | 설명 | 이미지 |
| --- | --- | --- |
| **타이틀** | 불꽃 연출과 로고 | ![타이틀](Screenshots/캡처.PNG) |
| **모드 선택** | 트레이닝·게임·3D 뷰어 선택 | ![모드선택](Screenshots/7.PNG) |
| **레벨 선택** | 초/중/고급 난이도 | ![레벨선택](Screenshots/3.PNG) |
| **트레이닝 진행** | 운동 영상 기반 루틴 가이드 | ![트레이닝](Screenshots/9.PNG) |
| **운동 시연(버드독)** | Bird Dog 자세를 3D 모델로 | ![버드독](Screenshots/10.jpg) |
| **3D 뷰어** | 자세 360도 회전·확대 | ![뷰어](Screenshots/8.PNG) |
| **프로필/리포트** | 운동 기록·뱃지·누적 시간 | ![프로필](Screenshots/1.PNG) |
| **게임 선택** | 3종 미니게임 선택 | ![게임선택](Screenshots/4.PNG) |
| **게임 - Delivery Man** | 균형 유지(좌우 움직임 판정) | ![Delivery](Screenshots/6.PNG) |
| **게임 - Tower Maker** | 블록 쌓기·균형 유지 | ![Tower](Screenshots/5.PNG) |

### 🔗 링크

- 📺 [유튜브 시연 영상](https://www.youtube.com/watch?v=Un5JtJjEnXU)
- 📲 [Google Play 다운로드](https://play.google.com/store/apps/details?id=com.gateways.amazingcore&hl=ko-KR)

### 📁 레포지토리 구성

```
.
├─ AmazingCore/      # 핵심 C# 스크립트 (3DViewMode/, Sensor/, Training·Game·모드·현지화 매니저)
└─ Screenshots/      # 게임 화면
```

> 이 저장소는 **포트폴리오용 코드·자료 모음**입니다(전체 Unity 프로젝트가 아닌 핵심 스크립트·스크린샷 큐레이션).

---

## 🇺🇸 English

### 📘 Overview

**Amazing Core** is a Unity-based **home-fitness content app**. The user wears a **BLE sensor** and performs real core exercises; based on the real-time motion data, three modes run: **Training**, **Game**, and a **3D pose viewer**.

It combines **gamification** with a structured **training system** to boost workout immersion and adherence. I took part in the entire process — planning, design, and development — gaining hands-on, production-level system-building experience.

> Fun like a game, consistent like content — a home-fitness solution that keeps you moving.

### 📊 Project Summary

| | |
| --- | --- |
| **Duration / Role** | **Oct 2022 – Mar 2023 (6 months)** · ~2 mo core development (training/game/3D viewer) + ~4 mo feature expansion/localization/QA<br>Team of 3 (1 planner · 1 designer · 1 developer) — **100% of development** |
| **Platform** | Android (released on Google Play) · dedicated BLE sensor |
| **Tech Stack** | Unity3D (C#) · **VideoPlayer / RenderTexture** (workout/tutorial video) · **BLE(ESP32)** (core posture/motion) · **Unity UI + DOTween** (interaction) · **PlayerPrefs** (history/profile) · **Unity Localization** (KO/EN) · **Cinemachine** (3D viewer/camera) |
| **Key Contributions** | full UI/UX · training routines (7 × 3 levels) · 3 mini-games · 3D pose viewer (pinch/zoom) · BLE integration · local data · localization |

### ✨ Key Features

- 🏃 **BLE-based core-motion recognition** — ESP32 sensor reads posture/balance shifts in real time for training & game judgments (`Sensor/SensorManager`, `Protractor`, `OnConnect`, `AccelerationManager`)
- 🧠 **Training routines (7 × 3 levels)** — beginner/intermediate/advanced; flow of **description → tutorial → main workout → result** (`Training_AppManager`, `Training_UIManager`, `Training_DataManager`)
- 🎮 **3 mini-games** — Tower Maker (stacking), Delivery Man (balance), Wire Walking (tightrope); clearing unlocks puzzle rewards (`Game_AppManager`, `Game_UIManager`, `Game_DataManager`)
- 📦 **3D pose viewer** — plays exercise poses as frame-by-frame 3D models with **pinch/zoom & rotation** (`3DViewMode/MediaPlayer`, `ExerciseDataSet`, `PinchDetection`, `ObjectZoomControls`, `CameraControls`)
- 🌍 **KO/EN localization** — instant switching via Unity Localization (`LocaleSelectors`, `LocalizeStringEventManager`)
- 📈 **Profile & history** — PlayerPrefs-based auto-login and records/badges/cumulative time (`GameManager`, `Login_UIManager`)
- ▶️ **Video guides** — workout/tutorial playback via VideoPlayer/RenderTexture (`VideoHandle`, `MediaPlayer`)

### 🛠️ Engineering Highlights

- **Training flow control** — Coroutine-driven stages (description → tutorial → workout → result), with timer, voice count, and button UI synced.
- **3D pose viewer** — `ExerciseDataSet` (ScriptableObject) presets instantiate frame objects in sequence; touch gestures for zoom/rotate.
- **Sensor guard** — checks BLE state; on disconnect shows a warning and disables buttons (`ConnectAlarm`, `SensorManager`).
- **Interaction polish** — DOTween for button emphasis, slider fills, and smooth UI motion.
- **Persistence** — PlayerPrefs for auto-login and workout history; game-clear records unlock rewards.

### 🎮 Mini-games (3)

| Game | Concept | Core logic |
| --- | --- | --- |
| **Tower Maker** | block stacking | camera height by stack, block Y movement |
| **Delivery Man** | keep balance | left/right tilt judgment, success on reaching goal |
| **Wire Walking** | tightrope | fail when out of range |

### ✅ At a Glance

| Item | Detail |
| --- | --- |
| **Duration** | 6 months (2 mo core + 4 mo expansion/QA) |
| **Contribution** | 100% of development |
| **Training** | 7 types × 3 levels |
| **Games** | Tower Maker · Delivery Man · Wire Walking |
| **BLE** | real-time balance/posture sensing |
| **Localization** | Korean / English |
| **UI** | ~30 screens & popups |
| **Highlights** | real-time feedback · repeatable routines · 3D pose viewer · multilingual |

### 🔁 Flow

```
▶ Login → Mode select
   ├ Training : description → tutorial → workout → clear popup → save data
   ├ Game     : pick game → play → success/fail → puzzle reward
   └ 3D Viewer: frame-based pose playback, zoom/rotate
▶ Profile / records / language switch
```

### 🧱 System / Script Structure

| Area | Key scripts | Role |
| --- | --- | --- |
| **App/Modes** | `GameManager`, `ChooseMode_UIManager`, `TitleManager`, `Login_UIManager` | global state · mode select · title · login |
| **Sensor (BLE)** | `Sensor/SensorManager`, `Protractor`, `OnConnect`, `ConnectAlarm`, `AccelerationManager` | ESP32 connect · angle/balance calc · alerts |
| **Training** | `Training_AppManager`, `Training_UIManager`, `Training_DataManager` | routine flow · timer · records |
| **Game** | `Game_AppManager`, `Game_UIManager`, `Game_DataManager` | gameplay · judgment · rewards |
| **3D Viewer** | `3DViewMode/MediaPlayer`, `ExerciseDataSet`, `PinchDetection`, `ObjectZoomControls`, `CameraControls`, `ViewTrainingManager` | frame playback · gestures · camera |
| **Localization** | `LocaleSelectors`, `LocalizeStringEventManager`, `CSVReader` | KO/EN switching · string management |
| **Video/Sound** | `VideoHandle`, `SoundManager`, `SoundCtrl` | workout video · sound |
| **Platform** | `GooglePlayManager`, `LoadingSceneManager` | Google Play · scene loading |

### 🔗 Links

- 📺 [Gameplay video (YouTube)](https://www.youtube.com/watch?v=Un5JtJjEnXU)
- 📲 [Google Play](https://play.google.com/store/apps/details?id=com.gateways.amazingcore&hl=ko-KR)

### 📁 Repository Layout

```
.
├─ AmazingCore/   # Core C# scripts (3DViewMode/, Sensor/, training·game·mode·localization managers)
└─ Screenshots/   # In-game screens
```

> This repository is a **portfolio curation** of the project's core scripts and screenshots — not the full Unity project.
