---
title: 設定 minikube
titleSuffix: SQL Server big data clusters
description: 瞭解如何在單一電腦上[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]設定部署的 minikube。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: b2022fe6ad8a0aa23c4dd7d917e925ae1daba572
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/20/2019
ms.locfileid: "69652409"
---
# <a name="configure-minikube-for-sql-server-big-data-cluster-deployments"></a>針對 SQL Server 巨量資料叢集部署設定 minikube

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文說明如何在單一電腦上設定**minikube**以進行[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]部署。 Minikube 是可讓您在單一電腦 (例如膝上型電腦或桌上型電腦) 上輕鬆執行 Kubernetes 的工具。 Minikube 會在您膝上型電腦的 VM 中，為想要試用 Kubernetes 或每天使用它進行開發的使用者，執行單一節點的 Kubernetes 叢集。 

## <a name="prerequisites"></a>必要條件

- 64 GB 的記憶體。

- 如果電腦只有建議的最小記憶體，請將叢集部署設定為只有 1 個計算集區執行個體、1 個資料集區執行個體及 1 個存放集區執行個體。 此組態只能用於資料持久性和可用性不重要的評估環境。 如需用於設定資料集區、計算集區和存放集區複本數目的環境變數詳細資訊，請參閱[部署文件](deployment-guidance.md#configfile)。

- 您必須在電腦的 BIOS 中啟用 VT-x 或 AMD-v 虛擬化。

## <a name="install-dependencies"></a>安裝相依性

1. 安裝 [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)。

1. 如果您尚未安裝 Hypervisor，請立即安裝。
   - 若是 OS X，請安裝 [xhyve 驅動程式](https://git.k8s.io/minikube/docs/drivers.md)、[VirtualBox](https://www.virtualbox.org/wiki/Downloads) 或 [VMware Fusion](https://www.vmware.com/products/fusion)。
   - 若是 Linux，請安裝 [VirtualBox](https://www.virtualbox.org/wiki/Downloads) 或 [KVM](https://www.linux-kvm.org/)。
   - 若是 Windows，請安裝 [VirtualBox](https://www.virtualbox.org/wiki/Downloads) 或 [Hyper-V](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install)。 如果您沒有在 Hyper-v 中設定的外部交換器, 請建立一個具有外部網路存取權的交換器。 瞭解如何[在 hyper-v 中建立 minikube 的外部交換器](https://blogs.msdn.microsoft.com/wasimbloch/2017/01/23/setting-up-kubernetes-on-windows10-laptop-with-minikube/)。

## <a name="install-minikube"></a>安裝 minikube

根據[1.3.0 版本](https://github.com/kubernetes/minikube/releases/tag/v1.3.0)的指示安裝 minikube 版本。 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]僅適用于1.0.0 版和更新版本。

## <a name="create-a-minikube-cluster"></a>建立 minikube 叢集

下列命令會在 Hyper-v VM 中建立具有8個 Cpu 的 minikube 叢集、64 GB 的記憶體, 以及 100 GB 的磁片大小。 磁碟大小不是保留空間。  它會視需要調整到該磁碟大小。  建議您不要將磁碟空間變更為低於 100 GB，因為此情形在我們測試時遇到問題。 這也會明確指定具有外部存取權的 Hyper-v 交換器。

請根據您的可用硬體及所要使用的 Hypervisor，視需要變更 **--memory** 等參數。  確定 **--hyper-v** 虛擬交換器參數值符合您在建立虛擬交換器時所使用的名稱。

```bash
minikube start --vm-driver="hyperv" --cpus 8 --memory 65536 --disk-size 100g --hyperv-virtual-switch "External"
```

如果您想要搭配 VirtualBox 使用 minikube，命令會如下所示：

```base
minikube start --cpus 8 --memory 65536 --disk-size 100g
```

## <a name="disable-automatic-checkpoint-with-hyper-v"></a>停用 Hyper-V 的自動檢查點

在 Windows 10，已在 VM 上啟用自動檢查點。 在 PowerShell 中執行下列命令, 以停用 VM 上的自動檢查點, 並將記憶體設定為靜態。

```PowerShell
Set-VM -Name minikube -CheckpointType Disabled -AutomaticCheckpointsEnabled $false -StaticMemory
```

## <a name="next-steps"></a>後續步驟

本文中的步驟設定了 minikube 叢集。 下一個步驟是部署 SQL Server 2019 巨量資料叢集。 如需指示，請參閱下列文章：

[在[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] Kubernetes 上部署](deployment-guidance.md#deploy)
