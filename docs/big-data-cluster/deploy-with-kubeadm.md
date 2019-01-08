---
title: 使用 kubeadm 設定 Kubernetes
titleSuffix: SQL Server 2019 big data clusters
description: 了解如何設定多個 Ubuntu 16.04 上的 Kubernetes 或適用於 SQL Server 2019 巨量資料叢集 （預覽） 部署的 18.04 機器 （實體或虛擬）。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 12/07/2018
ms.topic: conceptual
ms.prod: sql
ms.custom: seodec18
ms.openlocfilehash: 7b6c6aeced930bfdd17915e2acc130fc4446f4a5
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/11/2018
ms.locfileid: "53210277"
---
# <a name="configure-kubernetes-on-multiple-machines-for-sql-server-2019-big-data-cluster-preview-deployments"></a>設定適用於 SQL Server 2019 巨量資料叢集 （預覽） 部署的多部電腦上的 Kubernetes

這篇文章提供如何使用的範例**kubeadm**設定適用於 SQL Server 2019 巨量資料叢集 （預覽） 部署的多部電腦上的 Kubernetes。 在此範例中，多個 Ubuntu 16.04 或 18.04 LTS 機器 （實體或虛擬） 為目標。 如果您要部署到不同的 Linux 平台，您必須更改一些命令，以符合您的系統。  

> [!TIP] 
> 如需設定 Kubernetes 的範例指令碼，請參閱[建立 Kubernetes 叢集使用 Ubuntu 16.04 LTS 或 18.04 LTS Kubeadm](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/kubeadm)。

## <a name="prerequisites"></a>先決條件

- 多個 Linux 實體機器或虛擬機器使用叢集
- 建議的設定：8 個 Cpu，32 GB 的記憶體，並至少 100 GB 的每個機器的存放裝置
- 在叢集中的三部機器的最小值

## <a name="prepare-the-machines"></a>準備機器

在每一部機器，有數個所需的必要條件。 在 bash 終端機中，請在每部機器上執行下列命令：

1. 加入目前機器`/etc/hosts`檔案：

   ```bash
   echo $(hostname -i) $(hostname) | sudo tee -a /etc/hosts
   ```

1. 停用所有裝置上交換。

   ```bash
   sudo sed -i "/ swap / s/^/#/" /etc/fstab
   sudo swapoff -a
   ```

1. 匯入金鑰，並針對 Kubernetes 註冊存放庫。

   ```bash
   sudo curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
   echo 'deb http://apt.kubernetes.io/ kubernetes-xenial main' | sudo tee -a /etc/apt/sources.list.d/kubernetes.list
   ```

1. 在電腦上設定 docker 和 Kubernetes 的必要條件。

   ```bash
   KUBE_DPKG_VERSION=1.11.3-00
   sudo apt-get update && /
   sudo apt-get install -y ebtables ethtool && /
   sudo apt-get install -y docker.io && /
   sudo apt-get install -y apt-transport-https && /
   sudo apt-get install -y kubelet=$KUBE_DPKG_VERSION kubeadm=$KUBE_DPKG_VERSION kubectl=$KUBE_DPKG_VERSION && /
   curl https://raw.githubusercontent.com/kubernetes/helm/master/scripts/get | bash
   ```
 
1. 設定 `net.bridge.bridge-nf-call-iptables=1`。 在 Ubuntu 18.04，下列命令先啟用`br_netfilter`。

   ```bash
   . /etc/os-release
   if [ "$VERSION_CODENAME" == "bionic" ]; then sudo modprobe br_netfilter; fi
   sudo sysctl net.bridge.bridge-nf-call-iptables=1
   ```

## <a name="configure-the-kubernetes-master"></a>Kubernetes 主機設定

執行之後的前一個命令在每部機器上，選擇其中一個是您 Kubernetes 主機的機器。 然後的樂趣在該電腦上的下列命令。

1. 首先，在您目前的目錄，使用下列命令建立 rbac.yaml 檔案。 

   ```bash
   cat <<EOF > rbac.yaml
   apiVersion: rbac.authorization.k8s.io/v1beta1
   kind: ClusterRoleBinding
   metadata:
     name: default-rbac
   subjects:
   - kind: ServiceAccount
     name: default
     namespace: default
   roleRef:
     kind: ClusterRole
     name: cluster-admin
     apiGroup: rbac.authorization.k8s.io
   EOF
   ```

1. 初始化這部電腦上的 Kubernetes 主機。 您應該會看到已成功初始化 Kubernetes 主機的輸出。

   ```bash
   KUBE_VERSION=1.11.3
   sudo kubeadm init --pod-network-cidr=10.244.0.0/16 --kubernetes-version=$KUBE_VERSION
   ```

1. 請注意`kubeadm join`命令，您需要使用其他伺服器上加入 Kubernetes 叢集。 將此複製以供稍後使用。

   ![kubeadm 聯結](./media/deploy-with-kubeadm/kubeadm-join.png)

1. 您的主目錄設定 Kubernetes 組態檔。

   ```bash
   mkdir -p $HOME/.kube
   sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
   sudo chown $(id -u):$(id -g) $HOME/.kube/config
   ```

1. 設定叢集和 Kubernetes 儀表板。

   ```bash
   kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml
   helm init
   kubectl apply -f rbac.yaml
   kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/master/src/deploy/recommended/kubernetes-dashboard.yaml
   kubectl create clusterrolebinding kubernetes-dashboard --clusterrole=cluster-admin --serviceaccount=kube-system:kubernetes-dashboard
   ```

## <a name="configure-the-kubernetes-agents"></a>設定 Kubernetes 代理程式

其他電腦將做為 Kubernetes 叢集中的代理程式。 

在每個其他機器上執行`kubeadm join`您在上一節中複製的命令。

![kubeadm 聯結代理程式](./media/deploy-with-kubeadm/kubeadm-join-agents.png)

## <a name="view-the-cluster-status"></a>檢視叢集狀態

若要驗證您的叢集連線，請使用[kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands)命令來傳回叢集節點的清單。

```bash
kubectl get nodes
```

## <a name="next-steps"></a>後續步驟

這篇文章中的步驟設定多部 Ubuntu 電腦上的 Kubernetes 叢集。 下一個步驟是將 SQL Server 2019 巨量資料叢集部署。 如需指示，請參閱下列文章：

[部署 SQL Server 2019 CTP 2.2 上 Kubernetes](deployment-guidance.md#deploy)
