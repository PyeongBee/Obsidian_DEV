### Kubernetes Object
- Pod
- Namespace
- Replicaset
- Deployment
- Service
- Ingress
- Volume
- ConfigMap
- Secret

#### Object의 field
- `Spec` 정의된 상태
- `Status` 현재 상태
- `k8s controller`가 `Spec`과 `Status`가 계속해서 일치하도록 유지하도록 함

### Pod
- 쿠버네티스 클러스터를 구성하는 가장 최소 단위 오브젝트
- 하나의 Worker Node에는 N개의 Pod가 있다. 상황에 따라 그 수가 늘었다가 줄었다가 한다.
- 또한, 하나의 Pod 안에는 N개의 Container가 있을 수 있다. 하지만, 하나의 Pod 안에는 하나의 Container만 구성하는 것이 권장사항이다.
- `참고!` pod는 스스로 `auto healing, auto scaling`이 불가능하다. `k8s controller`가 제어한다.
- `중요!` pod는 일시적이다. 언제든지 생성되고 제거될 수 있다. pod에는 중요한 데이터를 저장하지 않아야 한다.

### Namespace
- 리소스의 그룹화 목적으로 사용되는 워크스페이스
- 동일한 단일 클러스터 내 가상 클러스터 구분
- 클러스터는 기본적으로 default namespace가 있다.

### Replicaset
- pod N개의 복제본을 유지하도록 한다.

### Deployment
- Pod의 자동복구, 버전 업데이트 및 롤백

### Service
- Pod로 고정주소를 사용하여 접근할 수 있도록 하는 오브젝트

### Ingress
- 서비스에 대한 외부 접근을 관리하는 API 오브젝트

### Volume
- 컨테이너가 사용하는 데이터를 관리하는 오브젝트

### Configmap, Secret
- 환경변수를 관리하는 오브젝트