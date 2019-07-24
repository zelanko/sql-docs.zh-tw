---
title: 使用 kubeadm 設定 Kubernetes
titleSuffix: SQL Server big data clusters
description: 瞭解如何在多個 Ubuntu 16.04 或18.04 部電腦 (實體或虛擬) 上設定 Kubernetes, 以進行 SQL Server 2019 big data cluster (預覽) 部署。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: ea79503869e7d403e4d3f4f960de9c95760eda0f
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419452"
---
# <a name="configure-kubernetes-on-multiple-machines-for-sql-server-big-data-cluster-deployments"></a>在多部電腦上設定 Kubernetes, 以進行 SQL Server big data cluster 部署

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文提供一個範例, 說明如何使用**kubeadm**來設定多部電腦上的 Kubernetes, 以進行 SQL Server 2019 big data cluster (預覽) 部署。 在此範例中, 有多個 Ubuntu 16.04 或 18.04 LTS 機器 (實體或虛擬) 為目標。 如果您要部署到不同的 Linux 平臺, 則必須改變一些命令以符合您的系統。  

> [!TIP] 
> 如需設定 Kubernetes 的範例腳本, 請參閱[在 Ubuntu 16.04 LTS 或 18.04 LTS 上使用 Kubeadm 建立 Kubernetes](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/kubeadm)叢集。

## <a name="prerequisites"></a>先決條件

- 至少3部 Linux 實體機器或虛擬機器
- 每一電腦的建議設定:
   - 8個 Cpu
   - 64 GB 的記憶體
   - 100 GB 的儲存空間

## <a name="prepare-the-machines"></a>準備機器

在每部電腦上, 有幾個必要的必要條件。 在 bash 終端機中, 在每部電腦上執行下列命令:

1. 將目前的電腦新增至`/etc/hosts`檔案:

   ```bash
   echo $(hostname -i) $(hostname) | sudo tee -a /etc/hosts
   ```

1. 停用所有裝置上的交換。

   ```bash
   sudo sed -i "/ swap / s/^/#/" /etc/fstab
   sudo swapoff -a
   ```

1. 匯入金鑰, 並註冊 Kubernetes 的存放庫。

   ```bash
   sudo curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
   echo 'deb http://apt.kubernetes.io/ kubernetes-xenial main' | sudo tee -a /etc/apt/sources.list.d/kubernetes.list
   ```

1. 在電腦上設定 docker 和 Kubernetes 必要條件。

   ```bash
   KUBE_DPKG_VERSION=1.11.3-00
   sudo apt-get update && /
   sudo apt-get install -y ebtables ethtool && /
   sudo apt-get install -y docker.io && /
   sudo apt-get install -y apt-transport-https && /
   sudo apt-get install -y kubelet=$KUBE_DPKG_VERSION kubeadm=$KUBE_DPKG_VERSION kubectl=$KUBE_DPKG_VERSION && /
   curl https://raw.githubusercontent.com/kubernetes/helm/master/scripts/get | bash
   ```
 
1. 設定 `net.bridge.bridge-nf-call-iptables=1`。 在 Ubuntu 18.04 上, 下列命令會先`br_netfilter`啟用。

   ```bash
   . /etc/os-release
   if [ "$VERSION_CODENAME" == "bionic" ]; then sudo modprobe br_netfilter; fi
   sudo sysctl net.bridge.bridge-nf-call-iptables=1
   ```

## <a name="configure-the-kubernetes-master"></a>設定 Kubernetes 主機

在每部電腦上執行上述命令之後, 請選擇其中一部電腦做為您的 Kubernetes 主機。 然後在該電腦上執行下列命令。

1. 首先, 使用下列命令, 在您的目前的目錄中建立 yaml 檔案。 

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

1. 初始化這部電腦上的 Kubernetes 主伺服器。 您應該會看到 Kubernetes 主機已成功初始化的輸出。

   ```bash
   KUBE_VERSION=1.11.3
   sudo kubeadm init --pod-network-cidr=10.244.0.0/16 --kubernetes-version=$KUBE_VERSION
   ```

1. 請注意`kubeadm join` , 您需要在其他伺服器上用來加入 Kubernetes 叢集的命令。 複製此版本以供稍後使用。

   ![kubeadm 聯結](./media/deploy-with-kubeadm/kubeadm-join.png)

1. 設定 Kubernetes 設定檔您的主目錄。

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

其他機器將作為叢集中的 Kubernetes 代理程式。 

在每部其他電腦上, 執行您在`kubeadm join`上一節中複製的命令。

![kubeadm 聯結代理程式](./media/deploy-with-kubeadm/kubeadm-join-agents.png)

## <a name="view-the-cluster-status"></a>查看叢集狀態

若要確認與叢集的連線, 請使用[kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands)命令來傳回叢集節點的清單。

```bash
kubectl get nodes
```

## <a name="next-steps"></a>後續步驟

這篇文章中的步驟已在多部 Ubuntu 電腦上設定 Kubernetes 叢集。 下一步是部署 SQL Server 2019 big data 叢集。 如需指示, 請參閱下列文章:

[在 Kubernetes 上部署 SQL Server](deployment-guidance.md#deploy)
