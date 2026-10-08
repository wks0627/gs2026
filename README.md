# 열매둥이 흔들기

10초 동안 나무를 연타해서 열매둥이를 수확하는 미니게임.
사내 캐릭터를 그대로 사용하며, 빌드 도구 없이 동작하는 정적 사이트 한 장입니다.

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

## 게임 흐름

접속 → 닉네임 입력 → 난이도 1~5 선택 → 게임 시작 버튼 → 3·2·1 카운트다운 →
10초 플레이 → 성공 시 기분 좋은 인삿말, 실패 시 응원말

## 규칙

- 한 판 10초. 나무를 누를 때마다 "흔들림"이 쌓입니다.
- 흔들림이 일정 수치를 넘으면 열매둥이가 떨어져 바구니에 담기고 1점.
- 손을 멈추면 흔들림이 식습니다. 쉬지 않고 연타해야 합니다.
- 난이도가 올라갈수록 더 많이 흔들어야 하고, 더 빨리 식습니다.
- PC는 클릭, 모바일은 터치, 스페이스바로도 됩니다.

| 난이도 | 열매 1개당 필요 흔들림 | 1초에 식는 양 | 목표 | 체감 |
|---|---|---|---|---|
| 1 아주 쉬움 | 2.0 | 0.4 | 10개 | 초당 3번 |
| 2 쉬움 | 2.4 | 0.8 | 12개 | 초당 4번 |
| 3 보통 | 2.8 | 1.2 | 14개 | 초당 5번 |
| 4 어려움 | 3.2 | 1.5 | 15개 | 초당 6~7번 |
| 5 아주 어려움 | 3.6 | 1.8 | 16개 | 초당 8번 |

결과 화면에 "10초 동안 N번 눌렀어요"가 함께 표시됩니다.

## 수치 조정

난이도는 `index.html`의 `LEVELS` 배열에서 바로 고칠 수 있습니다.
성공/실패 메시지는 같은 파일의 `WIN` / `LOSE` 배열에 있습니다.
나무에 열매가 매달리는 위치는 `SLOTS` 배열입니다.

## GitHub + Vercel 배포

### 방법 A — 웹에서 올리기 (git 설치 불필요, 가장 간단)

1. GitHub 저장소 페이지에서 **Add file → Upload files**를 누릅니다.
2. 이 폴더의 `index.html`, `vercel.json`, `README.md`와 `images` 폴더를
   드래그해서 올리고 Commit 합니다.
3. 이미 Vercel에 연결되어 있다면 커밋과 동시에 자동으로 다시 배포됩니다.

### 방법 B — git 명령으로 올리기

git이 설치되어 있어야 합니다. ([git-scm.com](https://git-scm.com/download/win))

```bash
git init
git add .
git commit -m "열매둥이 흔들기"
git branch -M main
git remote add origin https://github.com/<계정>/<저장소>.git
git push -u origin main
```

Vercel 설정은 Framework Preset **Other**, Build Command와 Output Directory를
비워두면 됩니다.

## 캐릭터 이미지

사내 캐릭터로, 상업적 배포가 아닌 내부용으로만 사용합니다.
