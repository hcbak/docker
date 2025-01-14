# Jupyter Base

## 개요

Jupyter 자제가 많은 의존성 문제가 발생할 수 있으므로 컨테이너에 격리된 운영 환경 필요

## 목표

1. 나에게 맞는 설정을 가진 Jupyter 이미지를 Dockerfile로 제작
2. 제작 완료 후 거대해진 이미지 용량 다이어트

## 개발

### 명령어

```bash
# 빌드
docker build -t jupyter .

# 실행 (종료 시 컨테이너 삭제)
docker run --rm -it -p 8888:8888 jupyter
```

## 운영

### 명령어

```bash
# 이미지 다운로드
docker pull hcbak/jupyter-base:latest

# 실행
docker run -d --name jupyter -p 8888:8888 hcbak/jupyter-base:latest
```

### 정보

|User Name|Jupyter Web Password|
|-|-|
|europa|europa|

- 기본 인터페이스의 언어는 한글입니다.
- D2Coding 글꼴을 사용할 수 있습니다.
  - "D2Coding", "D2Coding ligature" 등

[DockerHub](https://hub.docker.com/r/hcbak/jupyter-base)
