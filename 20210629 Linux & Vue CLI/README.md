# [210629] TIL

### Review - 큰 그림을 이해해야 하는 이유

- 현업 개발자의 업무는 코딩이 전부가 아님
- 개발 프로젝트는 시스템 설계부터 시작됨
- 작업의 범위 이해 및 버그 발생지 파악에 필요
- 기술 면접 시 질문
- i.g. Web-architecture

![Web Architecture 101 / Getting started as a web developer](https://cdn-images-1.medium.com/max/1600/1*K6M-x-6e39jMq_c-2xqZIQ.png)



## 1. Client - Server Architecture

> 박경민 컨설턴트님

```
- 상용 서버에서 일반적으로 많이 사용하는 운영체제 : 리눅스
- 개발자가 개발한 코드를 상용서버에 올리는 작업을 의미하는 용어 : 배포
- 24시간 켜져 있는 컴퓨터가 서비스를 제공하는 것을 의미하는 용어 : 호스팅
```

- 개발자의 OS
- 서버용으로 많이 활용
- 무료
- 오픈소스 프로젝트
- 기타 등등

### 1.1. Linux 란?

#### 1.1.1. 종류 (계열)

- Debian - **ubuntu** - linux mint
- Red Hat - **centOS** - **fedora**
- Slackware



#### 1.1.2. HW - 커널 - 쉘

- PC 설치

- 윈도우10의 WSL2

- 가상머신 VirtualBox

- 클라우드 AWS EC2

  - 아마존 AWS
  - 마이크로소프트 Azure
  - 구글 GCP

  

#### 1.1.3. 과제

[ LINUX ]

```
1. 어떠한 이유로 어떤 방법을 선택하였나?
2. 어떻게 리눅스 머신을 구했나?
3. 하다보니 무엇이 막혔는데 어떻게 해결했나?
4. 결국 무엇을 배웠나?
```



## 2. CI / CD - Vue CLI 프로젝트 기반 DevOps 개발환경 실습

> 최광호 컨설턴트님

### 2.1. DevOps 란?

DevOps는 애플리케이션과 서비스를 빠른 속도로 제공할 수 있도록 조직의 역량을 향상시키는 문화 철학, 방식 및 도구의 조합입니다. 기존의 소프트웨어 개발 및 인프라 관리 프로세스를 사용하는 조직보다 제품을 더 빠르게 혁신하고 개선할 수 있습니다. 이러한 빠른 속도를 통해 조직은 고객을 더 잘 지원하고 시장에서 좀 더 효과적으로 경쟁할 수 있습니다. 개발에서의 빌드, 배포, 워크 플로우, 운영, 모니터링 등 담당합니다. 



### 2.2. Vue CLI 전체 구성도

#### 2.2.1. JAM Stack

- Javascript + APIs + Markup `+ Headless CMS`



### 2.3. 명세서 살펴보기

```
1. Vue 프로젝트 생성 및 로컬 실행 확인
2. GitHub에 코드 Push 및 Pages에 수동 배포
3. GitHub Actions workflow로 배포 자동화
4. 코드 수정 및 테스트 실패로 인한 자동 배포 실패 확인
5. 코드 재수정 및 배포 성공 확인
```







## 3. Dockerize

