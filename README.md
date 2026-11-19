# TeamCP Games website

TeamCP 게임의 공식 정보와 공개 문서를 관리하는 GitHub Pages 저장소다.

## 방침 화면 생성 공통 규칙 (POLICY-MOBILE)

14개 방침 생성기는 `tools/policy-style.mjs`로 게임별 `policy.css`를 HTML 안에 넣는다.
별도 CSS 요청이 지연되어 첫 화면을 막는 의존성을 없앴다. 밝은 방침은 `color-scheme: only light`,
어두운 방침은 기존 `dark`와 색상을 유지한다. 원문 JSON과 본문·언어 링크는 바꾸지 않는다.
수정 후 해당 생성기의 `--check`, `node tools/check-policy-render.mjs`를 실행한다.
게시 후 `node tools/check-policy-render.mjs --live`는 전체 97개 방침의 HTTP 200과 소스 일치를 확인한다.
이 검사는 모바일 화면 판정을 대신하지 않는다. POLICY-MOBILE의 실제 기기 전후 판정은 아직 미검증이다.

## 구조

- `/index.html`: 전체 게임 목록과 공식 지원 허브
- `/games/<game-slug>/index.html`: 게임별 소개 페이지
- `/games/<game-slug>/privacy/index.html`: 게임별 개인정보처리방침
- `/app-ads.txt`: 출시 앱의 광고 판매자 인증 파일

현재 등록된 게임:

- 고양이 오목 (`com.teamcp.catgomoku`)
- 냥탐정 (`com.teamcp.catdetective`)
- 슬라임 택배 (`com.teamcp.slimeexpress`)
- DEAD FREQUENCY (`com.teamcp.deadfrequency`)
- 3분 냥냥 던전 (`com.teamcp.catrush3`)
- 인디 개발 타이쿤 (`com.teamcp.indiedevtycoon`)
- 냥냥 해적단: 야식 대작전 (`com.teamcp.catpirates`)
- 냥이 합치기 (`com.teamcp.nyangmerge`)
- 냥이 츄르 버스 (`com.teamcp.nyanchurubus`)
- 냥냥 도시락 공장 (`com.teamcp.catbentosort`)
- 냥이 털실 풀기 (`com.teamcp.yarntangle`)
- 냥냥 길 비켜 (`com.teamcp.catwayout`)
- 냥냥 고리 돌리기 (`com.teamcp.catringtwist`)

## 냥탐정 개인정보처리방침

한국어 기본 URL과 `#delete-data` 앵커를 유지한다. 영어·일본어·스페인어·프랑스어·독일어는
`/games/cat-detective/privacy/{en,ja,es,fr,de}/`에 제공한다. HTML은 JavaScript 없이 읽을 수 있다.
`tools/privacy/*.json`에서 수정하고 `node tools/build-cat-privacy.mjs`로 정적 페이지를 생성한다.
`node tools/build-cat-privacy.mjs --check` 및 `node tools/check-cat-privacy.mjs`로 생성 누락·경로·삭제 앵커를 검사한다.
승인된 게시 뒤 `node tools/check-cat-privacy.mjs --live`로 공개 6개 페이지와 CSS를 소스와 대조한다.
`--local`은 별도로 실행한 `127.0.0.1:8765` 미리보기만 검사한다. 어느 명령도 게시·사용자 데이터 변경을 수행하지 않는다.
번역은 자동 전수 법률 인증이 아니다. 실제 버전의 기능/SDK와 운영자 사실을 확인하고 갱신한다.

새 게임을 추가할 때는 게임 소개와 개인정보처리방침을 같은 디렉터리에 추가하고 루트 `index.html`에 게임 카드를 연결한다. 광고 사업자를 추가할 때는 해당 대시보드에서 발급·검증된 판매자 정보만 `app-ads.txt`에 반영한다.

## DEAD FREQUENCY 개인정보처리방침

한국어 기본 URL `/games/dead-frequency/privacy/`와 `#delete-data` 앵커를 유지하고, 영어·일본어·스페인어·프랑스어·독일어는 `/games/dead-frequency/privacy/{en,ja,es,fr,de}/`에 둔다.
`tools/privacy-dead-frequency/*.json`에서 수정하고 `node tools/build-dead-frequency-privacy.mjs`로 생성한다 (`--check`로 누락 확인).
광고 구성(Unity LevelPlay + Unity Ads), Android 자동 백업 허용, 앱 내 광고 개인화 선택 없음을 기준으로 작성했다. 앱 동작이 바뀌면 함께 갱신한다.

## 인디 개발 타이쿤 개인정보처리방침

한국어 기본 URL `/games/indie-dev-tycoon/privacy/`와 `#delete-data` 앵커를 유지하고, 영어는 `/games/indie-dev-tycoon/privacy/en/`에 둔다(게임 지원 언어와 동일).
`tools/privacy-indie-dev-tycoon/*.json`에서 수정하고 `node tools/build-indie-dev-tycoon-privacy.mjs`로 생성한다 (`--check`로 누락 확인).
광고 구성(Unity LevelPlay + Unity Ads, 17+ 광고 제한), 모든 이용자 대상 첫 실행 맞춤 광고 동의(선택 전 SDK 미시작), Android 자동 백업 허용을 기준으로 작성했다. 앱 동작이 바뀌면 함께 갱신한다.

## 냥냥 해적단 개인정보처리방침

한국어 기본 URL `/games/cat-pirates/privacy/`와 `#delete-data` 앵커를 유지하고, 영어는 `/games/cat-pirates/privacy/en/`에 둔다(게임 UI는 한국어).
`tools/privacy-cat-pirates/*.json`에서 수정하고 `node tools/build-cat-pirates-privacy.mjs`로 생성한다 (`--check`로 누락 확인).
광고 구성(Unity LevelPlay + Unity Ads, 보상형·전면, 배너 없음, 어린이 대상 아님), 모든 이용자 대상 첫 실행 맞춤 광고 동의(선택 전 SDK 미시작, 설정에서 변경), Google Play 게임즈 v2 자동 로그인·업적·리더보드(클라우드 저장 없음), Room + DataStore 기기 저장, Android 자동 백업 허용, 앱 내 결제 없음을 기준으로 작성했다. 앱 동작이 바뀌면 함께 갱신한다. 2026-11-19(PIR-REPORT): 설정의 오류 신고(이용자가 직접 보낼 때만 전송, Cafe24 호스팅 서버 보관 90일, 미전송분 기기 보관·백업 제외, 이메일 삭제 요청)를 7절로 추가하고 ‘오류 보고 도구가 없다’·‘게임 서버가 없다’는 옛 문구를 고쳤다.

## 냥이 합치기 개인정보처리방침

한국어 기본 URL `/games/nyang-merge/privacy/`와 `#delete-data` 앵커를 유지하고, 영어는 `/games/nyang-merge/privacy/en/`에 둔다.
`tools/privacy-nyang-merge/*.json`에서 수정하고 `node tools/build-nyang-merge-privacy.mjs`로 생성한다 (`--check`로 누락 확인).
계정·로그인·서버 없는 기기 저장, Google Play 게임즈 없음, 광고 구성(Unity LevelPlay + Unity Ads, 배너·전면·보상형), 모든 이용자 대상 첫 실행 맞춤 광고 동의(선택 전 SDK 미시작·광고 없음, 설정에서 다시 선택), Android 자동 백업 허용, 앱 내 결제 없음을 기준으로 작성했다. 앱 동작이 바뀌면 함께 갱신한다. 2026-11-19(NM-QA5FIX): 설정의 오류 신고(이용자가 직접 보낼 때만 전송, Cafe24 호스팅 서버 보관 90일, 미전송분 기기 보관)를 7절로 추가하고 ‘오류 보고 도구가 없다’·‘서버에 보관하는 정보가 없다’는 옛 문구를 고쳤다.

## 냥이 츄르 버스 개인정보처리방침

한국어 기본 URL `/games/nyan-churu-bus/privacy/`와 `#delete-data` 앵커를 유지하고, 게임과 같은 8개 언어(영어·일본어·스페인어·포르투갈어(브라질)·중국어(번체)·독일어·프랑스어)는 `/games/nyan-churu-bus/privacy/{en,ja,es,pt-br,zh-tw,de,fr}/`에 둔다. 앱 설정·첫 실행 동의 카드의 방침 버튼이 앱 언어의 경로를 연다(앱 저장소 ads 모듈의 `PrivacyLinks`).
`tools/privacy-nyan-churu-bus/*.json`에서 수정하고 `node tools/build-nyan-churu-bus-privacy.mjs`로 생성한다 (`--check`로 누락 확인, 절 id·`#delete-data` 1개·금지 이름 검사 포함).
계정·로그인 없는 기기 저장(progress.json·설정), Android 자동 백업 꺼짐(allowBackup=false), 광고 구성(Unity LevelPlay + Unity Ads, 배너·전면·보상형 간식 찬스, 자체 배너는 탭할 때만 사이트 열기), 모든 이용자 대상 첫 실행 맞춤 광고 동의(선택 전 SDK 미시작, 설정에서 다시 선택), 설정에서 이용자가 직접 보내는 오류 신고(설명·앱·버전·화면·언어·기기 모델, TeamCP 신고 서버·Cafe24), 앱 내 결제 없음을 기준으로 작성했다(앱 1.0.0, 2026-11-18). 앱 동작이 바뀌면 함께 갱신한다.

## 냥냥 도시락 공장 개인정보처리방침

한국어 기본 URL `/games/cat-bento-sort/privacy/`와 `#delete-data` 앵커를 유지하고, 게임과 같은 8개 언어(영어·일본어·스페인어·포르투갈어(브라질)·중국어(번체)·독일어·프랑스어)는 `/games/cat-bento-sort/privacy/{en,ja,es,pt-br,zh-tw,de,fr}/`에 둔다. 앱 설정의 방침 버튼이 앱 언어의 경로를 연다(앱 저장소 `tools/strings.csv`의 `privacy_url`).
`tools/privacy-cat-bento-sort/*.json`에서 수정하고 `node tools/build-cat-bento-sort-privacy.mjs`로 생성한다 (`--check`로 누락 확인, 절 id·`#delete-data` 1개·금지 이름 검사 포함).
계정·로그인 없는 기기 저장, Android 자동 백업 꺼짐(allowBackup=false), 광고 구성(Unity LevelPlay + Unity Ads, 배너·전면·보상형 냥이 찬스, 자체 배너는 탭할 때만 사이트 열기), 모든 이용자 대상 첫 실행 맞춤 광고 동의(선택 전 SDK 미시작, 설정에서 다시 선택), 설정에서 이용자가 직접 보내는 오류 신고(설명·앱·버전·화면·언어·기기 모델, TeamCP 신고 서버·Cafe24), 앱 내 결제 없음을 기준으로 작성했다(앱 1.0.0, 2026-11-17). 앱 동작이 바뀌면 함께 갱신한다.

## 냥이 털실 풀기 개인정보처리방침

한국어 기본 URL `/games/yarn-tangle-cats/privacy/`와 `#delete-data` 앵커를 유지하고, 게임과 같은 8개 언어(영어·일본어·스페인어·포르투갈어(브라질)·중국어(번체)·독일어·프랑스어)는 `/games/yarn-tangle-cats/privacy/{en,ja,es,pt-br,zh-tw,de,fr}/`에 둔다. 앱 설정·첫 실행 동의 카드의 방침 버튼이 앱 언어의 경로를 연다(앱 저장소 `tools/strings.csv`의 `privacy_url`).
`tools/privacy-yarn-tangle-cats/*.json`에서 수정하고 `node tools/build-yarn-tangle-cats-privacy.mjs`로 생성한다 (`--check`로 누락 확인, 절 id·`#delete-data` 1개·금지 이름 검사 포함).
계정·로그인 없는 기기 저장(progress.json·설정), Android 자동 백업 꺼짐(allowBackup=false), 광고 구성(Unity LevelPlay + Unity Ads, 배너·전면·보상형 냥이 가위 찬스, 자체 배너는 탭할 때만 사이트 열기), 모든 이용자 대상 첫 실행 맞춤 광고 동의(선택 전 SDK 미시작, 설정에서 다시 선택), 설정에서 이용자가 직접 보내는 오류 신고(설명·앱·버전·화면·언어·기기 모델, TeamCP 신고 서버·Cafe24), 앱 내 결제 없음을 기준으로 작성했다(앱 1.0.0, 2026-11-18). 앱 동작이 바뀌면 함께 갱신한다. 첫 화면 카드는 아직 없다(출시 시 추가).


## 냥냥 길 비켜 개인정보처리방침

한국어 기본 URL은 `/games/cat-way-out/privacy/`입니다. 영어·일본어·스페인어·포르투갈어(브라질)·중국어(번체)·독일어·프랑스어 페이지에도 데이터 삭제 안내 앵커 `#delete-data`가 있습니다. `tools/privacy-cat-way-out/*.json`에서 원문을 관리하며 `node tools/build-cat-way-out-privacy.mjs`로 정적 페이지를 생성합니다. `--check`로 생성 결과를 검증합니다.

## 냥냥 고리 돌리기 개인정보처리방침

한국어 기본 URL `/games/cat-ring-twist/privacy/`와 `#delete-data` 앵커를 유지하고, 게임과 같은 8개 언어(영어·일본어·스페인어·포르투갈어(브라질)·중국어(번체)·독일어·프랑스어)는 `/games/cat-ring-twist/privacy/{en,ja,es,pt-br,zh-tw,de,fr}/`에 둔다. 앱 설정·첫 실행 동의 카드의 방침 버튼이 앱 언어의 경로를 연다(앱 저장소 `tools/strings.csv`의 `privacy_url`).
`tools/privacy-cat-ring-twist/*.json`에서 수정하고 `node tools/build-cat-ring-twist-privacy.mjs`로 생성한다 (`--check`로 누락 확인, 절 id·`#delete-data` 1개·금지 이름 검사 포함). 양식은 냥이 털실 풀기 방침과 같다.
계정·로그인 없는 기기 저장(진행 JSON·설정), Android 자동 백업 꺼짐(allowBackup=false), 광고 구성(Unity LevelPlay + Unity Ads, 배너·`다음 레벨` 뒤 전면·보상형 힌트, 자체 배너는 탭할 때만 사이트 열기), 모든 이용자 대상 첫 실행 맞춤 광고 동의(선택 전 SDK 미시작, 설정에서 다시 선택), 설정에서 이용자가 직접 보내는 오류 신고(설명·앱·버전·화면·언어·기기 모델, TeamCP 신고 서버·Cafe24, 보관 90일), 앱 내 결제 없음을 기준으로 작성했다(앱 1.0.0, 2026-11-19 RING-QAFIX1). 앱 동작이 바뀌면 함께 갱신한다. 첫 화면 카드는 아직 없다(출시 시 추가).

## 냥이랑 한글 개인정보처리방침

한국어 기본 URL `/games/meow-hangul/privacy/`와 `#delete-data` 앵커를 유지하고, 앱과 같은 8개 언어(영어·일본어·스페인어·포르투갈어(브라질)·중국어(번체)·독일어·프랑스어)는 `/games/meow-hangul/privacy/{en,ja,es,pt-br,zh-tw,de,fr}/`에 둔다. 앱(`com.teamcp.meowhangul`)은 아직 출시 전이라 게임 소개 페이지와 첫 화면 카드가 없고 위 ‘현재 등록된 게임’ 목록에도 넣지 않았다(출시 시 추가). 방침 페이지의 돌아가기 링크는 첫 화면(`/`)으로 간다.
`tools/privacy-meow-hangul/*.json`에서 수정하고 `node tools/build-meow-hangul-privacy.mjs`로 생성한다 (`--check`로 누락 확인, 절 id·`#delete-data` 1개 검사 포함). 양식은 냥냥 고리 돌리기 방침과 같고 ‘음성과 마이크’ 절(`voice`)이 하나 더 있다.
계정·로그인 없는 기기 저장(학습 진행·복습 일정·설정), Android 자동 백업 꺼짐(allowBackup=false), 선택 기능 ‘듣고 따라 하기’의 마이크(처음 녹음을 누를 때만 권한 요청, 최대 15초 임시 녹음 1개, 업로드·채점·음성 인식 없음, 벗어나면 삭제), 미리 만든 AI 음성(Supertonic 3), 광고 구성(Unity LevelPlay + Unity Ads·ironSource, AdMob·UMP·Firebase 없음, 배너·결과 화면을 떠날 때의 전면·보상형 힌트/다시 풀기/보너스 복습, 자체 배너는 탭할 때만 사이트 열기), 모든 이용자 대상 첫 실행 맞춤 광고 동의(선택 전 SDK 미시작, 설정에서 다시 선택, 거부 시 do-not-sell), 문제·결과 화면과 설정에서 이용자가 직접 보내는 오류 신고(설명·분류·앱 버전·화면·문제 ID·보이는 문구·언어·기기 모델·신고 번호, TeamCP 신고 서버·Cafe24, 보관 90일, 미전송분 기기 보관 최대 100건), 앱 내 결제 없음을 기준으로 작성했다(앱 1.0.0, 2026-11-19 MH-QA3FIX). 앱 동작이 바뀌면 함께 갱신한다.
