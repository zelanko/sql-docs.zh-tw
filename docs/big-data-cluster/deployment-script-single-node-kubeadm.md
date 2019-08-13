---
title: 使用 Bash 指令碼部署至單一節點 kubeadm 叢集
titleSuffix: SQL Server big data clusters
description: 使用 Bash 部署指令碼，將 SQL Server 2019 巨量資料叢集 (預覽) 部署至單一節點 kubeadm 叢集。
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 37017221b636146a003f8af8890c655ed605bca9
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/25/2019
ms.locfileid: "68473070"
---
# <a name="deploy-with-a-bash-script-to-a-single-node-kubeadm-cluster"></a>使用 Bash 指令碼部署至單一節點 kubeadm 叢集

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

在本教學課程中，您會使用範例 Bash 部署指令碼，利用 kubeadm 和 SQL Server 巨量資料叢集來部署單一節點 Kubernetes 叢集。  

## <a name="prerequisites"></a>Prerequisites

- Vanilla Ubuntu 18.04 或 16.04 **伺服器** VM。 所有相依性都由指令碼設定，您可以從 VM 內執行指令碼。

  > [!NOTE]
  > 尚不支援使用 Azure VM。

- VM 至少應有 8 個 CPU、64 GB RAM 和 100 GB 的磁碟空間。 在提取所有巨量資料叢集 Docker 映像之後，您將會剩下用於所有元件的 50 GB 資料和記錄檔。

## <a name="instructions"></a>Instructions

1. 在您打算用於部署的 VM 上下載指令碼。

   ```bash
   curl --output setup-bdc.sh https://raw.githubusercontent.com/microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/deployment/kubeadm/ubuntu-single-node-vm/setup-bdc.sh
   ```

2. 使用下列命令，讓指令碼成為可執行檔。

   ```bash
   chmod +x setup-bdc.sh
   ```

3. 使用 **sudo** 執行指令碼。

   ```bash
   sudo ./setup-bdc.sh
   ```

   出現提示時，請提供您密碼的輸入以用於下列外部端點：控制器、SQL Server 主機和閘道。 控制器使用者名稱預設為 *admin*。

4. 設定 **azdata** 工具的別名。

   ```bash
   source ~/.bashrc
   ```

5. 驗證別名是否正常運作。

   ```bash
   azdata --version
   ```

## <a name="next-steps"></a>後續步驟

遵循[此教學課程](tutorial-load-sample-data.md)以開始使用巨量資料叢集。
