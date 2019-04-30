---
title: 將 Spark 連線到 SQL Server
titleSuffix: SQL Server big data clusters
description: 了解如何在 Spark 中使用 MSSQL Spark 連接器，來讀取和寫入至 SQL Server。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 04/23/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 54361f9a061169d51f11ccb130e78ba67c0a9a67
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/24/2019
ms.locfileid: "63759215"
---
# <a name="how-to-read-and-write-to-sql-server-from-spark-using-the-mssql-spark-connector"></a>如何讀取和寫入至 SQL Server 使用 MSSQL Spark 連接器從 Spark

索引鍵的巨量資料使用模式是在 Spark 中，後面接著將資料寫入至 SQL Server 中，以存取特定業務應用程式的大量資料處理。 這些使用模式受益於使用重要的 SQL 最佳化，並提供有效率的寫入機制的連接器。

CTP2.5 巨量資料叢集以提供新的 MSSQL Spark 連接器，並使用大量 Api 撰寫高效能 Spark SQL 寫入 SQL Server。 這篇文章提供如何讀取和寫入至 SQL Server 從 Spark 使用 MSSQL Spark 連接器的範例。 在此範例中，會從 HDFS 的巨量資料叢集，Spark 處理，以及接著會寫入至 SQL Server 主要執行個體在叢集中使用新 MSSQL Spark 連接器中讀取資料。

## <a name="mssql-spark-connector-interface"></a>MSSQL Spark 連接器介面

MSSQL Spark 連接器將 Spark 資料來源 Api 為基礎，並提供熟悉的 Spark JDBC 連接器介面。 如介面參數，請參閱[Apache Spark 文件](http://spark.apache.org/docs/latest/sql-data-sources-jdbc.html)。 依名稱參考 MSSQL Spark 連接器**com.microsoft.sqlserver.jdbc.spark**。

下表描述已變更或不熟悉的介面參數：

| 屬性名稱 | 選擇性 | 描述 |
|---|---|---|
| **isolationLevel** | 是 | 這會說明連接的隔離等級。 預設值為 MSSQLSpark 連接器**READ_COMMITTED** |

連接器會使用 SQL Server 大量寫入的 Api。 參數可以由使用者傳遞做為選擇性參數，以及傳遞做為任何大量寫入-為基礎的 API 連接器。 如需有關大量寫入作業，請參閱 < [SQLServerBulkCopyOptions]( ../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md#sqlserverbulkcopyoptions)。

## <a name="prerequisites"></a>先決條件

- A[巨量資料的 SQL Server 叢集](deploy-get-started.md)。

- [Azure Data Studio](../azure-data-studio/download.md)。

## <a name="create-the-target-database"></a>建立目標資料庫

1. 開啟 Azure Data Studio，並[連接到您的巨量資料叢集的 SQL Server 主要執行個體](connect-to-big-data-cluster.md)。

1. 建立新的查詢，並執行下列命令來建立名為的範例資料庫**MyTestDatabase**。

   ```sql
   Create DATABASE MyTestDatabase
   GO
   ```

## <a name="load-sample-data-into-hdfs"></a>將範例資料載入 HDFS

1. 下載[AdultCensusIncome.csv](https://amldockerdatasets.azureedge.net/AdultCensusIncome.csv)到本機電腦。

1. 在 Azure 資料 Studio 中，您的巨量資料叢集的 HDFS 資料夾上按一下滑鼠右鍵，然後選取**新的目錄**。 目錄命名為**spark_data**。

1. 以滑鼠右鍵按一下**spark_data**目錄，然後選取**將檔案上傳**。 上傳**AdultCensusIncome.csv**檔案。

   ![AdultCensusIncome CSV 檔案](./media/spark-mssql-connector/spark_data.png)

## <a name="run-the-sample-notebook"></a>執行範例 notebook

為了示範使用 MSSQL Spark 連接器，使用這項資料，您可以下載 notebook 範例，在 Azure Data Studio，開啟並執行每個程式碼區塊。 如需有關使用 notebook 的詳細資訊，請參閱[如何在 SQL Server 2019 預覽中使用 notebook](notebooks-guidance.md)。

1. 從 PowerShell 或 bash 命令列中，執行下列命令來下載**mssql_spark_connector.ipynb** notebook 範例：

   ```PowerShell
   curl -o mssql_spark_connector.ipynb "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/spark/spark_to_sql/mssql_spark_connector.ipynb"
   ```

1. 在 Azure 資料 Studio 中開啟範例筆記本檔案。 請確認它連線到您的巨量資料叢集的 HDFS/Spark 閘道。

1. 若要查看 MSSQL Spark 連接器的使用方式範例中執行每個程式碼儲存格。

## <a name="next-steps"></a>後續步驟

如需有關巨量資料叢集的詳細資訊，請參閱[如何部署 SQL Server 的巨量資料叢集的 Kubernetes 上](deployment-guidance.md)