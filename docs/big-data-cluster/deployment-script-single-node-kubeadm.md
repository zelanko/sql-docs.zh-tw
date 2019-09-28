---
title: 使用 Bash 指令碼部署至單一節點 kubeadm 叢集
titleSuffix: SQL Server big data clusters
description: 使用 bash 部署腳本，將 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] 部署至單一節點 kubeadm 叢集。
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 2379f96e3b5288fc33f5c925613bf9fd5d35612d
ms.sourcegitcommit: c4875c097e3aae1b76233777d15e0a0ec8e0d681
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/27/2019
ms.locfileid: "71341845"
---
# <a name="deploy-with-a-bash-script-to-a-single-node-kubeadm-cluster"></a>使用 Bash 指令碼部署至單一節點 kubeadm 叢集

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

在本教學課程中，您會使用範例 Bash 部署指令碼，利用 kubeadm 和 SQL Server 巨量資料叢集來部署單一節點 Kubernetes 叢集。  

## <a name="prerequisites"></a>必要條件

- Vanilla Ubuntu 18.04 或 16.04**伺服器**虛擬或實體機器。 所有相依性都由指令碼設定，您可以從 VM 內執行指令碼。

  > [!NOTE]
  > 尚不支援使用 Azure Linux Vm。

- VM 至少應有8個 Cpu、64 GB 的 RAM，以及 100 GB 的磁碟空間。 在提取所有巨量資料叢集 Docker 映像之後，您將會剩下用於所有元件的 50 GB 資料和記錄檔。

- 使用下列命令來更新現有的封裝，以確保 OS 映射是最新的。

   ``` bash
   sudo apt update && sudo apt upgrade -y
   sudo systemctl reboot
   ```

## <a name="recommended-virtual-machine-settings"></a>建議的虛擬機器設定

1. 使用虛擬機器的靜態記憶體設定。 例如，在 Hyper-v 安裝中，不會使用動態記憶體配置，而是要配置建議的 64 GB 或更高版本。

1. 在您的超面板中使用檢查點或快照集功能，讓您可以將虛擬機器復原到「清除」狀態。


## <a name="instructions-to-deploy-sql-server-big-data-cluster"></a>部署 SQL Server big data cluster 的指示

1. 在您打算用於部署的 VM 上下載指令碼。

   ```bash
   curl --output setup-bdc.sh https://raw.githubusercontent.com/microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/deployment/kubeadm/ubuntu-single-node-vm/setup-bdc.sh
   ```

2. 使用下列命令，讓指令碼成為可執行檔。

   ```bash
   chmod +x setup-bdc.sh
   ```

3. 執行腳本（請確定您正在使用*sudo*）

   ```bash
   sudo ./setup-bdc.sh
   ```

   出現提示時，請提供您密碼的輸入以用於下列外部端點：控制器、SQL Server 主機和閘道。 根據 SQL Server 密碼的現有規則，密碼應該夠複雜。 控制器使用者名稱預設為 *admin*。

4. 設定 **azdata** 工具的別名。

   ```bash
   source ~/.bashrc
   ```

5. 重新整理 azdata 的別名設定。

   ```bash
   azdata --version
   ```

## <a name="cleanup"></a>清理

視需要提供[cleanup-bdc.sh](https://raw.githubusercontent.com/microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/deployment/kubeadm/ubuntu-single-node-vm/cleanup-bdc.sh)腳本來重設環境。 不過，我們建議您使用虛擬機器進行測試，並在您的管理程式中使用快照集功能，將虛擬機器回復為「清除」狀態。

## <a name="next-steps"></a>後續步驟

若要開始使用 big data 叢集，請參閱 @no__t 0Tutorial：將範例資料載入 SQL Server big data cluster @ no__t-0。
