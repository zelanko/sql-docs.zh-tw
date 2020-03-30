---
title: 部署單一節點 kubeadm 叢集
titleSuffix: SQL Server Big Data Clusters
description: 使用 Bash 部署指令碼，將 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] 部署至單一節點 kubeadm 叢集。
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.metadata: seo-lt-2019
ms.date: 12/13/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: f60256e58339387323f923c85d2b880459455663
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "75252095"
---
# <a name="deploy-with-a-bash-script-to-a-single-node-kubeadm-cluster"></a>使用 Bash 指令碼部署至單一節點 kubeadm 叢集

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

在本教學課程中，您會使用範例 Bash 部署指令碼，利用 kubeadm 和 SQL Server 巨量資料叢集來部署單一節點 Kubernetes 叢集。

## <a name="prerequisites"></a>Prerequisites

- Vanilla Ubuntu 18.04 或 16.04 **伺服器**虛擬或實體機器。 所有相依性都由指令碼設定，您可以從 VM 內執行指令碼。

  > [!NOTE]
  > 尚不支援使用 Azure Linux VM。

- VM 至少應有 8 個 CPU、64 GB RAM 和 100 GB 的磁碟空間。 在提取所有巨量資料叢集 Docker 映像之後，您將會剩下用於所有元件的 50 GB 資料和記錄檔。

- 使用下方命令來更新現有套件，以確保 OS 映像是最新的。

   ``` bash
   sudo apt update && sudo apt upgrade -y
   sudo systemctl reboot
   ```

## <a name="recommended-virtual-machine-settings"></a>建議的虛擬機器設定

1. 針對虛擬機器使用靜態記憶體設定。 例如，在 Hyper-V 安裝中，請勿使用動態記憶體配置，而是改為配置建議的 64 GB 或更多記憶體。

1. 使用您 Hypervisor 中的檢查點或快照集功能，以便將虛擬機器復原至乾淨的狀態。


## <a name="instructions-to-deploy-sql-server-big-data-cluster"></a>部署 SQL Server 巨量資料叢集簡介

1. 在您打算用於部署的 VM 上下載指令碼。

   ```bash
   curl --output setup-bdc.sh https://raw.githubusercontent.com/microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/deployment/kubeadm/ubuntu-single-node-vm/setup-bdc.sh
   ```

2. 使用下列命令，讓指令碼成為可執行檔。

   ```bash
   chmod +x setup-bdc.sh
   ```

3. 執行指令碼 (確定您是以 *sudo* 執行)

   ```bash
   sudo ./setup-bdc.sh
   ```

   出現提示時，請提供您密碼的輸入以用於下列外部端點：控制器、SQL Server 主機和閘道。 根據 SQL Server 密碼的現有規則，密碼應該有足夠的複雜度。 控制器使用者名稱預設為 *admin*。

4. 設定 **azdata** 工具的別名。

   ```bash
   source ~/.bashrc
   ```

5. 重新整理 azdata 的別名設定。

   ```bash
   azdata --version
   ```

## <a name="cleanup"></a>清理

提供 [cleanup-bdc.sh](https://raw.githubusercontent.com/microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/deployment/kubeadm/ubuntu-single-node-vm/cleanup-bdc.sh) 指令碼是作為一種重設環境 (如有必要) 的便利措施。 不過，建議您使用虛擬機器來進行測試，並使用您 Hypervisor 中的快照集功能將虛擬機器復原至乾淨的狀態。

## <a name="next-steps"></a>後續步驟

若要開始使用巨量資料叢集，請參閱[教學課程：將範例資料載入 SQL Server 巨量資料叢集](tutorial-load-sample-data.md)。
