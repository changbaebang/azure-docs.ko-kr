---
title: '빠른 시작: Azure CLI를 사용하여 기밀 컴퓨팅 노드가 있는 AKS(Azure Kubernetes Service) 클러스터 배포'
description: 기밀 노드가 있는 AKS 클러스터를 만들고, Azure CLI를 사용하여 hello world 앱을 배포하는 방법을 알아봅니다.
author: agowdamsft
ms.service: container-service
ms.topic: quickstart
ms.date: 2/25/2020
ms.author: amgowda
ms.openlocfilehash: 51b0813849236d9335d1482019f740fc8b23749f
ms.sourcegitcommit: c27a20b278f2ac758447418ea4c8c61e27927d6a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/03/2021
ms.locfileid: "101703289"
---
# <a name="quickstart-deploy-an-azure-kubernetes-service-aks-cluster-with-confidential-computing-nodes-dcsv2-using-azure-cli"></a>빠른 시작: Azure CLI를 사용하여 기밀 컴퓨팅 노드(DCsv2)가 있는 AKS(Azure Kubernetes Service) 클러스터 배포

이 빠른 시작은 AKS 클러스터를 빠르게 만들고 애플리케이션을 배포하여 Azure에서 관리형 Kubernetes 서비스를 사용하여 애플리케이션을 모니터링하려는 개발자 또는 클러스터 운영자를 위한 것입니다. Azure Portal에서 클러스터를 프로비저닝하고 기밀 컴퓨팅 노드를 추가할 수도 있습니다.

## <a name="overview"></a>개요

이 빠른 시작에서는 Azure CLI를 사용하여 기밀 컴퓨팅 노드가 있는 AKS(Azure Kubernetes Service) 클러스터를 배포하고, enclave에서 간단한 hello world 애플리케이션을 실행하는 방법에 대해 알아봅니다. AKS는 클러스터를 빠르게 배포하고 관리할 수 있는 관리형 Kubernetes 서비스입니다. AKS에 대한 자세한 내용은 [여기](../aks/intro-kubernetes.md)를 참조하세요.

> [!NOTE]
> 기밀 컴퓨팅 DCsv2 VM은 더 높은 가격 책정 및 지역 가용성이 적용되는 특별한 하드웨어를 활용합니다. 자세한 내용은 [사용 가능한 SKU 및 지원되는 지역](virtual-machine-solutions.md)에 대한 가상 머신 페이지를 참조하세요.

### <a name="confidential-computing-node-features-dcxs-v2"></a>기밀 컴퓨팅 노드 기능(DC<x>s-v2)

1. Linux 컨테이너를 지원하는 Linux 작업자 노드
1. Ubuntu 18.04 Virtual Machines 노드를 사용하는 2세대 VM
1. EPC(암호화된 페이지 캐시) 메모리가 있는 Intel SGX 기반 CPU. [여기](./faq.md)에서 자세히 알아보기
1. Kubernetes 버전 1.16+ 지원
1. AKS 노드에 미리 설치된 SGX DCAP 드라이버 [여기](./faq.md)에서 자세히 알아보기

## <a name="deployment-prerequisites"></a>배포 필수 조건
배포 자습서에는 다음이 필요합니다.

1. 활성화된 Azure 구독이 필요합니다. Azure 구독이 없는 경우 시작하기 전에 [체험 계정을 만듭니다](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).
1. Azure CLI 버전 2.0.64 이상이 배포 머신에 설치되고 구성되어 있어야 합니다(버전을 확인하려면 `az --version` 실행). 설치 또는 업그레이드해야 하는 경우 [Azure CLI 설치](../container-registry/container-registry-get-started-azure-cli.md)를 참조하세요.
1. 구독에서 사용할 수 있는 6개 이상의 **DC<x>s-v2** 코어 기본적으로 Azure 구독 8개 코어당 기밀 컴퓨팅에 대한 VM 코어 할당량입니다. 8개 초과된 코어가 필요한 클러스터를 프로비저닝하려면 [이러한](../azure-portal/supportability/per-vm-quota-requests.md) 지침에 따라 할당량 증가 티켓을 제출합니다.

## <a name="creating-new-aks-cluster-with-confidential-computing-nodes-and-add-on"></a>기밀 컴퓨팅 노드 및 추가 기능을 사용하여 새 AKS 클러스터 만들기
아래 지침에 따라 추가 기능을 사용하여 기밀 컴퓨팅 가능 노드를 추가합니다.

### <a name="step-1-creating-an-aks-cluster-with-system-node-pool"></a>1단계: 시스템 노드 풀을 사용하여 AKS 클러스터 만들기

위의 요구 사항을 충족하는 AKS 클러스터가 이미 있는 경우 [기존 클러스터 섹션으로 건너뛰어](#existing-cluster) 새 기밀 컴퓨팅 노드 풀을 추가합니다.

먼저, az group create 명령을 사용하여 클러스터에 대한 리소스 그룹을 만듭니다. 다음 예제에서는 *myResourceGroup* 이라는 리소스 그룹을 *westus2* 지역에 만듭니다.

```azurecli-interactive
az group create --name myResourceGroup --location westus2
```

이제 az aks create 명령을 사용하여 AKS 클러스터를 만듭니다.

```azurecli-interactive
# Create a new AKS cluster with system node pool with Confidential Computing addon enabled
az aks create -g myResourceGroup --name myAKSCluster --generate-ssh-keys --enable-addon confcom
```
위의 방법은 추가 기능이 사용하도록 설정된 시스템 노드 풀이 있는 새 AKS 클러스터를 만듭니다. 이제 AKS(DCsv2)에 기밀 컴퓨팅 노드 풀 유형의 사용자 노드를 추가하는 과정을 진행합니다.

### <a name="step-2-adding-confidential-computing-node-pool-to-aks-cluster"></a>2단계: AKS 클러스터에 기밀 컴퓨팅 노드 풀 추가 

3개의 노드가 있는 `Standard_DC2s_v2` 크기의 사용자 노드 풀에 아래 명령을 실행합니다. [여기](../virtual-machines/dcv2-series.md)서 지원되는 다른 DCsv2 SKU 목록을 선택할 수 있습니다.

```azurecli-interactive
az aks nodepool add --cluster-name myAKSCluster --name confcompool1 --resource-group myResourceGroup --node-vm-size Standard_DC2s_v2
```
위의 명령은 새 노드 풀(**DC<x>s-v2**)을 완료하고 기밀 컴퓨팅 추가 기능 DaemonSet([SGX Device Plugin](confidential-nodes-aks-overview.md#sgx-plugin))와 함께 표시되어야 합니다.
 
### <a name="step-3-verify-the-node-pool-and-add-on"></a>3단계: 노드 풀 및 추가 기능 확인
az aks get-credentials 명령을 사용하여 AKS 클러스터의 자격 증명을 가져옵니다.

```azurecli-interactive
az aks get-credentials --resource-group myResourceGroup --name myAKSCluster
```
아래와 같이 kubectl get pods 및 nodes 명령을 사용하여 노드가 올바르게 만들어지고 SGX 관련 디먼 세트가 **DC<x>s-v2** 노드 풀에서 실행되는지 확인합니다.

```console
$ kubectl get pods --all-namespaces

output
kube-system     sgx-device-plugin-xxxx     1/1     Running
```
출력이 위와 일치하면 이제 AKS 클러스터에서 기밀 애플리케이션을 실행할 준비가 된 것입니다.

[enclave에서 Hello World](#hello-world) 배포 섹션으로 이동하여 enclave의 앱을 테스트합니다. 또는 아래 지침에 따라 노드 풀을 AKS에 추가합니다(AKS는 SGX 노드 풀과 비 SGX 노드 풀의 혼합을 지원함).

## <a name="adding-confidential-computing-node-pool-to-existing-aks-cluster"></a>기존 AKS 클러스터에 기밀 컴퓨팅 노드 풀 추가<a id="existing-cluster"></a>

이 섹션에서는 필수 구성 요소 섹션에 나열된 조건을 충족하는 AKS 클러스터가 이미 실행되고 있다고 가정합니다(추가 기능에 적용).

### <a name="step-1-enabling-the-confidential-computing-aks-add-on-on-the-existing-cluster"></a>1단계: 기존 클러스터에서 기밀 컴퓨팅 AKS 추가 기능 사용

아래 명령을 실행하여 기밀 컴퓨팅 추가 기능을 사용하도록 설정합니다.

```azurecli-interactive
az aks enable-addons --addons confcom --name MyManagedCluster --resource-group MyResourceGroup 
```
### <a name="step-2-add-dcxs-v2-user-node-pool-to-the-cluster"></a>2단계: 클러스터에 **DC<x>s-v2** 사용자 노드 풀 추가
    
> [!NOTE]
> 기밀 컴퓨팅 기능을 사용하려면 기존 AKS 클러스터에 하나 이상의 **DC<x>s-v2** VM SKU 기반 노드 풀이 있어야 합니다. 기밀 컴퓨팅 DCsv2 VM SKU에 대한 자세한 내용은 여기에 [사용 가능한 SKU 및 지원되는 지역](virtual-machine-solutions.md)을 참조하세요.
    
  ```azurecli-interactive
az aks nodepool add --cluster-name myAKSCluster --name confcompool1 --resource-group myResourceGroup --node-count 1 --node-vm-size Standard_DC4s_v2

output node pool added

Verify

az aks nodepool list --cluster-name myAKSCluster --resource-group myResourceGroup
```
위의 명령은 confcompool1 이름으로 추가한 최근 노드 풀을 나열해야 합니다.

### <a name="step-3-verify-that-daemonsets-are-running-on-confidential-node-pools"></a>3단계: DaemonSet가 기밀 노드 풀에서 실행되고 있는지 확인

기존 AKS 클러스터에 로그인하여 아래 확인을 수행합니다. 

```console
kubectl get nodes
```
출력에 AKS 클러스터에 새로 추가된 confcompool1이 표시됩니다.

```console
$ kubectl get pods --all-namespaces

output (you may also see other daemonsets along SGX daemonsets as below)
kube-system     sgx-device-plugin-xxxx     1/1     Running
```
출력이 위와 일치하면 이제 AKS 클러스터에서 기밀 애플리케이션을 실행할 준비가 된 것입니다. 아래 테스트 애플리케이션 배포를 수행하세요.

## <a name="hello-world-from-isolated-enclave-application"></a>격리된 enclave 애플리케이션에서 Hello World <a id="hello-world"></a>
*hello-world-enclave.yaml* 이라는 파일을 만들고, 다음 YAML 매니페스트를 붙여넣습니다. 이 Open Enclave 기반 샘플 애플리케이션 코드는 [Open Enclave 프로젝트](https://github.com/openenclave/openenclave/tree/master/samples/helloworld)에서 찾을 수 있습니다. 아래 배포에서는 "confcom"이라는 추가 기능을 배포했다고 가정합니다.

```yaml
apiVersion: batch/v1
kind: Job
metadata:
  name: sgx-test
  labels:
    app: sgx-test
spec:
  template:
    metadata:
      labels:
        app: sgx-test
    spec:
      containers:
      - name: sgxtest
        image: oeciteam/sgx-test:1.0
        resources:
          limits:
            kubernetes.azure.com/sgx_epc_mem_in_MiB: 5 # This limit will automatically place the job into confidential computing node. Alternatively you can target deployment to nodepools
      restartPolicy: Never
  backoffLimit: 0
  ```

이제 다음 예제 출력과 같이 kubectl apply 명령을 사용하여 보안 enclave에서 시작할 샘플 작업을 만듭니다.

```console
$ kubectl apply -f hello-world-enclave.yaml

job "sgx-test" created
```

다음 명령을 실행하여 워크로드에서 신뢰할 수 있는 실행 환경(Enclave)을 성공적으로 만들었는지 확인할 수 있습니다.

```console
$ kubectl get jobs -l app=sgx-test
```

```console
$ kubectl get jobs -l app=sgx-test
NAME       COMPLETIONS   DURATION   AGE
sgx-test   1/1           1s         23s
```

```console
$ kubectl get pods -l app=sgx-test
```

```console
$ kubectl get pods -l app=sgx-test
NAME             READY   STATUS      RESTARTS   AGE
sgx-test-rchvg   0/1     Completed   0          25s
```

```console
$ kubectl logs -l app=sgx-test
```

```console
$ kubectl logs -l app=sgx-test
Hello world from the enclave
Enclave called into host to print: Hello World!
```

## <a name="clean-up-resources"></a>리소스 정리

연결된 노드 풀을 제거하거나 AKS 클러스터를 삭제하려면 아래 명령을 사용합니다.

AKS 클러스터를 삭제합니다.
``````azurecli-interactive
az aks delete --resource-group myResourceGroup --name myAKSCluster
```
Removing the confidential computing node pool

``````azurecli-interactive
az aks nodepool delete --cluster-name myAKSCluster --name myNodePoolName --resource-group myResourceGroup
``````

## <a name="next-steps"></a>다음 단계

[기밀 컨테이너 샘플](https://github.com/Azure-Samples/confidential-container-samples)을 방문하여 기밀 컨테이너를 통해 Python, Node 등의 애플리케이션을 기밀로 실행합니다.

[enclave 인식 Azure 컨테이너 샘플](https://github.com/Azure-Samples/confidential-computing/blob/main/containersamples/)을 방문하여 enclave 인식 애플리케이션을 실행합니다.
