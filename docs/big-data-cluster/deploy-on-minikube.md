---
title: 設定 minikube
titleSuffix: SQL Server big data clusters
description: 了解如何設定適用於 SQL Server 2019 巨量資料叢集 （預覽） 部署 minikube 在單一電腦上。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 04/23/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 6c2261b5cfbbe590c76ce410da4b95ee678a20b5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67958479"
---
# <a name="configure-minikube-for-sql-server-big-data-cluster-deployments"></a>設定適用於 SQL Server 的巨量資料叢集部署的 minikube

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

這篇文章說明如何設定**minikube**適用於 SQL Server 2019 巨量資料叢集 （預覽） 部署在單一電腦上。 Minikube 是一種工具，輕鬆地執行類似的桌上型或膝上型電腦在單一機器上的 Kubernetes。 Minikube 會執行使用者想要試用 Kubernetes，或使用它進行開發的膝上型電腦上每日的 VM 內的單一節點 Kubernetes 叢集。 

## <a name="prerequisites"></a>先決條件

- 32 GB 的記憶體 (建議的 64 GB)。

- 如果機器有建議的記憶體最小值，然後設定叢集有 1 個計算集區執行個體、 1 個資料集區執行個體和 1 個儲存體集區執行個體的部署。 這項設定應該只用於評估環境，持久性和可用性的資料不重要。 請參閱[部署文件](deployment-guidance.md#configfile)如需有關設定來設定資料集區的複本數目的環境變數的詳細資訊，請計算集區和儲存體集區。

- 必須在您電腦的 BIOS 中啟用 VT x 或 amd-v 的虛擬化。

## <a name="install-dependencies"></a>安裝相依項目

1. 安裝[kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)。

1. Instalovat Python 3:
   - 如果遺漏的 pip，請下載[get clspip.py](https://bootstrap.pypa.io/get-pip.py)並執行`python get-pip.py`。
   - 封裝使用的安裝要求`python -m pip install requests`。

1. 如果您還沒有安裝 」 的 hypervisor，現在安裝一個。
   - OS x 安裝[xhyve driver](https://git.k8s.io/minikube/docs/drivers.md)， [VirtualBox](https://www.virtualbox.org/wiki/Downloads)，或[VMware Fusion](https://www.vmware.com/products/fusion)。
   - 針對 Linux，安裝[VirtualBox](https://www.virtualbox.org/wiki/Downloads)或是[KVM](https://www.linux-kvm.org/)。
   - 對於 Windows，安裝[VirtualBox](https://www.virtualbox.org/wiki/Downloads)或是[HYPER-V](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install)。 如果您沒有外部交換器在 hyper-v 中設定，然後建立一個具有 「 外部網路存取權。  請參閱如何[minikube 的 hyper-v 中建立外部交換器](https://blogs.msdn.microsoft.com/wasimbloch/2017/01/23/setting-up-kubernetes-on-windows10-laptop-with-minikube/)。

## <a name="install-minikube"></a>安裝 minikube

安裝的指示根據 minikube [v0.28.2 版本](https://github.com/kubernetes/minikube/releases/tag/v0.28.2)。 使用版本 v0.24.1 和向上，僅適用於 SQL Server 2019 巨量資料叢集 （預覽）。

## <a name="create-a-minikube-cluster"></a>建立 minikube 叢集

下列命令會建立 minikube 叢集，在具有 8 個 Cpu 的 HYPER-V VM、 28 GB 記憶體，而 100 gb 的磁碟大小。 磁碟大小不是保留的空間。  它會隨著該大小在磁碟上所需。  我們建議您不要變更 磁碟空間為小於 100 GB，我們遇到中測試此問題。 這也會指定 hyper-v 交換器的外部存取明確。

這類變更的參數 **-記憶體**取決於您可用的硬體和會視您使用的 hypervisor。  請確定 **-hyper-v**虛擬交換器的參數值符合建立您的虛擬交換器時所使用的名稱。

```bash
minikube start --vm-driver="hyperv" --cpus 8 --memory 28672 --disk-size 100g --hyperv-virtual-switch "External"
```

如果您使用 VirtualBox minikube 命令會如下所示：

```base
minikube start --cpus 8 --memory 28672 --disk-size 100g
```

## <a name="disable-automatic-checkpoint-with-hyper-v"></a>停用 hyper-v 的自動檢查點

Windows 10 上的 VM 上啟用自動的檢查點。 若要停用自動檢查點，在 VM 上的 PowerShell 中執行下列命令。

```PowerShell
Set-VM -Name minikube -CheckpointType Disabled -AutomaticCheckpointsEnabled $false
```

## <a name="next-steps"></a>後續步驟

這篇文章中的步驟設定 minikube 叢集。 下一個步驟是將 SQL Server 2019 巨量資料叢集部署。 如需指示，請參閱下列文章：

[部署在 Kubernetes 上的 SQL Server 2019 巨量資料叢集](deployment-guidance.md#deploy)
