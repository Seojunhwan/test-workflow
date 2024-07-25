## 링크

- S3 버킷 웹사이트 링크: [http://hanghae-fe2.s3-website.ap-northeast-2.amazonaws.com](http://hanghae-fe2.s3-website.ap-northeast-2.amazonaws.com)
- CloudFront 배포 링크: [https://d29mciphtw3fcz.cloudfront.net](https://d29mciphtw3fcz.cloudfront.net)

---

## 다이어그램

![제목 없음-2024-07-26-0039](https://github.com/user-attachments/assets/bab11ac7-61ba-44fb-ad6b-185deea0bde1)

---

## GitHub Actions과 CI/CD 도구

Github Actions는 개발 워크플로우를 자동화하는 지속적 통합, 지속적 배포 플랫폼 입니다.

주요 특징으론 아래와 같습니다.

- 자동화
  - 코드 변경에 따른 자동 테스트 및 빌드
  - 배포 자동화
- 유연성
  - 다양한 언어와 여러 환경(플랫폼)을 지원하며 더 나아가 self hosted runner를 사용할 수 있습니다.
- GitHub 통합
  - GitHub 저장소와 긴밀하게 연동되어 있습니다.
- 다양한 액션
  - 이미 만들어진 액션을 사용하거나, 직접 만들어 사용할 수 있습니다.

CI/CD 도구의 주요 이점

- 빠른 피드백: 코드 변경 시 즉시 테스트와 빌드를 수행하여 문제를 빠르게 발견합니다.
- 품질 향상: 자동화된 테스트로 버그를 줄이고 코드 품질을 높입니다.
- 생산성 향상: 반복적인 작업을 자동화하여 개발자가 핵심 업무에 집중할 수 있습니다.
- 안정적인 배포: 자동화된 배포 프로세스로 인적 오류를 줄이고 안정성을 높입니다.

---

## S3와 스토리지

Amazon S3(Simple Storage Service)는 AWS에서 제공하는 클라우드 객체 스토리지 서비스입니다. 웹 사이트, 모바일 애플리케이션, 백업 및 복원, 아카이브, 엔터프라이즈 애플리케이션, IoT 디바이스, 빅 데이터 분석 등 다양한 용도로 사용됩니다.

### S3의 주요 특징

- 확장성: 거의 무제한의 데이터를 저장할 수 있습니다.
- 내구성: 99.999999999%의 데이터 내구성을 제공합니다.
- 가용성: 99.99%의 가용성을 보장합니다.
- 보안성: 다양한 보안 기능을 제공합니다 (암호화, 액세스 제어 등).
- 성능: 대용량 데이터의 빠른 업로드 및 다운로드를 지원합니다.
- 저렴한 비용: 사용한 만큼만 지불하는 방식으로 비용 효율적입니다.

### S3의 주요 사용 사례

- 정적 웹사이트 호스팅: HTML, CSS, JavaScript 파일을 저장하고 웹사이트로 제공할 수 있습니다.
- 데이터 백업 및 복구: 중요한 데이터를 안전하게 백업하고 필요시 복구할 수 있습니다.
- 빅데이터 분석: 대용량 데이터를 저장하고 분석 도구와 연동하여 사용할 수 있습니다.
- 콘텐츠 배포: CloudFront와 연동하여 전 세계에 콘텐츠를 빠르게 배포할 수 있습니다.
- 데이터 아카이빙: 장기 보관이 필요한 데이터를 저렴한 비용으로 저장할 수 있습니다.

---

## CloudFront 와 CDN

CloudFront는 AWS의 CDN 서비스 입니다.
기본적으로 동작 방식은 아래와 같습니다.

- DNS가 요청을 잘 처리할 수 있는 CloudFront POP으로 요청을 라우팅 합니다.
- 사용자가 요청한 콘텐츠가 캐시에 존재하는 경우, 캐시를 사용합니다.
- 캐시가 없는 경우, 원본 서버로 요청을 라우팅 합니다.

CDN(Content Delivery Network)은 상호 연결된 서버 네트워크로 콘텐츠를 전 세계에 빠르게 배포하기 위해 사용되는 서비스입니다.
주요 목적은 대기 시간을 줄이거나, 네트워크 설계로 인한 통신 지연을 줄이는 것입니다.

[동작 원리](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/HowCloudFrontWorks.html)

---

## 캐시 무효화

캐시 무효화는 CDN(Content Delivery Network)의 엣지 로케이션에 저장된 캐시된 콘텐츠를 강제로 제거하거나 업데이트하는 프로세스입니다. CloudFront와 같은 CDN 서비스에서 중요한 기능입니다.

### 캐시 무효화가 필요한 이유

- 콘텐츠 업데이트: 웹사이트의 내용이 변경되었을 때 최신 버전을 즉시 반영하기 위해 사용합니다.
- 오류 수정: 잘못된 콘텐츠가 캐시되었을 때 이를 신속하게 제거하기 위해 필요합니다.
- 보안 문제: 보안상 민감한 정보가 캐시되었을 때 이를 제거하기 위해 사용됩니다.

### 주의

- 필요한 파일만 무효화
- 버전 관리 사용: 파일 이름에 버전 정보를 포함시켜 무효화 없이도 최신 버전을 사용할 수 있습니다.

[참고](https://docs.aws.amazon.com/ko_kr/AmazonCloudFront/latest/DeveloperGuide/Invalidation.html)

---

## GitHub Actions Workflow

### Checkout repository | actions/checkout@v4

- 작업 디렉토리를 체크아웃합니다.

### Install pnpm | pnpm/action-setup@v4

- pnpm을 설치하고 설정합니다.

### Set up Node.js | actions/setup-node@v4

- Node.js를 설치하고 설정합니다.
- `cache` 를 `pnpm` 으로 설정하여 의존성 캐시를 사용합니다.

### Build cache | actions/cache@v4

- [CI 작업 중 Next.js Build Cache를](https://nextjs.org/docs/pages/building-your-application/deploying/ci-build-caching#github-actions) 사용합니다.

### Install dependencies

- 프로젝트 의존성을 설치합니다.

### Build

- Next.js 프로젝트를 빌드합니다.

### Configure AWS credentials | aws-actions/configure-aws-credentials@v1

- AWS 자격 증명을 구성합니다.

### Deploy to S3 | aws-actions/s3-deploy@v4

- 빌드 결과를 S3 버킷에 업로드합니다.

### Deploy to CloudFront | aws-actions/cloudfront-deploy@v4

- CloudFront 캐시를 무효화하여 새로운 빌드 결과를 배포합니다.
