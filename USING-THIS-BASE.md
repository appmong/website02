# 이 폴더는 "공통 베이스"예요

애드센스 승인용 정보 콘텐츠 사이트의 재사용 템플릿입니다.
새 사이트를 만들 때마다 **이 폴더를 복사 → 이름·도메인만 바꿔치기 → 콘텐츠 채우기** 순서로 찍어내면 돼요.

포함된 것: 신뢰 장치 컴포넌트, 필수 페이지(about/contact/privacy/terms), sitemap/RSS/robots/ads.txt,
체류 장치(포춘쿠키·구독폼·읽기진행바·맨위로), 한글 슬러그 URL 구조.
콘텐츠는 예시 1편만 들어 있어요(`src/content/posts/재산세-이의신청-기한.md` — 새 글 쓸 때 복제할 견본).

---

## 새 사이트 하나 찍어내기

### 1) 폴더 복사

원하는 위치로 이 폴더를 통째로 복사해요. 예:

```powershell
robocopy E:\base_project E:\sites\새사이트 /E /XD node_modules dist .astro
```

### 2) 이름·도메인 넣기 (스크립트가 3곳을 자동 수정)

복사한 폴더에서:

```bash
node scripts/new-site.mjs --name "사이트이름" --url "도메인.com" --email "hello@도메인.com"
```

- `--name` 사이트 브랜드명 (필수)
- `--url` 도메인 — `http(s)://` 없이 넣어도 됨 (필수)
- `--email` 대표 이메일 (생략하면 `hello@도메인` 자동)

이 스크립트가 `src/site.config.ts`, `astro.config.mjs`, `public/robots.txt`의 도메인/이름/이메일을 한 번에 바꿔줘요.

### 3) 니치·저자 손보기 (선택)

`src/site.config.ts`에서:
- `CATEGORIES` — 카테고리(니치). 지금은 정부지원금·세금 등 8개 플레이스홀더
- `AUTHORS` — 필명·경력 한 줄(저자 박스). **승인 신뢰도의 핵심이라 실제 경험을 걸 수 있게 채우기**
- `FORTUNE_NOTES` — "오늘의 쪽지" 문구
- `EDITORIAL_PRINCIPLES` — about 페이지 편집 원칙

### 4) 설치 & 실행

```bash
npm install
npm run dev      # 개발 서버 http://localhost:4321
npm run build    # 프로덕션 빌드 → dist/
```

### 5) 승인 준비되면 나중에 채우는 값

`src/site.config.ts`:
- `VERIFICATION.google` / `VERIFICATION.naver` — Search Console·네이버 웹마스터 인증 메타값
- `ADSENSE.clientId` — `ca-pub-XXXX` (애드센스 발급 후). 넣으면 광고 스크립트와 `/ads.txt`가 자동 활성화

---

## 참고
- Node가 없으면: `winget install OpenJS.NodeJS.LTS`
- 이 PC에서 미리보기가 안 뜨면 `node`가 PATH에 없을 수 있어요. 새 터미널을 열거나 `C:\Program Files\nodejs\`를 PATH에 추가하세요.
- 자세한 프로젝트 구조·글 작성법은 `README.md` 참고.
