## ✏️ CI/CD 란 ?

![CI/CD](https://velog.velcdn.com/images/wnguswn7/post/589ad526-7e10-4b16-bad3-68575258a100/image.PNG)

### ✔ CI ( Continuous Integration )

- 지속적인 통합
    - 여러명이 하나의 코드에 대해 수정을 진행해도 지속적으로 통합하면서 관리할 수 있음을 의미.
- 개발을 진행하면서도 품질을 관리할 수 있도록 하는 것
- 애플리케이션의 새로운 코드 변경사항이 정기적으로 빌드 / 테스트 되어 공유 레포지토리에 병합하는 것을 의미

👉 즉, 새로운 소스코드의 **빌드, 테스트, 병합**

#### ✔️ CI의 목적
➜ 버그를 신속하게 찾아 해결한다 <br>
➜ 소프트웨어의 품질을 개선한다 <br>
➜ 새로운 업데이터의 검증 및 릴리즈의 시간을 단축시킨다

> CI가 나오기 전까지는 개발을 마치고 배포가 되어야만 코드에 오류가 없는지, 올바르게 동작하는지 검증하며 코드 품질을 관리할 수 있었는데, CI를 적용하면 개발자는 각자 자신이 구현해야할 기능만 구현하면 된다.

### ✔ CD ( Continuous Delivery / Continuous Deployment )

- 지속적 제공 (Continuous Delivery)<br>
    ➜ 공유 레포지토리까지 자동으로 릴리즈 하는 것

- 지속적인 배포 (Continuous Deployment)<br>
    ➜ Production 레벨까지 자동으로 배포하는 것

- 항상 신뢰 가능한 수준에서 배포될 수 있도록 관리하자는 개념

👉 즉, CI가 정상적으로 진행된 이후에
개발자의 변경 사항이 **레포지토리를 넘어 고객의 Production 환경까지 릴리즈**되는 것
➜ **배포 자동화**

### 추가자료<br>
[CI/CD가 뭔가요?](https://tecoble.techcourse.co.kr/post/2021-08-14-ci-cd/)<br>
[CI/CD란 무엇인가 (Feat. DevOps 엔지니어)](https://artist-developer.tistory.com/24) 

---

### ✏️ 배포 자동화란 ?
- 한번의 클릭 또는 명령어 입력을 통해 전체 배포 과정을 자동으로 진행하는 것
- 배포 과정을 자동화시킴으로써 시간 절약 및 휴먼 에러 방지 가능

---

### ✔ 배포 자동화 파이프라인

1. Source 단계<br>
    ➜ 원격 저장소에 관리되고 있는 소스 코드에 변경 사항이 일어날 경우, 이를 감지하고 다음 단계로 전달하는 작업 수행

2. Build 단계<br>
    ➜ Source 단계에서 전달받은 코드를 컴파일, 빌드, 테스트하여 가공
    ➜ Build 단계를 거쳐 생성된 결과물을 다음 단계로 전달하는 작업 수행

3. Deploy 단계<br>
    ➜ Build 단계로부터 전달받은 결과물을 실제 서비스에 반영하는 작업 수행

> ### ✔️ 파이프라인 (Pipeline)
> - 소스 코드의 관리부터 실제 서비스로의 배포 과정을 연결하는 구조
> - 각 배포 단계는 파이프라인 안에서 순차적으로 실행됨

---

### 📌 CodePipeline
- 각 단계를 연결하는 파이프라인을 구축할 때 이용<br>

> ⚠️ AWS 프리티어 계정 사용 시, 한 계정에 두 개 이상의 파이프라인을 생성하면 추가 요금이 부여될 수 있음 !!

---
### ✏️ Github Actions

- Github이 공식적으로 제공하는 빌드, 테스트 및 배포 파이프라인을 자동화할 수 있는 CI/CD 플랫폼
- 특정 파일(.yml)에 따라 Github Repository에 특정 변동사항을 트리거로 작동
- 레포지토리에서 Pull Request나 push같은 이벤트를 트리거로 GitHub 작업 워크플로 (Workflow) 구성 가능

> ### ✔️ 워크플로 (Workflow) <br>
> - 하나 이상의 작업이 실행되는 자동화 프로세스
> - .yml or .yaml 파일에 의해 구성
> - 기능에 따라 여러개의 워크플로 생성 가능 <br>
>   Ex) 테스트 / 배포 ... <br>
>     ( 생성된 워크플로는 .github/workflows 디렉토리 이하에 위치 )

- 레포지토리의 공개 / 비공개에 따라 요금 제한이 다름
    - Private 레포지토리 <br>
        ➜ Github Actions 가 작동할 때의 용량과 시간이 제한됨
    - Public 레포지토리 <br>
        ➜ 무료로 사용 가능

[[ 공식문서 ]](https://docs.github.com/en/actions) <br>
[[ 사용법 참고 링크 ]](https://zzsza.github.io/development/2020/06/06/github-action/)
        
---

### ✔ Github Actions를 통한 자동 배포 Flow

![배포](https://velog.velcdn.com/images/wnguswn7/post/55ada33a-2979-4666-9bfc-910664a216ed/image.png)

![배포](https://velog.velcdn.com/images/wnguswn7/post/de83efa5-a513-45b2-821e-7b5c4cea8243/image.png)

- S3
    - 여기서는 정적 웹 페이지를 배포하는 것이 아닌, 저장소로 사용
    - Github Actions에서 빌드한 결과물이 압축되어 S3로 전송되고, 버킷에 저장됨

- Code Deploy
    - S3에 저장되어있는 빌드 결과물을 EC2 인스턴스로 이동
    - 프로젝트 최상단에 위치한 appspec.yml 설정 파일에 의해 쉘 스크립트 등 단계에 따라서 특정 동작을 함

> Code Deploy가 S3버킷에서 EC2 인스턴스로 프로젝트를 이동할 수 있도록 EC2 인스턴스에 Code Deploy Agent의 설치가 필요

- EC2
    - Code Deploy에 의해 빌드 과정을 거친 프로젝트가 EC2 인스턴스로 전달되고,
.yml(설정파일)과 .sh(쉘 스크립트)에 의해 각 배포 결과를 로그로 저장하며 빌드 파일(.jar)을 실행

---

