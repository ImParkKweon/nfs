# Kubernetes NFS Storage Configuration

## 📌 Overview
이 저장소는 **Kubernetes 환경에서 NFS(Network File System)를 기반으로 한 영구 스토리지 구성 예제**를 정리한 리포지토리입니다.  
실제 클러스터 환경에서 **NFS 서버 배포 → StorageClass 생성 → PVC/PV 테스트**까지의 전체 흐름을 YAML 기반으로 구성했습니다.

단순한 설정 나열이 아니라,  
👉 **클라우드/컨테이너 환경에서 스토리지가 어떻게 동작하는지 이해하고 직접 구성할 수 있음을 증명**하는 것을 목표로 합니다.

---

## 🧩 Architecture
```
[ Pod ]
   |
[ PVC ]
   |
[ StorageClass (NFS) ]
   |
[ NFS Server ]
```

---

## 📂 Repository Structure
```
.
├── deployment.yaml        # NFS 서버 Deployment
├── rbac.yaml              # NFS 관련 RBAC 설정
├── sc.yaml                # NFS StorageClass 정의
├── test_pod.yaml          # PVC 마운트 테스트용 Pod
├── test_pvc.yaml          # 테스트용 PersistentVolumeClaim
```

---

## ⚙️ Prerequisites
- Kubernetes Cluster (온프레미스 / 퍼블릭 클라우드 무관)
- kubectl configured
- Kubernetes 기본 리소스 이해 (Pod, PVC, PV, StorageClass)

---

## 🚀 How to Use

### 1️⃣ NFS 서버 배포
```bash
kubectl apply -f deployment.yaml
kubectl apply -f rbac.yaml
```

### 2️⃣ StorageClass 생성
```bash
kubectl apply -f sc.yaml
```

### 3️⃣ PVC 생성
```bash
kubectl apply -f test_pvc.yaml
kubectl get pvc
```

### 4️⃣ Pod에서 PVC 마운트 테스트
```bash
kubectl apply -f test_pod.yaml
kubectl exec -it <pod-name> -- /bin/sh
df -h
```

---

## ✅ What This Project Demonstrates
- Kubernetes 스토리지 구조 이해 (PV / PVC / StorageClass)
- NFS 기반 공유 스토리지 구성 경험
- YAML 기반 인프라 리소스 정의 능력
- 클라우드 환경에서 Stateful 서비스 운영 기초 역량

---

