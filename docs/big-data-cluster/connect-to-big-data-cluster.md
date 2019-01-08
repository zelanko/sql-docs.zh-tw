---
title: 連接到 master 和 HDFS
titleSuffix: SQL Server 2019 big data clusters
description: 了解如何連接到 SQL Server 的主要執行個體和 SQL Server 2019 巨量資料叢集 （預覽） 的 HDFS/Spark 閘道。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 12/10/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 8bccadd8fbce9fe2a8cc6f16db75dbd09f3d1ed0
ms.sourcegitcommit: edf7372cb674179f03a330de5e674824a8b4118f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/11/2018
ms.locfileid: "53264360"
---
# <a name="connect-to-a-sql-server-big-data-cluster-with-azure-data-studio"></a>連線到 SQL Server 的巨量資料叢集使用 Azure Data Studio

本文說明如何從 Azure Data Studio 連接到 SQL Server 2019 巨量資料叢集 （預覽）。

## <a name="prerequisites"></a>先決條件

- 已部署[SQL Server 2019 巨量資料叢集](deployment-guidance.md)。
- [SQL Server 2019 巨量資料工具](deploy-big-data-tools.md):
   - **Azure Data Studio**
   - **SQL Server 2019 延伸模組**
   - **kubectl**

## <a name="connect-to-the-cluster"></a>連線到叢集

當您連線至巨量資料叢集時，您可以選擇連接到 SQL Server[主要執行個體](concept-master-instance.md)或 HDFS/Spark 閘道。 下列各節示範如何連接到每個。

## <a id="master"></a> 主要執行個體

SQL Server 的主要執行個體是傳統的 SQL Server 執行個體，包含 SQL Server 的關聯式資料庫。 下列步驟說明如何使用 Azure Data Studio 的主要執行個體的連接。

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

## <a id="hdfs"></a> HDFS/Spark 閘道

**HDFS/Spark 閘道**可讓您連接才能使用 HDFS 儲存體集區，並執行 Spark 作業。 下列步驟說明如何使用 Azure Data Studio 來連線。

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

1. 輸入中的巨量資料叢集的 IP 位址**伺服器名稱**（不指定連接埠）。

1. 請輸入`root`for**使用者**並指定**密碼**到您的巨量資料叢集。

   ![連線到 HDFS/Spark 閘道](./media/connect-to-big-data-cluster/connect-to-cluster-hdfs-spark.png)

   > [!TIP]
   > 根據預設，使用者名稱是**根**和密碼對應至**KNOX_PASSWORD**在部署期間使用的環境變數。

1. 按下**Connect**，而**Server 儀表板**應該會出現。

## <a name="next-steps"></a>後續步驟

如需有關 SQL Server 2019 巨量資料叢集的詳細資訊，請參閱 <<c0> [ 什麼是 SQL Server 2019 巨量資料叢集](big-data-cluster-overview.md)。