
# Kubernetes Microservices Deployment (Fleetman Example)

이 저장소는 Udemy 강의 **"Kubernetes 실습: AWS 클라우드에 마이크로서비스 배포하기"** 실습을 기반으로 작성된 Kubernetes 매니페스트 모음입니다.  
Fleetman 애플리케이션을 마이크로서비스 아키텍처로 배포하기 위한 Deployment, Service, Storage 설정을 포함합니다.

---

## 구성 파일

- **workloads.yaml**
  - Queue 서비스 (ActiveMQ 기반)
  - Position Simulator (위치 데이터 생성)
  - Position Tracker (위치 데이터 처리)
  - API Gateway (서비스 엔드포인트 집약)
  - Webapp (Angular 기반 프론트엔드)

- **storage.yaml**
  - MongoDB용 PersistentVolumeClaim (PVC)
  - PersistentVolume (PV) 정의 (hostPath 기반)

- **services.yaml**
  - `fleetman-webapp` (NodePort, 브라우저 접속용 → 포트 30080)
  - `fleetman-queue` (NodePort, 메시지 큐 관리용 → 포트 30010)
  - `fleetman-position-tracker` (ClusterIP, 내부 통신용 → 포트 8080)
  - `fleetman-api-gateway` (ClusterIP, 내부 통신용 → 포트 8080)

- **mongo-stack.yaml**
  - MongoDB Deployment (PVC 마운트)
  - `fleetman-mongodb` Service (ClusterIP → 포트 27017)

---

## 실행 방법

"스토리지 리소스 생성"
bash
kubectl apply -f storage.yaml

"MongoDB 배포"
bash
kubectl apply -f mongo-stack.yaml

"워크로드 배포"
bash
kubectl apply -f workloads.yaml

"서비스 생성"
bash
kubectl apply -f services.yaml
