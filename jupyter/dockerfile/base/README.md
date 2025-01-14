# Jupyter Base

## 개요

Jupyter 자제가 많은 의존성 문제가 발생할 수 있으므로 컨테이너에 격리된 운영 환경 필요

## 목표

1. 나에게 맞는 설정을 가진 Jupyter 이미지를 Dockerfile로 제작
2. 제작 완료 후 거대해진 이미지 용량 다이어트

## 개발용 명령어

```bash
# 빌드
sudo docker build -t jupyter .

# 실행
sudo docker run --rm -it -p 8888:8888 jupyter
```
