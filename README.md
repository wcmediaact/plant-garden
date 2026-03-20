# 나의 AI 식물 정원 — PWA 배포 가이드

## 파일 구조
```
plant-pwa/
├── index.html       ← 게임 전체 (빌드 불필요)
├── manifest.json    ← PWA 설정
├── sw.js            ← 서비스 워커 (오프라인 지원)
├── vercel.json      ← Vercel 배포 설정
├── icons/
│   ├── icon-192.png ← 앱 아이콘 (192×192px)
│   └── icon-512.png ← 앱 아이콘 (512×512px)
└── README.md
```

---

## Step 1 — 아이콘 준비

`icons/` 폴더를 만들고 PNG 이미지 2개를 넣어주세요.
- `icon-192.png` : 192×192 픽셀
- `icon-512.png` : 512×512 픽셀

무료 도구: https://realfavicongenerator.net  
(식물 이모지 🪴 또는 직접 그린 캐릭터 사용 가능)

---

## Step 2 — API 키 임시 설정 (테스트 전용)

`index.html` 맨 아래 부분을 찾아 수정:

```html
<!-- 이 줄의 주석을 해제하고 실제 키를 입력 -->
window.__ANTHROPIC_KEY__ = 'sk-ant-xxxxxxxx';
```

⚠️ 이 방법은 로컬 테스트 전용입니다.
실제 배포 전에 반드시 Firebase Cloud Functions로 교체해야 합니다.
(키가 노출되면 무제한 과금 발생 가능)

---

## Step 3 — Vercel 배포

### 방법 A (GitHub 연동 — 추천)
1. GitHub 계정 생성 → 새 저장소(Repository) 생성
2. 이 폴더의 파일들을 저장소에 업로드
3. vercel.com 접속 → GitHub 계정 연동
4. "New Project" → 저장소 선택 → Deploy 클릭
5. 자동으로 도메인 생성됨 (예: plant-garden.vercel.app)

### 방법 B (드래그 앤 드롭)
1. vercel.com/new 접속
2. 폴더 전체를 드래그 앤 드롭
3. 즉시 배포됨

---

## Step 4 — 모바일에서 테스트

배포 URL을 스마트폰 브라우저로 열면:
- Android Chrome: "홈 화면에 추가" 프롬프트 자동 표시
- iPhone Safari: 공유 버튼 → "홈 화면에 추가" 수동 선택

홈 화면에서 아이콘으로 실행하면 앱처럼 동작합니다.

---

## 다음 단계 (Phase 2)

PWA 테스트 후 실제 앱스토어 출시를 위한 Capacitor 래핑:
- Capacitor.js 설치 → iOS/Android 빌드 파일 생성
- Firebase 연동 → API 키 보안 + 클라우드 저장
- TestFlight(iOS) / Play Console(Android) 내부 테스트

---

## 비용 예상

| 항목 | 비용 |
|---|---|
| Vercel 호스팅 | 무료 |
| Claude Haiku 4.5 API | 대화 1만 건 기준 약 ₩1,000~3,000/월 |
| Firebase (소규모) | 무료 (Spark Plan) |
| Apple Developer 등록 | $99/년 (₩약 135,000) |
| Google Play 등록 | $25 일회성 |
