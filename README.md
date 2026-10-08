# 열매둥이 잡기

30초 두더지 잡기 미니게임. 사내 캐릭터를 두더지로 사용합니다.
빌드 도구 없이 동작하는 정적 사이트 한 장입니다.

## 구조

```
index.html                     게임 전체 (HTML + CSS + JS + 캐릭터 이미지)
vercel.json                    정적 배포 설정 (이미지 캐시)
README.md                      이 문서
.gitignore
images/mole-a.png              캐릭터 - 왼쪽
images/mole-b.png              캐릭터 - 가운데 (꽃다발)
images/mole-c.png              캐릭터 - 오른쪽
images/characters-original.png 원본 3종 일러스트
```

캐릭터 이미지는 `index.html` 안에 base64로 내장되어 있습니다.
따라서 배포에 꼭 필요한 파일은 `index.html` 하나뿐이고,
`images/` 폴더는 나중에 캐릭터를 교체하거나 다른 곳에 쓰기 위한 원본 보관용입니다.

## 로컬에서 보기

`index.html`을 브라우저로 열면 바로 실행됩니다. 서버가 필요 없습니다.

## 게임 규칙

- 한 판 30초, 3×3 구멍에서 캐릭터가 올라옵니다.
- 올라온 캐릭터를 누르면 1점.
- 난이도별 목표 개수를 채우면 성공, 못 채우면 실패.

| 난이도 | 올라와 있는 시간 | 출현 간격 | 동시 최대 | 목표 |
|---|---|---|---|---|
| 1 아주 쉬움 | 1.50초 | 0.90초 | 1 | 10개 |
| 2 쉬움 | 1.20초 | 0.75초 | 1 | 14개 |
| 3 보통 | 1.00초 | 0.60초 | 2 | 20개 |
| 4 어려움 | 0.80초 | 0.47초 | 2 | 26개 |
| 5 아주 어려움 | 0.65초 | 0.36초 | 3 | 34개 |

난이도 수치는 `index.html`의 `LEVELS` 배열에서 바로 조정할 수 있습니다.
성공/실패 메시지는 같은 파일의 `WIN` / `LOSE` 배열에 있습니다.

## GitHub + Vercel 배포

### 방법 A — 웹에서 올리기 (git 설치 불필요, 가장 간단)

1. [github.com/new](https://github.com/new)에서 저장소를 만듭니다.
   (README 추가 옵션은 체크하지 않습니다.)
2. 만들어진 화면에서 **uploading an existing file** 링크를 누릅니다.
3. 이 폴더의 `index.html`, `vercel.json`, `README.md`와 `images` 폴더를
   드래그해서 올리고 Commit 합니다.
4. [vercel.com/new](https://vercel.com/new)에서 그 저장소를 Import 합니다.

### 방법 B — git 명령으로 올리기

git이 설치되어 있어야 합니다. ([git-scm.com](https://git-scm.com/download/win))

```bash
git init
git add .
git commit -m "열매둥이 잡기 미니게임"
git branch -M main
git remote add origin https://github.com/<계정>/<저장소>.git
git push -u origin main
```

그다음 [vercel.com/new](https://vercel.com/new)에서 저장소를 Import 합니다.
빌드 설정은 그대로 두면 됩니다 (Framework Preset: **Other**, Build Command 비움,
Output Directory 비움). Deploy를 누르면 끝이고, 이후 `main`에 푸시할 때마다
자동으로 다시 배포됩니다.

## 캐릭터 이미지

사내 캐릭터로, 상업적 배포가 아닌 내부용으로만 사용합니다.
