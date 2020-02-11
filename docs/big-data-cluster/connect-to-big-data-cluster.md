---
title: 連線到主要執行個體和 HDFS 巨量資料叢集
description: 了解如何連線到 SQL Server 巨量資料叢集中的 SQL Server 主要執行個體和 HDFS/Spark 閘道。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 0c5ba08a492be621e4b1f8871bdfcb49983af26d
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "73882397"
---
# <a name="connect-to-a-sql-server-big-data-cluster-with-azure-data-studio"></a>使用 Azure Data Studio 連線到 SQL Server 巨量資料叢集

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文描述如何從 Azure Data Studio 連線到 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]。

## <a name="prerequisites"></a>Prerequisites

- 已部署的 [SQL Server 2019 巨量資料叢集](deployment-guidance.md)。
- [SQL Server 2019 巨量資料工具](deploy-big-data-tools.md)：
   - **Azure Data Studio**
   - **SQL Server 2019 延伸模組**
   - **kubectl**
   - **azdata**

## <a id="master"></a> 連線到叢集

若要使用 Azure Data Studio 連線到巨量資料叢集，請建立與叢集中 SQL Server 主要執行個體的新連線。 方法如下。

1. 尋找 SQL Server 主要執行個體端點：

   ```
   azdata bdc endpoint list -e sql-server-master
   ```

   > [!TIP]
   > 如需如何取得端點的詳細資訊，請參閱[擷取端點](deployment-guidance.md#endpoints)。

1. 在 Azure Data Studio 中，按 **F1** 鍵 > [新增連線]  。

1. 在 [連線類型]  中，選取 [Microsoft SQL Server]  。

1. 在 [伺服器名稱]  文字方塊中，鍵入您在 SQL Server 主要執行個體找到的端點名稱 (例如： **\<IP_Address\>,31433**)。 

1. 選擇您的驗證類型。 針對在大型資料叢集中執行的 SQL Server 主要執行個體，僅支援 **Windows 驗證** 和 **SQL 登入**。 

1. 如果使用 SQL 登入，請輸入您的 SQL 登入**使用者名稱**和**密碼**。

   > [!TIP]
   > 根據預設，在巨量資料叢集部署期間，將會停用 **SA** 使用者名稱。 部署期間會佈建一個新的系統管理員使用者，其名稱與密碼會與 **AZDATA_USERNAME**和 **AZDATA_PASSWORD** 環境變數相對應，並且會在部署之前或部署期間設定。

1. 將目標**資料庫名稱**變更為您的關聯式資料庫之一。

   ![連線到主要執行個體](./media/connect-to-big-data-cluster/connect-to-cluster.png)

1. 按下 [連線]  ，**伺服器儀表板**應該會隨即出現。

在 2019 年 2 月版的 Azure Data Studio 中，連線到 SQL Server 主要執行個體也可讓您與 HDFS/Spark 閘道互動。 這表示您不需要對 HDFS 和 Spark 使用個別連線 (如下一節所述)。

- 物件總管現在包含新的 [資料服務]  節點，按一下滑鼠右鍵可取得巨量資料叢集工作的支援，例如建立新的筆記本或提交 Spark 作業。 
- **資料服務** 節點也包含 **HDFS** 資料夾，可讓您探索 HDFS 的內容及執行牽涉到 HDFS 的一般工作，例如，建立外部資料表或開啟筆記本來分析 HDFS 內容。
- 安裝延伸模組之後，連線的**伺服器儀表板**也會包含 [SQL Server 巨量資料叢集]  和 [SQL Server 2019]  索引標籤。

   ![Azure Data Studio 資料服務節點](./media/connect-to-big-data-cluster/connect-data-services-node.png)

## <a name="next-steps"></a>後續步驟

如需 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] 的詳細資訊，請參閱[什麼是 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]](big-data-cluster-overview.md)。
