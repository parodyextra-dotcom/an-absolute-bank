# 🏋️ 스포츠지도사 문제은행

2급 전문스포츠지도사 필기시험 대비 문제은행 웹앱 (PWA)

## 📌 프로젝트 개요

- **목표**: 2016~2025년 기출문제 기반 스포츠지도사 필기시험 학습 도구
- **7과목**: 스포츠사회학, 스포츠교육학, 스포츠심리학, 한국체육사, 운동생리학, 운동역학, 스포츠윤리
- **기출문제**: 10개 연도 × 7과목 × 20문항 = 약 1,400+ 문항

---

## ✅ 구현 완료 기능

### 1. 메인 문제풀이 (index.html)
- 연도별/과목별 기출문제 풀이
- 오답노트, 요점정리 보기
- 학습 진도 관리 (localStorage)
- PWA 지원 (홈 화면 추가 가능)

### 2. ⚔️ 배틀 모드 (battle.html) - Firebase 연동 완료
- **Firebase Firestore 실시간 동기화**
  - 방 만들기 / 참가하기 (4자리 코드)
  - 최대 4인 동시 대결
  - `onSnapshot` 리스너로 실시간 플레이어 상태 동기화
  - 실시간 점수판 업데이트
- **게임 흐름**
  - 방장: 과목 선택 → 문제 수 선택 (5/10/15/20) → 게임 시작
  - 참가자: 방 코드 입력 → 실시간 대기 → 자동 게임 시작
  - 카운트다운 (3-2-1) 후 게임 시작
  - 문항당 60초 타이머
  - 정답/오답 즉시 피드백 + 해설 표시
- **결과 화면**
  - 점수 기반 랭킹 (동점 시 평균 응답시간 기준)
  - 1등: 역도 스내치 마스코트 / 하위: 실패 마스코트
  - "한판 더!" 기능 (방장)

---

## 📂 프로젝트 구조

```
index.html              # 메인 문제풀이 앱
battle.html             # 배틀모드 (Firebase 실시간 대전)
manifest.json           # PWA 매니페스트
data/
  ├── 2016.json         # 2016년 기출문제
  ├── 2017.json
  ├── 2018.json
  ├── 2019.json
  ├── 2020.json
  ├── 2021.json
  ├── 2022.json
  ├── 2023.json
  ├── 2024.json
  ├── 2025.json         # 2025년 기출문제
  └── 요점정리.txt       # 전과목 요점정리
images/
  ├── knsu-mascot.png           # KNSU 마스코트 (메인)
  ├── knsu-mascot-snatch.png    # 역도 스내치 (승리 시)
  └── knsu-mascot-fail.png      # 실패 포즈 (패배 시)
```

---

## 🔗 URI 경로

| 경로 | 설명 |
|------|------|
| `/index.html` | 메인 페이지 (문제풀이, 요점정리, 학습 관리) |
| `/battle.html` | 배틀모드 (Firebase 실시간 대전) |
| `/data/{year}.json` | 연도별 기출문제 JSON 데이터 |
| `/manifest.json` | PWA 매니페스트 |

---

## 🔥 Firebase 설정

### 사용 서비스
- **Firebase Firestore**: 실시간 배틀 데이터 동기화

### Firestore 데이터 구조

```
rooms (컬렉션)
  └── {roomId} (문서)
      ├── room_code: string (4자리 방코드)
      ├── host_id: string (방장 플레이어 ID)
      ├── subject: string (선택 과목)
      ├── status: "waiting" | "playing" | "finished"
      ├── questions: array (문제 배열)
      ├── question_count: number (5/10/15/20)
      ├── max_players: 4
      ├── created_at: timestamp
      ├── started_at: timestamp
      ├── finished_at: timestamp
      └── players (서브컬렉션)
          └── {playerId} (문서)
              ├── player_id: string
              ├── nickname: string
              ├── avatar: string (이모지)
              ├── is_host: boolean
              ├── score: number
              ├── answers: array
              ├── is_connected: boolean
              ├── joined_at: timestamp
              └── last_ping: timestamp
```

### ⚠️ Firestore 보안 규칙 (반드시 설정 필요!)

Firebase 콘솔 > Firestore Database > Rules 에서 다음 규칙을 설정하세요:

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    // 배틀 방 - 누구나 읽기/쓰기 가능 (공개 게임)
    match /rooms/{roomId} {
      allow read, write: if true;
      
      // 플레이어 서브컬렉션
      match /players/{playerId} {
        allow read, write: if true;
      }
    }
  }
}
```

> **참고**: 프로덕션 환경에서는 더 엄격한 보안 규칙을 적용하는 것이 좋습니다.

### Firebase 프로젝트 정보
- **Project ID**: `battle-4975c`
- **Auth Domain**: `battle-4975c.firebaseapp.com`

---

## 🛠️ 기술 스택

- **HTML5 / CSS3 / Vanilla JavaScript**
- **Firebase Firestore** (실시간 데이터 동기화)
- **Firebase Compat SDK** v10.12.2 (CDN)
- **Font Awesome** 6.5.0 (아이콘)
- **Google Fonts** - Noto Sans KR
- **PWA** (Service Worker, Manifest)

---

## 🔮 향후 개발 추천 사항

1. **Firebase Authentication** 도입 - 사용자 인증 및 보안 규칙 강화
2. **전적 시스템** - 배틀 결과 영구 저장 및 통계
3. **오래된 방 자동 정리** - Cloud Functions로 일정 시간 후 방 삭제
4. **채팅 기능** - 배틀 중 간단한 이모지 채팅
5. **관전 모드** - 진행 중인 배틀 관전
6. **Service Worker** - 오프라인 지원 강화
