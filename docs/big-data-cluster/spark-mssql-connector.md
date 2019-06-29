---
title: 將 Spark 連線到 SQL Server
titleSuffix: SQL Server big data clusters
description: 了解如何在 Spark 中使用 MSSQL Spark 連接器，來讀取和寫入至 SQL Server。
author: rothja
ms.author: jroth
manager: jroth
ms.date: 06/26/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 878e08426fc58d6ad5a921eff4ac33dca18aa03c
ms.sourcegitcommit: f7ad034f748ebc3e5691a5e4c3eb7490e5cf3ccf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/29/2019
ms.locfileid: "67469115"
---
# <a name="how-to-read-and-write-to-sql-server-from-spark-using-the-mssql-spark-connector"></a>如何讀取和寫入至 SQL Server 使用 MSSQL Spark 連接器從 Spark

索引鍵的巨量資料使用模式是在 Spark 中，後面接著將資料寫入至 SQL Server 中，以存取特定業務應用程式的大量資料處理。 這些使用模式受益於使用重要的 SQL 最佳化，並提供有效率的寫入機制的連接器。

這篇文章提供如何使用 MSSQL Spark 連接器來讀取和寫入下列位置中的巨量資料叢集的範例：

1. SQL Server 的主要執行個體
1. SQL Server 資料集區

   ![MSSQL Spark 連接器圖表](./media/spark-mssql-connector/mssql-spark-connector-diagram.png)

此範例會執行下列工作：

- 從 HDFS 讀取檔案，並進行一些基本的處理。
- 寫入 SQL Server 主要執行個體為 SQL 資料表的資料框架，然後讀取資料表的資料框架。
- 寫入當做 SQL 外部資料表的 SQL Server 資料集區中的資料框架，然後讀取 外部資料表的資料框架。

## <a name="mssql-spark-connector-interface"></a>MSSQL Spark 連接器介面

SQL Server 2019 preview 可提供**MSSQL Spark 連接器**適用於巨量資料叢集所使用 SQL Server 大量寫入 Api 適用於 Spark SQL 寫入。 MSSQL Spark 連接器將 Spark 資料來源 Api 為基礎，並提供熟悉的 Spark JDBC 連接器介面。 如介面參數，請參閱[Apache Spark 文件](http://spark.apache.org/docs/latest/sql-data-sources-jdbc.html)。 依名稱參考 MSSQL Spark 連接器**com.microsoft.sqlserver.jdbc.spark**。

下表描述已變更或不熟悉的介面參數：

| 屬性名稱 | 選擇性 | 描述 |
|---|---|---|
| **isolationLevel** | 是 | 這會說明連接的隔離等級。 預設值為 MSSQLSpark 連接器**READ_COMMITTED** |

連接器會使用 SQL Server 大量寫入的 Api。 參數可以由使用者傳遞做為選擇性參數，以及傳遞做為任何大量寫入-為基礎的 API 連接器。 如需有關大量寫入作業，請參閱 < [SQLServerBulkCopyOptions]( ../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md#sqlserverbulkcopyoptions)。

## <a name="prerequisites"></a>先決條件

- A[巨量資料的 SQL Server 叢集](deploy-get-started.md)。

- [Azure Data Studio](https://aka.ms/azdata-insiders)。

## <a name="create-the-target-database"></a>建立目標資料庫

1. 開啟 Azure Data Studio，並[連接到您的巨量資料叢集的 SQL Server 主要執行個體](connect-to-big-data-cluster.md)。

1. 建立新的查詢，並執行下列命令來建立名為的範例資料庫**MyTestDatabase**。

   ```sql
   Create DATABASE MyTestDatabase
   GO
   ```

## <a name="load-sample-data-into-hdfs"></a>將範例資料載入 HDFS

1. 下載[AdultCensusIncome.csv](https://amldockerdatasets.azureedge.net/AdultCensusIncome.csv)到本機電腦。

1. 啟動 Azure Data Studio，並[連線到您的巨量資料叢集](connect-to-big-data-cluster.md)。

1. 在您的巨量資料叢集的 HDFS 資料夾上按一下滑鼠右鍵，然後選取**新的目錄**。 目錄命名為**spark_data**。

1. 以滑鼠右鍵按一下**spark_data**目錄，然後選取**將檔案上傳**。 上傳**AdultCensusIncome.csv**檔案。

   ![AdultCensusIncome CSV 檔案](./media/spark-mssql-connector/spark_data.png)

## <a name="run-the-sample-notebook"></a>執行範例 notebook

為了示範使用 MSSQL Spark 連接器，使用這項資料，您可以下載 notebook 範例，在 Azure Data Studio，開啟並執行每個程式碼區塊。 如需有關使用 notebook 的詳細資訊，請參閱[如何在 SQL Server 2019 預覽中使用 notebook](notebooks-guidance.md)。

1. 從 PowerShell 或 bash 命令列中，執行下列命令來下載**mssql_spark_connector.ipynb** notebook 範例：

   ```PowerShell
   curl -o mssql_spark_connector.ipynb "https://raw.githubusercontent.com/microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/spark/data-virtualization/mssql_spark_connector.ipynb"
   ```

1. 在 Azure 資料 Studio 中開啟範例筆記本檔案。 請確認它連線到您的巨量資料叢集的 HDFS/Spark 閘道。

1. 若要查看 MSSQL Spark 連接器的使用方式範例中執行每個程式碼儲存格。

## <a name="next-steps"></a>後續步驟

如需有關巨量資料叢集的詳細資訊，請參閱[如何部署 SQL Server 的巨量資料叢集的 Kubernetes 上](deployment-guidance.md)