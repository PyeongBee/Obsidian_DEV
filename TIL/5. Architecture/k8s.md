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
- `type: Recreate`
	- replicaSet v1 -> v2 완전히 Terminate 후 재생성하여 배포
	![[Pasted image 20240703211702.png]]
- `type: RollingUpdate`
	- replicaSet v2 pod를 하나씩 생성하고 v1 pod를 하나씩 제거하면서 점진적으로 배포
	![[Pasted image 20240703212832.png]]
	
### Service
- Pod로 고정주소를 사용하여 접근할 수 있도록 하는 오브젝트
- 이게 무슨 말일까? Pod는 계속해서 생성되고 삭제되기 때문에, 주소가 계속 달라진다.
- user가 이 변경되는 주소를 계속 따라갈 수가 없기 때문에 Service라는 고정 주소의 객체를 두고, user는 이 Service 객체를 접근하게 한다.
- Service는 어떻게 pod를 추적할까? -> `pod의 selector의 app label로 접근한다`
- Service는 어떻게 부하를 분산할까? -> `round robin 방식으로 pod를 선택한다`
- service 객체에는 다음과 같은 종류들이 있다.
	- ClusterIP
		- 쿠버네티스 클러스터 내부 전용 가상 IP엔드포인트를 제공하는 로드밸런서 구성(L4)
		- 내부에서만 사용 가능하기 때문에, 이것만으로는 접근 불가!
		- 외부에서 접근하려면, proxy/NodePort가 필요하다.
	- NodePort
		- pod들이 올라가 있는 node에 port를 뚫어서, 그 port가 엔드포인트가 된다
		- 근데, 그 worker node 아무개가 내려간다면? 자동으로 다른 노드를 통해 접근을 하는 게 불가능하다
		- 이를 해결하기 위해 LoadBalancer를 사용한다.
		![[Pasted image 20240703220135.png]]
	- LoadBalancer
		- NodePort타입 앞단에 Loadbalancer가 붙어서 살아있는 노드를 체크하여 접근 가능하다

			![[Pasted image 20240703220201.png]]

### Ingress
- 서비스에 대한 외부 접근을 관리하는 API 오브젝트

### Volume
- 컨테이너가 사용하는 데이터를 관리하는 오브젝트

### Configmap, Secret
- 환경변수를 관리하는 오브젝트