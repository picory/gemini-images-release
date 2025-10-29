# Gemini Images - AI 기반 모델 이미지 생성 도구

Google Gemini 웹페이지를 활용하여 모델 이미지와 상품 이미지를 합성하여 자연스러운 착용 이미지를 생성하는 자동화 도구입니다.

## 주요 기능

- **자동 이미지 생성**: 모델 이미지와 상품 이미지를 결합하여 AI 기반 착용 이미지 생성
- **FastAPI 기반 REST API 서버**: 외부 시스템과의 연동을 위한 웹 API 제공
- **GUI 런처**: 사용자 친화적인 GUI를 통한 서버 관리
- **모델 이미지 관리**: 여러 모델 이미지를 등록하고 관리
- **자동 업데이트**: GitHub 릴리스를 통한 자동 업데이트 기능
- **라이선스 인증**: 시리얼 키 기반 라이선스 검증 시스템

## 시스템 요구사항

### 필수 구성 요소

1. **Python**: 3.10 이상
2. **Google Chrome**: Playwright를 통한 브라우저 자동화에 필요
3. **Google API Key**: Gemini API 사용을 위한 인증 키

### 설치 파일 다운로드

- **최신 릴리스**: [GitHub Releases](https://github.com/picory/gemini-images-release/releases/latest)
- **기본 앱 설치 파일**: [GeminiImagesInstaller.exe](https://github.com/picory/gemini-images-release/releases/download/1.3.0/GeminiImagesLauncher.exe)
- **Chrome 확장 프로그램**: [오버링크 썸네일 헬퍼](https://chromewebstore.google.com/detail/%EC%98%A4%EB%B2%84%EB%A7%81%ED%81%AC-%EC%8D%B8%EB%84%A4%EC%9D%BC-%ED%97%AC%ED%8D%BC/emjolgbjdaanhiihkaecbmmebpgpggmf?authuser=0&hl=en)
- 실행 파일(`.exe`)을 다운로드하여 별도의 설치 없이 사용 가능

## 설치 방법

### 방법 1: 실행 파일 사용 (권장)

1. [GitHub Releases](https://github.com/picory/gemini-images-release/releases/latest)에서 최신 `.exe` 파일 다운로드
2. 다운로드한 파일 실행
3. 시리얼 키 입력 및 인증

### 방법 2: 소스 코드에서 실행

#### 1. 저장소 클론

```bash
git clone https://github.com/picory/gemini-images-release.git
cd gemini-images
```

#### GUI 기능

- **데이터 기본 경로**: 생성된 이미지 및 모델 이미지가 저장되는 디렉토리 설정
- **서버 포트**: API 서버가 실행될 포트 번호 (기본값: 9998)
- **자동 실행**: 프로그램 시작 시 서버 자동 시작
- **임시 파일 삭제**: 프로그램 시작 시 생성된 이미지 자동 삭제
- **API 문서 열기**: FastAPI 자동 생성 문서(`/docs`) 열기
- **업데이트 확인**: 수동으로 새 버전 확인
- **설정**: 타임아웃 등 자동화 관련 설정 조정
- **시리얼 등록**: 라이선스 키 입력 및 인증

### API 엔드포인트

서버 실행 후 `http://localhost:9998/docs`에서 전체 API 문서 확인 가능

#### 주요 API

- `POST /generate`: 파일 업로드를 통한 이미지 생성
- `POST /generate-by-url`: URL 기반 이미지 생성
- `POST /models`: 모델 이미지 등록
- `GET /models`: 등록된 모델 이미지 목록 조회
- `GET /models/{model_id}`: 특정 모델 이미지 조회
- `PUT /models/{model_id}`: 모델 이미지 수정
- `DELETE /models/{model_id}`: 모델 이미지 삭제

#### API 사용 예시

```bash
# 모델 이미지 등록
curl -X POST "http://localhost:9998/models"   -F "image=@model.jpg"   -F "name=전신 모델 남"

# URL 기반 이미지 생성
curl -X POST "http://localhost:9998/generate-by-url"   -H "Content-Type: application/json"   -d '{
    "site": "your-site",
    "model_url": "http://localhost:9998/model-images/abc123.jpg",
    "product_url": ["https://example.com/product.jpg"],
    "return_count": 2,
    "headless": true
  }'
```

## 프로젝트 구조

```
GeminiImages/
├── generated_images/        # 생성된 이미지 저장 디렉토리
├── model_images/            # 등록된 모델 이미지
├── uploads/                 # 임시 업로드 파일
└── thumbnails/              # 썸네일 캐시
```

## 설정 파일

설정 파일은 다음 위치에 저장됩니다:

- **Windows**: `%APPDATA%\GeminiImages\config\`
- **Linux/Mac**: `~/.config/GeminiImages/`

주요 설정 파일:

- `launcher.bin` / `launcher.json`: 런처 설정 (자동 실행, 라이선스 키 등)
- `automation.bin` / `automation.json`: 자동화 타임아웃 설정
- `update.json`: 자동 업데이트 설정
- `test-prompt.json`: 프롬프트 테스트 파일(우선으로 확인)

## 문제 해결

### 라이선스 인증 실패

- 시리얼 키 형식: `XXXX-XXXX-XXXX-XXXX`
- 문제 지속 시: bitsense@kakao.com 문의

### 로그 확인

- 로그 파일 위치: `logs/app_YYYYMMDD.log`

## 라이선스

이 프로젝트는 상용 라이선스로 보호됩니다. 시리얼 키 구매 및 문의는 bitsense@kakao.com으로 연락 주세요.

## 지원 및 문의

- **이슈 리포트**: [GitHub Issues](https://github.com/picory/gemini-images-release/issues)
- **이메일**: bitsense@kakao.com

## 버전 정보

- **현재 버전**: 1.3.0
- **업데이트 확인**: GUI 런처에서 "업데이트 확인" 버튼 클릭
- **변경 내역**: [GitHub Releases](https://github.com/picory/gemini-images-release/releases)
