# 🏋️ 스포츠지도사 문제은행

2급 전문스포츠지도사 필기시험 대비 문제은행 웹 애플리케이션

## 📌 주요 기능

### ✅ 구현 완료
- **문제풀이**: 2016~2025년도 기출문제 (7개 과목)
- **요점정리**: 과목별 핵심 요약 + 빈출 TOP 20 + 챕터별 토픽
- **배틀모드**: 실시간 대전형 퀴즈 (battle.html)
- **한국체육사 300제**: 별도 문제은행
- **동영상강의 연동** (NEW):
  - 한국체육사 빈출 TOP20 펼침 시 YouTube 강의 링크 (상/중/하)
  - 스포츠교육학 빈출 TOP20 펼침 시 YouTube 강의 링크 (상/중/하)
- PWA 지원 (manifest.json, 홈 화면 추가 가능)

### 📂 파일 구조
```
index.html          - 메인 앱 (문제풀이 + 요점정리)
battle.html         - 배틀모드
manifest.json       - PWA 매니페스트
images/
  └── knsu-mascot.png  - 앱 아이콘/마스코트
data/
  ├── 2016.json ~ 2025.json  - 연도별 기출문제
  └── 한국체육사300.json       - 한국체육사 300제
```

### 🎬 동영상강의 YouTube 링크
| 과목 | 구분 | YouTube URL |
|------|------|-------------|
| 한국체육사 | 상 | https://youtu.be/l82SXYXABVQ |
| 한국체육사 | 중 | https://youtu.be/Gd98OLo9bXU |
| 한국체육사 | 하 | https://youtu.be/9zPDQ7SS1V4 |
| 스포츠교육학 | 상 | https://youtu.be/r9WV7X6iP9w |
| 스포츠교육학 | 중 | https://youtu.be/ZzrILTJuNaQ |
| 스포츠교육학 | 하 | https://youtu.be/y9nq_NHzL-U |

### 🔗 진입 경로
- `index.html` - 메인 페이지 (문제풀이 / 요점정리 탭)
- `battle.html` - 배틀모드
- 요점정리 → 과목 선택 → 빈출 TOP 펼치기 → 동영상강의 버튼

### 🚀 향후 개발 권장사항
- 나머지 과목(스포츠심리학, 스포츠사회학, 운동생리학, 운동역학, 스포츠윤리)에도 동영상강의 추가
- 오답노트 기능
- 학습 통계 대시보드
