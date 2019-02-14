---
title: 連接到 master 和 HDFS
titleSuffix: SQL Server 2019 big data clusters
description: 了解如何連接到 SQL Server 的主要執行個體和 SQL Server 2019 巨量資料叢集 （預覽） 的 HDFS/Spark 閘道。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/12/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 103e02d456f1176c3bb49c1e67f84215399ab5cd
ms.sourcegitcommit: 009bee6f66142c48477849ee03d5177bcc3b6380
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/13/2019
ms.locfileid: "56231035"
---
# <a name="connect-to-a-sql-server-big-data-cluster-with-azure-data-studio"></a>連線到 SQL Server 的巨量資料叢集使用 Azure Data Studio

本文說明如何從 Azure Data Studio 連接到 SQL Server 2019 巨量資料叢集 （預覽）。 有兩個用來與巨量資料叢集互動的主要端點：

| 端點 | 描述 |
|---|---|
| SQL Server Master 執行個體 | SQL Server 主要執行個體在叢集中包含 SQL Server 的關聯式資料庫。 |
| HDFS/Spark 閘道 | 存取叢集和執行 Spark 作業的能力中的 HDFS 儲存體。 |

> [!TIP]
> Azure Data Studio 2019 年 2 月版本中，會自動連接到 SQL Server 的主要執行個體提供 UI 存取 HDFS/Spark 閘道。

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
   kubectl get svc endpoint-master-pool -n <your-cluster-name>
   ```

1. 在 Azure Data Studio，按下**F1** > **新連線**。

1. 在 **連線類型**，選取**Microsoft SQL Server**。

1. 輸入中的 SQL Server 主要執行個體的 IP 位址**伺服器名稱**(例如：**\<IP 位址\>31433、**)。

1. 輸入 SQL 登入**使用者名**並**密碼**。

   > [!TIP]
   > 根據預設，使用者名稱是**SA**和密碼變更，除非對應至**MSSQL_SA_PASSWORD**在部署期間使用的環境變數。

1. 變更目標**資料庫名稱**其中一項關聯式資料庫。

   ![連接到主要執行個體](./media/connect-to-big-data-cluster/connect-to-cluster.png)

1. 按下**Connect**，而**Server 儀表板**應該會出現。

Azure Data Studio 2019 年 2 月版本中，連接到 SQL Server 的主要執行個體也可讓您與 HDFS/Spark 閘道互動。 這表示您不需要針對 HDFS 和下一節說明的 Spark 使用個別的連線。

- [物件總管] 現在包含新**Data Services**節點，以滑鼠右鍵按一下支援巨量資料叢集工作，例如建立新的 notebook 或提交 spark 作業。 
- **Data Services**  節點也包含**HDFS** HDFS 探勘和 Notebook 中執行動作，例如 Create External Table 或分析的資料夾。
- **Server 儀表板**連線也會包含索引標籤**SQL Server 巨量資料叢集**並**SQL Server 2019 （預覽）** 安裝擴充功能時。

   ![Azure Data Studio 資料服務 節點](./media/connect-to-big-data-cluster/connect-data-services-node.png)

> [!IMPORTANT]
> 如果您看到**未知的錯誤**在 UI 中，您可能要[直接連接到 HDFS/Spark 閘道](#hdfs)。 此錯誤的其中一個原因是 SQL Server 的主要執行個體與 HDFS/Spark 閘道不同的密碼。 Azure Data Studio 假設相同的密碼使用於兩者。
  
## <a id="hdfs"></a> 連線到 HDFS/Spark 閘道

在大部分情況下，連接到 SQL Server 的主要執行個體可讓您存取的 HDFS 和 Spark 也透過**Data Services**節點。 不過，您仍然可以建立的專用的連接**HDFS/Spark 閘道**如有需要。 下列步驟說明如何使用 Azure Data Studio 來連線。

1. 從命令列中，尋找您的 HDFS/Spark 閘道與其中一個下列的命令的 IP 位址。
   
   **AKS 部署：**

   ```
   kubectl get svc service-security-lb -n <your-cluster-name>
   ```

   **不 AKS 部署**:

   ```
   kubectl get svc service-security-nodeport -n <your-cluster-name>
   ```
 
1. 在 Azure Data Studio，按下**F1** > **新連線**。

1. 在 **連線類型**，選取**巨量資料的 SQL Server 叢集**。

   > [!TIP]
   > 如果您看不見**巨量資料的 SQL Server 叢集**連線類型，請確定您已安裝[SQL Server 2019 延伸模組](../azure-data-studio/sql-server-2019-extension.md)和您在完成的延伸模組後重新啟動 Azure Data Studio正在安裝。

1. 輸入中的巨量資料叢集的 IP 位址**伺服器名稱**（不指定連接埠）。

1. 請輸入`root`for**使用者**並指定**密碼**到您的巨量資料叢集。

   ![連線到 HDFS/Spark 閘道](./media/connect-to-big-data-cluster/connect-to-cluster-hdfs-spark.png)

   > [!TIP]
   > 根據預設，使用者名稱是**根**和密碼對應至**KNOX_PASSWORD**在部署期間使用的環境變數。

1. 按下**Connect**，而**Server 儀表板**應該會出現。

## <a name="next-steps"></a>後續步驟

如需有關 SQL Server 2019 巨量資料叢集的詳細資訊，請參閱 <<c0> [ 什麼是 SQL Server 2019 巨量資料叢集](big-data-cluster-overview.md)。