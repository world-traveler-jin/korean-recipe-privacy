# 한식 레시피 (Korean Recipes) — 공개 정적 파일

공개 주소: https://world-traveler-jin.github.io/korean-recipe-privacy/

## index.html — 개인정보처리방침

Google Play · App Store 등록용 페이지입니다. 원본은 앱 저장소의
`docs/PRIVACY-POLICY.md` (영문판 `docs/PRIVACY-POLICY.en.md`) 이고,
게시용 HTML 은 앱 저장소의 `docs/privacy-site/index.html` 를 그대로 복사한
것입니다. **방침을 고칠 때는 앱 저장소에서 고치고 여기로 복사합니다.**

## dataset/ — 레시피 데이터 업데이트

앱이 스토어를 거치지 않고 레시피 데이터만 받아 갈 수 있게 둔 정적 파일입니다.
서버가 아니라 GitHub Pages 이므로 우리 쪽 로그도 계정도 없습니다.

| 파일 | 내용 |
| --- | --- |
| `dataset/latest.json` | 어떤 판이 최신인지 알려 주는 목록. 앱이 먼저 읽는 파일 |
| `dataset/recipes-<버전>.json` | 레시피 데이터 본문 |

**앱이 접속하는 유일한 주소가 `dataset/latest.json` 입니다.** 그리고 사용자가
설정에서 「업데이트 확인」을 직접 누를 때만 읽습니다.

올리는 방법과 `latest.json` 의 모양은 앱 저장소의 `docs/10-DATASET-UPDATE.md`
에 적어 두었습니다. 파일은 `data-pipeline/publish_dataset_update.py` 가 앱에
들어 있는 바이트를 그대로 복사해 만듭니다 — 다시 직렬화하지 않으므로 앱 번들과
sha256 이 같습니다.

### 주의

- `latest.json` 의 `sha256` 과 `sizeBytes` 가 본문 파일과 **반드시** 맞아야
  합니다. 어긋나면 앱이 받은 파일을 버리고 번들 데이터를 씁니다(그렇게
  설계했습니다). 스크립트가 둘을 함께 만들므로 손으로 고치지 마십시오.
- 본문 파일은 지우지 않고 쌓습니다. 받다가 끊긴 사용자가 다시 받을 수 있어야
  하고, 파일 하나가 10MB 아래라 쌓아 둬도 괜찮습니다.
- `.nojekyll` 은 Pages 가 파일을 건드리지 않게 두는 표시입니다. 지우지 마십시오.
