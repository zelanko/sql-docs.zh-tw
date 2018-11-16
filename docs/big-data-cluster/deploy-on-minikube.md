---
title: 設定適用於 SQL Server 2019 巨量資料叢集部署的 Minikube |Microsoft Docs
description: 了解如何設定 Minikube 適用於在單一機器上的 SQL Server 2019 巨量資料叢集 （預覽） 部署。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 11/06/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 9b6902057c3bf5da706de8832b33c959ed285a9b
ms.sourcegitcommit: 50b60ea99551b688caf0aa2d897029b95e5c01f3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/15/2018
ms.locfileid: "51702346"
---
# <a name="configure-minikube-for-sql-server-2019-big-data-cluster-deployments"></a>設定適用於 SQL Server 2019 巨量資料叢集部署的 Minikube

這篇文章說明如何設定**minikube**適用於 SQL Server 2019 巨量資料叢集 （預覽） 部署在單一電腦上。 Minikube 是一種工具，輕鬆地執行類似的桌上型或膝上型電腦在單一機器上的 Kubernetes。 Minikube 會執行使用者想要試用 Kubernetes，或使用它進行開發的膝上型電腦上每日的 VM 內的單一節點 Kubernetes 叢集。 

## <a name="prerequisites"></a>先決條件

- 若要執行 Minikube 叢集 SQL Server 2019 CTP 2.1 SQL 巨量資料叢集組態，建議您的電腦必須至少 32 GB 的 RAM。

   > [!TIP] 
   > 如果機器有建議的記憶體最小值，然後設定叢集有 1 個計算集區執行個體、 1 個資料集區執行個體和 1 個儲存體集區執行個體的部署。 這項設定應該只用於評估環境，持久性和可用性的資料不重要。 請參閱[部署文件](deployment-guidance.md#define-environment-variables)如需有關設定來設定資料集區的複本數目的環境變數的詳細資訊，請計算集區和儲存體集區。

- 必須在您電腦的 BIOS 中啟用 VT x 或 amd-v 的虛擬化。

## <a name="install-dependencies"></a>安裝相依項目

1. 如果尚未安裝，安裝在本機上的 git [Windows](https://git-for-windows.github.io/)， [Linux 或 Mac](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)。

1. 安裝[kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)。

1. Instalovat Python 3:
   - 如果遺漏的 pip，請下載[get clspip.py](https://bootstrap.pypa.io/get-pip.py)並執行`python get-pip.py`。
   - 封裝使用的安裝要求`python -m pip install requests`。

1. 如果您還沒有安裝 」 的 hypervisor，現在安裝一個。
   - OS x 安裝[xhyve driver](https://git.k8s.io/minikube/docs/drivers.md)， [VirtualBox](https://www.virtualbox.org/wiki/Downloads)，或[VMware Fusion](https://www.vmware.com/products/fusion)。
   - 針對 Linux，安裝[VirtualBox](https://www.virtualbox.org/wiki/Downloads)或是[KVM](https://www.linux-kvm.org/)。
   - 對於 Windows，安裝[VirtualBox](https://www.virtualbox.org/wiki/Downloads)或是[HYPER-V](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install)。 如果您沒有外部交換器在 hyper-v 中設定，然後建立一個具有 「 外部網路存取權。  請參閱如何[minikube 的 hyper-v 中建立外部交換器](https://blogs.msdn.microsoft.com/wasimbloch/2017/01/23/setting-up-kubernetes-on-windows10-laptop-with-minikube/)。

## <a name="install-minikube"></a>安裝 Minikube

根據的指示安裝 Minikube [v0.28.2 版本](https://github.com/kubernetes/minikube/releases/tag/v0.28.2)。 SQL Server 2019 CTP 2.1 版本 v0.24.1 與設定，僅適用於巨量資料叢集。

## <a name="create-a-minikube-cluster"></a>建立 Minikube 叢集

下列命令會建立 minikube 叢集，在具有 8 個 Cpu 的 HYPER-V VM、 28 GB 記憶體，而 100 gb 的磁碟大小。 磁碟大小不是保留的空間。  它會隨著該大小在磁碟上所需。  我們建議您不要變更 磁碟空間為小於 100 GB，我們遇到中測試此問題。 這也會指定 hyper-v 交換器的外部存取明確。

這類變更的參數 **-記憶體**取決於您可用的硬體和會視您使用的 hypervisor。  請確定 **-hyper-v**虛擬交換器的參數值符合建立您的虛擬交換器時所使用的名稱。

```bash
minikube start --vm-driver="hyperv" --cpus 8 --memory 28672 --disk-size 100g --hyperv-virtual-switch "External"
```

如果您使用 VirtualBox Minikube 命令會如下所示：

```base
minikube start --cpus 8 --memory 28672 --disk-size 100g
```

## <a name="disable-automatic-checkpoint-with-hyper-v"></a>停用 hyper-v 的自動檢查點

Windows 10 上的 VM 上啟用自動的檢查點。 若要停用自動檢查點，在 VM 上的 PowerShell 中執行下列命令。

```PowerShell
Set-VM -Name minikube -CheckpointType Disabled -AutomaticCheckpointsEnabled $false
```

## <a name="next-steps"></a>後續步驟

這篇文章中的步驟設定 Minikube 叢集。 下一個步驟是將 SQL Server 2019 巨量資料叢集部署。 如需指示，請參閱下列文章：

[將 SQL Server 2019 CTP 2.1 在 Kubernetes 上部署](deployment-guidance.md#deploy)
