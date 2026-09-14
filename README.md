# LGD Production & Quality Report Dashboard

## 제목

**LG디스플레이 생산·품질 보고서 웹 서비스**

LG디스플레이 직무 이해 및 생산·품질 관리 업무 학습을 목적으로 제작한 교육용 웹 프로젝트입니다.

생산 실적과 목표 수량, 검사 수량, 불량 데이터를 조회하고 이를 기반으로 생산 달성률과 불량률을 확인할 수 있습니다. 또한 Three.js를 이용한 패널 검사·이송 설비의 3D 시각화와 생산·품질 보고서 작성 및 저장 기능을 제공합니다.

---

## 날짜

**2026년 09월 14일**

---

## 사용 라이브러리 및 기술

### Backend

* Python
* Flask
* Werkzeug
* JSON
* Threading
* Asyncio

### Frontend

* HTML5
* CSS3
* JavaScript
* Fetch API

### 3D Visualization

* Three.js
* OrbitControls
* WebGL

### Server / Network

* Google Colab
* Cloudflared Tunnel

### 기타 Python 모듈

* `pathlib`
* `subprocess`
* `urllib.request`
* `socket`
* `threading`
* `datetime`
* `json`
* `re`
* `os`
* `sys`

---

## 설명

본 프로젝트는 생산 및 품질 관리 업무를 웹 환경에서 간단하게 체험할 수 있도록 제작한 교육용 생산·품질 관리 시스템입니다.

사용자는 조회 기간과 생산라인을 선택하여 LOT별 생산 및 검사 결과를 조회할 수 있습니다.

### 1. 생산 실적 조회

조회 조건에 따라 다음 정보를 확인할 수 있습니다.

* 목표 생산량
* 실제 생산량
* 생산 달성률
* 검사 수량
* 불량 수량
* 불량률

생산 달성률은 다음과 같이 계산합니다.

```text
생산 달성률 = 실제 생산량 ÷ 목표 생산량 × 100
```

불량률은 다음과 같이 계산합니다.

```text
불량률 = 불량 수량 ÷ 검사 수량 × 100
```

검사 수량이 0인 경우 불량률은 판단하지 않습니다.

### 2. LOT 생산·품질 데이터 조회

생산라인과 조회 날짜에 따라 LOT별 데이터를 조회할 수 있습니다.

조회 정보는 다음과 같습니다.

* 일자
* 생산라인
* LOT
* 목표 수량
* 생산 수량
* 검사 수량
* 불량 수량

조회된 데이터를 기반으로 전체 생산량과 품질 지표를 자동으로 계산합니다.

### 3. 일자별 불량률 시각화

조회 기간 내 생산 데이터를 이용하여 일자별 불량률을 막대 형태로 표현합니다.

이를 통해 특정 날짜의 품질 상태와 불량률 변화를 쉽게 확인할 수 있습니다.

### 4. 설비 사건 이력 조회

생산라인에서 발생한 설비 관련 이벤트를 함께 조회할 수 있습니다.

예시 상태는 다음과 같습니다.

* 정상
* 온도 주의
* 설비 정지
* 정상 복귀
* 미해제 이벤트

생산·품질 데이터와 설비 이벤트를 함께 확인하여 보고서 작성 시 참고할 수 있도록 구성했습니다.

### 5. Three.js 패널 검사·이송 설비

Three.js와 WebGL을 이용하여 패널 검사·이송 설비를 3D 형태로 구현했습니다.

3D 설비에는 다음 요소가 포함됩니다.

* 금속 설비 프레임
* 설비 베이스
* 롤러 컨베이어
* 디스플레이 패널
* 투명 검사 커버
* 검사 카메라 및 검사 헤드
* 조작 패널
* 상태 표시등
* 패널 이동 애니메이션

사용자는 마우스를 이용하여 설비를 회전하거나 확대·축소할 수 있습니다.

### 6. 생산·품질 보고서 생성

현재 조회한 생산·품질 데이터를 기반으로 보고서 초안을 자동 생성할 수 있습니다.

보고서에는 다음 내용이 포함됩니다.

* 조회 기간
* 생산라인
* 생산량
* 목표 생산량
* 생산 달성률
* 검사 수량
* 불량 수량
* 불량률
* LOT 기록 수
* 설비 사건
* 현재 설비 상태
* 추가 확인 사항

보고서는 생성 후 사용자가 직접 내용을 수정할 수 있습니다.

### 7. 보고서 검토 및 저장

작성된 보고서에 대해 검토 여부를 기록할 수 있으며, 수정된 보고서는 JSON 파일에 저장됩니다.

보고서는 고유한 ID를 사용하여 관리합니다.

예시:

```text
R001
R002
R003
```

저장된 보고서는 다시 불러와 수정할 수 있습니다.

### 8. 보고서 다운로드

저장한 보고서는 다음 형식으로 다운로드할 수 있습니다.

* TXT 보고서
* JSON 근거 데이터

TXT 파일에는 최종 보고서 내용이 포함되며, JSON 파일에는 보고서 작성에 사용된 생산·품질 데이터가 저장됩니다.

### 9. Flask REST API

Frontend와 Backend 사이의 데이터 처리를 위해 Flask 기반 API를 사용했습니다.

주요 API는 다음과 같습니다.

```text
GET  /api/view
GET  /api/reports
POST /api/report
GET  /api/report/<report_id>
POST /api/report/<report_id>
GET  /api/download/<report_id>/<type>
```

### 10. Cloudflared 외부 접속

Google Colab에서 실행되는 Flask 서버는 기본적으로 외부에서 직접 접속하기 어렵기 때문에 Cloudflared Tunnel을 사용했습니다.

Cloudflared 실행 후 다음과 같은 임시 주소가 생성됩니다.

```text
https://xxxxx.trycloudflare.com
```

해당 URL을 이용하면 PC 또는 모바일 브라우저에서 Colab에서 실행 중인 웹 서비스에 접속할 수 있습니다.

> Cloudflared 주소는 Colab 런타임을 다시 실행하면 변경될 수 있습니다.

---

## 프로젝트 목적

이 프로젝트의 목적은 실제 제조 현장에서 사용되는 생산·품질 관리 업무의 기본 흐름을 웹 서비스를 통해 학습하는 것입니다.

특히 다음 과정을 중심으로 구성했습니다.

```text
생산 데이터 조회
        ↓
생산 목표 대비 실적 확인
        ↓
검사 및 불량 데이터 확인
        ↓
설비 상태 및 사건 확인
        ↓
생산·품질 데이터 비교
        ↓
업무 보고서 작성
        ↓
보고서 검토 및 저장
```

실제 생산시스템이나 MES 데이터를 사용하는 것이 아니라 교육을 위해 생성한 가상 데이터를 사용합니다.

---

## 실행 환경

본 프로젝트는 **Google Colab 환경**을 기준으로 제작했습니다.

Python 코드를 실행하면 다음 작업이 자동으로 수행됩니다.

1. 필요한 Flask 패키지 확인 및 설치
2. 프로젝트 디렉터리 생성
3. Three.js 및 OrbitControls 다운로드
4. Flask 웹 서버 실행
5. 사용 가능한 포트 탐색
6. Cloudflared 다운로드 및 실행
7. 외부 접속 URL 생성
8. 웹 서비스 실행

---

## 데이터 저장

생성한 생산·품질 보고서는 다음 JSON 파일에 저장됩니다.

```text
/content/04_lgd_web/04_reports.json
```

보고서 생성 시 기존 데이터를 유지하면서 새로운 보고서를 추가합니다.

---

## 참고 문헌

### Flask

Flask Documentation
https://flask.palletsprojects.com/

### Werkzeug

Werkzeug Documentation
https://werkzeug.palletsprojects.com/

### Three.js

Three.js Documentation
https://threejs.org/docs/

### Three.js OrbitControls

Three.js OrbitControls Documentation
https://threejs.org/docs/#examples/en/controls/OrbitControls

### Cloudflare Tunnel

Cloudflare Tunnel Documentation
https://developers.cloudflare.com/cloudflare-one/connections/connect-networks/

### Google Colab

Google Colaboratory
https://colab.research.google.com/

### MDN Web Docs

HTML / CSS / JavaScript 및 Fetch API 참고
https://developer.mozilla.org/

---

## 주의사항

본 프로젝트에서 사용되는 생산량, LOT, 불량률, 설비 상태 및 설비 사건 데이터는 실제 LG디스플레이의 생산 데이터가 아닌 **교육 목적으로 제작한 가상 데이터**입니다.

실제 제조 시스템, 생산설비, 사내 MES 또는 품질관리 시스템의 구조와는 차이가 있을 수 있습니다.

---

## License

This project is intended for educational and practice purposes.
