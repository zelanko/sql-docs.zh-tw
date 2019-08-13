---
title: 設定 minikube
titleSuffix: SQL Server big data clusters
description: 了解如何在單一電腦上針對 SQL Server 2019 巨量資料叢集 (預覽) 部署設定 minikube。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 04/23/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 6c2261b5cfbbe590c76ce410da4b95ee678a20b5
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/25/2019
ms.locfileid: "67958479"
---
# <a name="configure-minikube-for-sql-server-big-data-cluster-deployments"></a>針對 SQL Server 巨量資料叢集部署設定 minikube

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文描述如何在單一電腦上針對 SQL Server 2019 巨量資料叢集 (預覽) 部署設定 **minikube**。 Minikube 是可讓您在單一電腦 (例如膝上型電腦或桌上型電腦) 上輕鬆執行 Kubernetes 的工具。 Minikube 會在您膝上型電腦的 VM 中，為想要試用 Kubernetes 或每天使用它進行開發的使用者，執行單一節點的 Kubernetes 叢集。 

## <a name="prerequisites"></a>Prerequisites

- 32 GB 記憶體 (建議使用 64 GB)。

- 如果電腦只有建議的最小記憶體，請將叢集部署設定為只有 1 個計算集區執行個體、1 個資料集區執行個體及 1 個存放集區執行個體。 此組態只能用於資料持久性和可用性不重要的評估環境。 如需用於設定資料集區、計算集區和存放集區複本數目的環境變數詳細資訊，請參閱[部署文件](deployment-guidance.md#configfile)。

- 您必須在電腦的 BIOS 中啟用 VT-x 或 AMD-v 虛擬化。

## <a name="install-dependencies"></a>安裝相依性

1. 安裝 [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)。

1. 安裝 Python 3：
   - 如果遺漏 pip，請下載 [get-clspip.py](https://bootstrap.pypa.io/get-pip.py) 並執行 `python get-pip.py`。
   - 使用 `python -m pip install requests` 安裝要求套件。

1. 如果您尚未安裝 Hypervisor，請立即安裝。
   - 若是 OS X，請安裝 [xhyve 驅動程式](https://git.k8s.io/minikube/docs/drivers.md)、[VirtualBox](https://www.virtualbox.org/wiki/Downloads) 或 [VMware Fusion](https://www.vmware.com/products/fusion)。
   - 若是 Linux，請安裝 [VirtualBox](https://www.virtualbox.org/wiki/Downloads) 或 [KVM](https://www.linux-kvm.org/)。
   - 若是 Windows，請安裝 [VirtualBox](https://www.virtualbox.org/wiki/Downloads) 或 [Hyper-V](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install)。 如果未在 Hyper-V 中設定外部交換器，請建立一個可存取外部網路的交換器。  了解如何[在 Hyper-V 中為 minikube 建立外部交換器](https://blogs.msdn.microsoft.com/wasimbloch/2017/01/23/setting-up-kubernetes-on-windows10-laptop-with-minikube/)。

## <a name="install-minikube"></a>安裝 minikube

請根據 [v0.28.2 版](https://github.com/kubernetes/minikube/releases/tag/v0.28.2)的指示來安裝 minikube。 SQL Server 2019 巨量資料叢集 (預覽) 僅適用於 v0.24.1 版和更新版本。

## <a name="create-a-minikube-cluster"></a>建立 minikube 叢集

下列命令會在具有 8 CPU、28 GB 記憶體和磁碟大小 100 GB 的 Hyper-V VM 中建立 minikube 叢集。 磁碟大小不是保留空間。  它會視需要調整到該磁碟大小。  建議您不要將磁碟空間變更為低於 100 GB，因為此情形在我們測試時遇到問題。 這也會明確指定 Hyper-V 交換器的外部存取功能。

請根據您的可用硬體及所要使用的 Hypervisor，視需要變更 **--memory** 等參數。  確定 **--hyper-v** 虛擬交換器參數值符合您在建立虛擬交換器時所使用的名稱。

```bash
minikube start --vm-driver="hyperv" --cpus 8 --memory 28672 --disk-size 100g --hyperv-virtual-switch "External"
```

如果您想要搭配 VirtualBox 使用 minikube，命令會如下所示：

```base
minikube start --cpus 8 --memory 28672 --disk-size 100g
```

## <a name="disable-automatic-checkpoint-with-hyper-v"></a>停用 Hyper-V 的自動檢查點

在 Windows 10，已在 VM 上啟用自動檢查點。 在 PowerShell 中執行下列命令，停用 VM 上的自動檢查點。

```PowerShell
Set-VM -Name minikube -CheckpointType Disabled -AutomaticCheckpointsEnabled $false
```

## <a name="next-steps"></a>後續步驟

本文中的步驟設定了 minikube 叢集。 下一個步驟是部署 SQL Server 2019 巨量資料叢集。 如需指示，請參閱下列文章：

[在 Kubernetes 上部署 SQL Server 2019 巨量資料叢集](deployment-guidance.md#deploy)
