---
title: 連接到 master 和 HDFS
titleSuffix: SQL Server big data clusters
description: 了解如何連接到 SQL Server 的主要執行個體和 SQL Server 2019 巨量資料叢集 （預覽） 的 HDFS/Spark 閘道。
author: rothja
ms.author: jroth
manager: jroth
ms.date: 05/22/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 245e88034194a01908b69d545deb9fa717c19a4a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66782977"
---
# <a name="connect-to-a-sql-server-big-data-cluster-with-azure-data-studio"></a>連線到 SQL Server 的巨量資料叢集使用 Azure Data Studio

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文說明如何從 Azure Data Studio 連接到 SQL Server 2019 巨量資料叢集 （預覽）。

## <a name="prerequisites"></a>先決條件

- 已部署[SQL Server 2019 巨量資料叢集](deployment-guidance.md)。
- [SQL Server 2019 巨量資料工具](deploy-big-data-tools.md):
   - **Azure Data Studio**
   - **SQL Server 2019 延伸模組**
   - **kubectl**

## <a id="master"></a> 連線到叢集

若要連線至巨量資料叢集使用 Azure Data Studio，請在叢集中的 SQL Server 的主要執行個體的新連接。 下列步驟說明如何使用 Azure Data Studio 的主要執行個體的連接。

1. 從命令列中，找出 IP 主要執行個體使用下列命令：

   ```
   kubectl get svc master-svc-external -n <your-big-data-cluster-name>
   ```

   > [!TIP]
   > 巨量資料叢集名稱預設為**mssql 叢集**除非您自訂部署設定檔中的名稱。 如需詳細資訊，請參閱 <<c0> [ 巨量資料叢集的部署設定](deployment-custom-configuration.md#clustername)。

1. 在 Azure Data Studio，按下**F1** > **新連線**。

1. 在 **連線類型**，選取**Microsoft SQL Server**。

1. 輸入中的 SQL Server 主要執行個體的 IP 位址**伺服器名稱**(例如： **\<IP 位址\>31433、** )。

1. 輸入 SQL 登入**使用者名**並**密碼**。

   > [!TIP]
   > 根據預設，使用者名稱是**SA**和密碼變更，除非對應至**MSSQL_SA_PASSWORD**在部署期間使用的環境變數。

1. 變更目標**資料庫名稱**其中一項關聯式資料庫。

   ![連接到主要執行個體](./media/connect-to-big-data-cluster/connect-to-cluster.png)

1. 按下**Connect**，而**Server 儀表板**應該會出現。

Azure Data Studio 2019 年 2 月版本中，連接到 SQL Server 的主要執行個體也可讓您與 HDFS/Spark 閘道互動。 這表示您不需要針對 HDFS 和下一節說明的 Spark 使用個別的連線。

- [物件總管] 現在包含新**Data Services**節點，以滑鼠右鍵按一下支援巨量資料叢集工作，例如建立新的 notebook 或提交 spark 作業。 
- **Data Services**  節點也包含**HDFS** HDFS 探勘和 Notebook 中執行動作，例如 Create External Table 或分析的資料夾。
- **Server 儀表板**連線也會包含索引標籤**巨量資料的 SQL Server 叢集**並**SQL Server 2019 （預覽）** 安裝擴充功能時。

   ![Azure Data Studio 資料服務 節點](./media/connect-to-big-data-cluster/connect-data-services-node.png)

## <a name="next-steps"></a>後續步驟

如需有關 SQL Server 2019 巨量資料叢集的詳細資訊，請參閱 <<c0> [ 什麼是 SQL Server 2019 巨量資料叢集](big-data-cluster-overview.md)。