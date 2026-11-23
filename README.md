<!--
  프로필 레포(seonghong1/seonghong1)의 README.md에 그대로 붙여 넣는다. 한국어판. 2026-11-23 작성, 같은 날 담백하게 다시 씀.
  이력서처럼 경력을 나열하지 않고, 개발 · 사이드 프로젝트(개연시) · 기술 스택만 담는다.
  꾸밈은 기술 스택 배지에만 쓴다. 애니메이션 헤더 · 타이핑 문구 · 통계 카드 · 이모지는 쓰지 않는다 (본인 요청).
  근거: ../사이드_프로젝트/gaeyeonsi/프로젝트_정리.md (8-1 · 8-2 · 8-3 · 8-4 · 8-6 · 8-14 · 9장),
        gaeyeonsi 레포 documents/development/cicd/01-github-actions.md (OIDC, 커밋 SHA 태그, SSM Run Command)
  쓰지 않은 숫자: 에피소드 수 · 테스트 수(계속 바뀜), 월 운영비(추정치), 사용자 · 다운로드 수(근거 없음)
-->

### 안녕하세요, 백엔드 개발자 조성홍입니다.

지금은 외국어 교육 플랫폼에서 수업, 예약, B2B 서비스를 만들고 있고, 개인적으로는 Kubernetes와 Terraform으로 사이드 프로젝트를 운영하고 있습니다.

<br/>

## 기술 스택

| 분야 | 기술 |
|:---:|:---|
| **Backend** | <img src="https://img.shields.io/badge/Kotlin-7F52FF?style=for-the-badge&logo=kotlin&logoColor=white" alt="Kotlin"/> <img src="https://img.shields.io/badge/Spring_Boot-6DB33F?style=for-the-badge&logo=springboot&logoColor=white" alt="Spring Boot"/> <img src="https://img.shields.io/badge/PHP-777BB4?style=for-the-badge&logo=php&logoColor=white" alt="PHP"/> <img src="https://img.shields.io/badge/Laravel-FF2D20?style=for-the-badge&logo=laravel&logoColor=white" alt="Laravel"/> <img src="https://img.shields.io/badge/TypeScript-3178C6?style=for-the-badge&logo=typescript&logoColor=white" alt="TypeScript"/> <img src="https://img.shields.io/badge/NestJS-E0234E?style=for-the-badge&logo=nestjs&logoColor=white" alt="NestJS"/> |
| **Database** | <img src="https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white" alt="MySQL"/> <img src="https://img.shields.io/badge/PostgreSQL-4169E1?style=for-the-badge&logo=postgresql&logoColor=white" alt="PostgreSQL"/> <img src="https://img.shields.io/badge/Redis-FF4438?style=for-the-badge&logo=redis&logoColor=white" alt="Redis"/> |
| **Infra · DevOps** | <img src="https://img.shields.io/badge/AWS-FF9900?style=for-the-badge&logo=amazonwebservices&logoColor=white" alt="AWS"/> <img src="https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white" alt="Docker"/> <img src="https://img.shields.io/badge/Kubernetes-326CE5?style=for-the-badge&logo=kubernetes&logoColor=white" alt="Kubernetes"/> <img src="https://img.shields.io/badge/Terraform-844FBA?style=for-the-badge&logo=terraform&logoColor=white" alt="Terraform"/> <img src="https://img.shields.io/badge/GitHub_Actions-2088FF?style=for-the-badge&logo=githubactions&logoColor=white" alt="GitHub Actions"/> <img src="https://img.shields.io/badge/Cloudflare-F38020?style=for-the-badge&logo=cloudflare&logoColor=white" alt="Cloudflare"/> <img src="https://img.shields.io/badge/Datadog-632CA6?style=for-the-badge&logo=datadog&logoColor=white" alt="Datadog"/> |
| **Frontend · App** | <img src="https://img.shields.io/badge/React-61DAFB?style=for-the-badge&logo=react&logoColor=black" alt="React"/> <img src="https://img.shields.io/badge/Vue.js-4FC08D?style=for-the-badge&logo=vuedotjs&logoColor=white" alt="Vue.js"/> <img src="https://img.shields.io/badge/Swift-F05138?style=for-the-badge&logo=swift&logoColor=white" alt="Swift"/> <img src="https://img.shields.io/badge/Capacitor-119EFF?style=for-the-badge&logo=capacitor&logoColor=white" alt="Capacitor"/> |
| **AI** | <img src="https://img.shields.io/badge/Claude_Code-D97757?style=for-the-badge&logo=claude&logoColor=white" alt="Claude Code"/> <img src="https://img.shields.io/badge/OpenAI_API-412991?style=for-the-badge&logo=openai&logoColor=white" alt="OpenAI API"/> |

<br/>

## 개연시

장애 대응 시뮬레이션 게임 · [gaeyeonsi.com](https://gaeyeonsi.com) · [App Store](https://apps.apple.com/kr/app/id6832839828)

장애 알림이 울리면 로그와 지표에서 단서를 찾고, 대응을 골라 서비스를 복구하는 게임입니다. Kubernetes와 Terraform을 직접 운영해 보려고 시작했고, 기획부터 웹과 iOS 출시, 운영까지 혼자 하고 있습니다.

Kotlin · Spring Boot · PostgreSQL · React · Capacitor · k3s · Terraform · AWS · Cloudflare

```mermaid
flowchart LR
    user(["사용자<br/>웹 · iOS 앱"]) --> cf["Cloudflare<br/>DNS · 정적 호스팅 · 프록시"]
    cf -- "443, Cloudflare IP만 허용" --> ing
    subgraph ec2 ["AWS EC2 1대 · Terraform으로 구성"]
        ing["k3s · Traefik Ingress"] --> api["Spring Boot · Kotlin"]
        api --> db[("PostgreSQL<br/>별도 EBS · 매일 스냅샷")]
    end
    gha["GitHub Actions"] -- "OIDC · 커밋 SHA 이미지" --> ecr[("Amazon ECR")]
    ecr -. "이미지 pull" .-> api
    gha -- "SSM Run Command 배포" --> ing
    gha -- "wrangler deploy" --> cf
```

- 시나리오를 DB 테이블과 1:1인 JSON으로 두고 엔진은 해석만 합니다. 에피소드를 늘려도 엔진 코드는 그대로입니다.
- 모든 선택 경로를 끝까지 플레이하는 검증기가 PR CI에서 돌아, 막다른 길이나 도달할 수 없는 엔딩이 있으면 병합을 막습니다.
- EKS, RDS, ALB, NAT 없이 EC2 1대에 k3s와 PostgreSQL을 두고, DB 데이터만 별도 EBS와 매일 스냅샷으로 지킵니다. 표준 Ingress와 ConfigMap만 써서 EKS로 옮길 수 있게 했습니다.
- GitHub Actions는 OIDC로 AWS에 인증하고, 커밋 SHA 태그 이미지를 SSM Run Command로 배포합니다. 서버에 SSH 포트는 열지 않습니다.
- Access token은 15분 동안 메모리에만 두고, Refresh Token Rotation에서 이미 쓴 토큰이 다시 오면 그 계열을 모두 무효화합니다.
- 채점식을 바꿀 때 배포와 전환을 설정값으로 나누고, 드라이런으로 영향을 본 뒤 끝난 판 286개를 다시 채점했습니다. 포인트가 줄어든 회원은 0명입니다.

Claude Code와 함께 개발합니다. 결정은 버린 안과 받아들인 대가까지 문서에 먼저 쓰고, 구현은 에이전트에 맡기되 검증은 검증기와 테스트, CI로 합니다.

<br/>

## 요즘 관심 있는 것

- Kubernetes와 Terraform: k3s로 시작한 개연시를 EKS로 옮기는 절차를 공부하고 있습니다.
- AI 에이전트로 테스트하기: 단계마다 에이전트를 나누고, 테스트는 에이전트가 실제 브라우저를 조작해 확인하게 합니다.
- 서비스 보안: 런타임과 서버 취약점 소식을 찾아보고, 운영 중인 서버에 영향이 있는지 직접 확인합니다.

<br/>

## 연락처

[Email](mailto:seonghong_jo-dev@naver.com) · [LinkedIn](https://www.linkedin.com/in/seonghong-jo-ba611a306) · [개연시](https://gaeyeonsi.com)
