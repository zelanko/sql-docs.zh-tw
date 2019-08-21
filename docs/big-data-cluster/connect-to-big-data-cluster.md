---
title: 連接到 master 和 HDFS Big data 叢集
description: 瞭解如何連接到的 SQL Server 主要實例和 HDFS/Spark 閘道[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: fb6e1f684a277740c06fbd0a2fdc23dbd77f8e5c
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/20/2019
ms.locfileid: "69652426"
---
# <a name="connect-to-a-sql-server-big-data-cluster-with-azure-data-studio"></a>使用 Azure Data Studio 連線到 SQL Server 巨量資料叢集

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文說明如何[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]從 Azure Data Studio 連接到。

## <a name="prerequisites"></a>必要條件

- 已部署的 [SQL Server 2019 巨量資料叢集](deployment-guidance.md)。
- [SQL Server 2019 巨量資料工具](deploy-big-data-tools.md)：
   - **Azure Data Studio**
   - **SQL Server 2019 延伸模組**
   - **kubectl**

## <a id="master"></a> 連線到叢集

若要使用 Azure Data Studio 連線到巨量資料叢集，請建立與叢集中 SQL Server 主要執行個體的新連線。 下列步驟描述如何使用 Azure Data Studio 連線到主要執行個體。

1. 從命令列，使用下列命令尋找主要執行個體的 IP：

   ```
   kubectl get svc master-svc-external -n <your-big-data-cluster-name>
   ```

   > [!TIP]
   > 巨量資料叢集名稱預設為 **mssql-cluster** (除非您在部署組態檔中自訂名稱)。 如需詳細資訊，請參閱[針對巨量資料叢集設定部署設定](deployment-custom-configuration.md#clustername)。

1. 在 Azure Data Studio 中，按 **F1** 鍵 > [新增連線]。

1. 在 [連線類型] 中，選取 [Microsoft SQL Server]。

1. 在 [伺服器名稱] 中鍵入 SQL Server 主要執行個體的 IP 位址 (例如： **\<IP Address\>,31433**)。

1. 輸入 SQL 登入**使用者名稱**和**密碼**。

   > [!TIP]
   > 根據預設，使用者名稱為 **SA**，而且除非變更，否則密碼會對應到部署期間所使用的 **MSSQL_SA_PASSWORD** 環境變數。

1. 將目標**資料庫名稱**變更為您的關聯式資料庫之一。

   ![連線到主要執行個體](./media/connect-to-big-data-cluster/connect-to-cluster.png)

1. 按下 [連線]，**伺服器儀表板**應該會隨即出現。

在 2019 年 2 月版的 Azure Data Studio 中，連線到 SQL Server 主要執行個體也可讓您與 HDFS/Spark 閘道互動。 這表示您不需要對 HDFS 和 Spark 使用個別連線 (如下一節所述)。

- 物件總管現在包含新的 [資料服務] 節點，按一下滑鼠右鍵可取得巨量資料叢集工作的支援，例如建立新的筆記本或提交 Spark 作業。 
- [資料服務] 節點也會包含 **HDFS** 資料夾，以供 HDFS 探索及執行「建立外部資料表」或「在筆記本中進行分析」等動作。
- 安裝延伸模組之後，連線的**伺服器儀表板**也會包含 [SQL Server 巨量資料叢集] 和 [SQL Server 2019 (Preview)] 索引標籤。

   ![Azure Data Studio 資料服務節點](./media/connect-to-big-data-cluster/connect-data-services-node.png)

## <a name="next-steps"></a>後續步驟

如需的詳細[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]資訊, 請參閱[什麼是[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] ](big-data-cluster-overview.md)。