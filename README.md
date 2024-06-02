# 개요
* kubernetse 임시 볼륨(ephemeral volume)을 잘못 사용하여 장애 발생하는 시나리오 재현

# 테스트 환경 구축 방법
* [로컬에서 테스트 - kind](./install_kubernetes/kind/)
* [EKS](./install_kubernetes/eks/)

# 테스트 방법

1. node label 설정

```sh
kubectl label node {node이름} env=test
```

2. emptydir pod에서 파일을 생성하면 어디에 생성될까?

```sh
kubectl apply -f ./manifests/emptydir/busybox.yaml
```

3. 임시 볼륨을 다 쓰도록 디스크 용량 부하 발생

```sh
kubectl apply -f ./manifests/emptydir/stress.yaml
```

4. (옵션) EKS에서 nginx 배포: 다른 pod의 임시볼륨때문에 nginx ALB가 호출안되는 것을 테스트하는 예제

```sh
kubectl apply -f ./manifests/eks/nginx
```


# 테스트 기록
* [문서 바로가기](./documents/)
