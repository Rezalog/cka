Kubernetes 실습을 위한 단계별 가이드를 제공합니다. 여기서는 Visual Studio Code (VSCode)를 사용하여 로컬에서 Kubernetes 클러스터를 설정하고 관리하는 방법을 설명하고, 이를 GitHub 리포지토리에 업로드하는 방법도 포함하겠습니다.

### 1. 환경 설정

#### 1.1 Minikube 설치 및 설정

Minikube는 로컬에서 Kubernetes 클러스터를 실행할 수 있게 해주는 도구입니다.

1. **Minikube 설치**
   - [Minikube 설치 가이드](https://minikube.sigs.k8s.io/docs/start/)를 참고하여 운영 체제에 맞는 설치 방법을 따라 설치합니다.

2. **클러스터 시작**
   ```bash
   minikube start
   ```

#### 1.2 kubectl 설치 및 설정

kubectl은 Kubernetes 클러스터를 관리하기 위한 명령줄 도구입니다.

1. **kubectl 설치**
   - [kubectl 설치 가이드](https://kubernetes.io/docs/tasks/tools/install-kubectl/)를 참고하여 운영 체제에 맞는 설치 방법을 따라 설치합니다.

2. **kubectl 설정**
   ```bash
   kubectl config set-context minikube
   kubectl config use-context minikube
   ```

### 2. Kubernetes 기본 개념

#### 2.1 파드(Pod) 생성

1. **파드 생성용 YAML 파일 작성**
   - `pod.yaml` 파일을 생성하고 다음 내용을 추가합니다:
     ```yaml
     apiVersion: v1
     kind: Pod
     metadata:
       name: nginx-pod
     spec:
       containers:
       - name: nginx
         image: nginx:latest
         ports:
         - containerPort: 80
     ```

2. **파드 생성**
   ```bash
   kubectl apply -f pod.yaml
   ```

#### 2.2 서비스(Service) 생성

1. **서비스 생성용 YAML 파일 작성**
   - `service.yaml` 파일을 생성하고 다음 내용을 추가합니다:
     ```yaml
     apiVersion: v1
     kind: Service
     metadata:
       name: nginx-service
     spec:
       selector:
         app: nginx
       ports:
       - protocol: TCP
         port: 80
         targetPort: 80
       type: NodePort
     ```

2. **서비스 생성**
   ```bash
   kubectl apply -f service.yaml
   ```

#### 2.3 디플로이먼트(Deployment) 생성

1. **디플로이먼트 생성용 YAML 파일 작성**
   - `deployment.yaml` 파일을 생성하고 다음 내용을 추가합니다:
     ```yaml
     apiVersion: apps/v1
     kind: Deployment
     metadata:
       name: nginx-deployment
     spec:
       replicas: 2
       selector:
         matchLabels:
           app: nginx
       template:
         metadata:
           labels:
             app: nginx
         spec:
           containers:
           - name: nginx
             image: nginx:latest
             ports:
             - containerPort: 80
     ```

2. **디플로이먼트 생성**
   ```bash
   kubectl apply -f deployment.yaml
   ```

### 3. GitHub 리포지토리에 업로드

#### 3.1 Git 초기화 및 파일 추가

1. **Git 초기화**
   ```bash
   git init
   ```

2. **파일 추가 및 커밋**
   ```bash
   git add .
   git commit -m "Initial commit with Kubernetes configurations"
   ```

#### 3.2 GitHub 리포지토리 생성 및 원격 설정

1. **GitHub 리포지토리 생성**
   - GitHub 웹사이트에서 새로운 리포지토리를 생성합니다.

2. **원격 리포지토리 추가**
   ```bash
   git remote add origin https://github.com/username/repository.git
   ```

3. **코드 푸시**
   ```bash
   git push -u origin master
   ```

### 예제 프로젝트 디렉토리 구조

```
.
├── deployment.yaml
├── pod.yaml
├── service.yaml
└── README.md
```

### README.md 파일 작성 예시

```markdown
# Kubernetes 실습 프로젝트

이 리포지토리는 Kubernetes 기본 개념 실습을 위한 예제 파일을 포함하고 있습니다.

## 파일 설명

- `pod.yaml`: Nginx 파드를 생성하기 위한 구성 파일.
- `service.yaml`: Nginx 파드를 노출하기 위한 서비스 구성 파일.
- `deployment.yaml`: Nginx 디플로이먼트를 생성하기 위한 구성 파일.

## 사용 방법

1. Minikube 클러스터 시작:
   ```bash
   minikube start
   ```

2. 파드 생성:
   ```bash
   kubectl apply -f pod.yaml
   ```

3. 서비스 생성:
   ```bash
   kubectl apply -f service.yaml
   ```

4. 디플로이먼트 생성:
   ```bash
   kubectl apply -f deployment.yaml
   ```
```

이 가이드를 따라 Kubernetes 실습을 진행하고, GitHub 리포지토리에 코드를 업로드할 수 있습니다. 추가적인 질문이 있으면 언제든지 말씀해 주세요.