---
title: 載入範例資料
titleSuffix: SQL Server big data clusters
description: 本教學課程示範如何將範例資料載入 SQL Server 巨量資料叢集中。 範例資料包含 SQL Server 主要執行個體中的關聯式資料。 此範例資料也包含儲存集區中的 HDFS 資料。 此資料也支援本節中的其他教學課程。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 52285164928e1a4811abc17e931a1af1921c6d07
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "76831415"
---
# <a name="tutorial-load-sample-data-into-a-sql-server-big-data-cluster"></a>教學課程：將範例資料載入 SQL Server 巨量資料叢集

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本教學課程說明如何使用指令碼將範例資料載入至 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]。 文件中的許多其他教學課程都使用此範例資料。

> [!TIP]
> 您可以在 [sql-server-samples](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster) GitHub 存放庫中找到 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]的其他範例。 這些範例位於 **sql-server-samples/samples/features/sql-big-data-cluster/** 路徑中。

## <a name="prerequisites"></a>Prerequisites

- [已部署的巨量資料叢集](deployment-guidance.md)
- [巨量資料工具](deploy-big-data-tools.md)
   - **azdata**
   - **kubectl**
   - **sqlcmd**
   - **curl**
 
## <a name="load-sample-data"></a><a id="sampledata"></a> 載入範例資料

下列步驟會使用啟動程序指令碼來下載 SQL Server 資料庫備份，並將資料載入您的巨量資料叢集中。 為了方便，這些步驟已細分為 [Windows](#windows) 和 [Linux](#linux) 章節。 如果您想要使用基本使用者名稱/密碼作為驗證機制，請在執行指令碼之前，先設定 AZDATA_USERNAME 與 AZDATA_PASSWORD 環境變數。 否則，指令碼將使用整合式驗證來連線到 SQL Server 主要執行個體與 Knox 閘道。 此外，也應該為端點指定 DNS 名稱以使用整合式驗證。

## <a name="windows"></a><a id="windows"></a> Windows

下列步驟描述如何使用 Windows 用戶端將範例資料載入您的巨量資料叢集。

1. 開啟新的 Windows 命令提示字元。

   > [!IMPORTANT]
   > 請勿使用 Windows PowerShell 執行這些步驟。 指令碼在 PowerShell 中會失敗，因為其會使用 **curl** 的 PowerShell 版本。

1. 使用 **url** 下載範例資料的啟動程序指令碼。

   ```cmd
   curl -o bootstrap-sample-db.cmd "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.cmd"
   ```

1. 下載 **bootstrap-sample-db.sql** Transact-SQL 指令碼。 此指令碼是由啟動程序指令碼所呼叫。

   ```cmd
   curl -o bootstrap-sample-db.sql "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.sql"
   ```

1. 啟動程序指令碼需要巨量資料叢集的下列位置參數：

   | 參數 | 描述 |
   |---|---|
   | <CLUSTER_NAMESPACE> | 您為巨量資料叢集提供的名稱。 |
   | <SQL_MASTER_ENDPOINT> | 主要執行個體的 DNS 名稱或 IP 位址。 |
   | <KNOX_ENDPOINT> | HDFS/Spark 閘道的 DNS 名稱或 IP 位址。 |
   
   > [!TIP]
   > 使用 [kubectl](cluster-troubleshooting-commands.md) 來尋找 SQL Server 主要執行個體和 Knox 的 IP 位址。 執行 `kubectl get svc -n <your-big-data-cluster-name>` 並查看主要執行個體 (**master-svc-external**) 和 Knox (**gateway-svc-external**) 的外部 IP 位址。 叢集的預設名稱是 **mssql-cluster**。

1. 執行啟動程序指令碼。

   ```cmd
   .\bootstrap-sample-db.cmd <CLUSTER_NAMESPACE> <SQL_MASTER_ENDPOINT> <KNOX_ENDPOINT>
   ```

## <a name="linux"></a><a id="linux"></a> Linux

下列步驟描述如何使用 Linux 用戶端將範例資料載入您的巨量資料叢集。

1. 下載啟動程序指令碼，並為其指派可執行檔的權限。

   ```bash
   curl -o bootstrap-sample-db.sh "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.sh"
   chmod +x bootstrap-sample-db.sh
   ```

1. 下載 **bootstrap-sample-db.sql** Transact-SQL 指令碼。 此指令碼是由啟動程序指令碼所呼叫。

   ```bash
   curl -o bootstrap-sample-db.sql "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.sql"
   ```

1. 啟動程序指令碼需要巨量資料叢集的下列位置參數：

   | 參數 | 描述 |
   |---|---|
   | <CLUSTER_NAMESPACE> | 您為巨量資料叢集提供的名稱。 |
   | <SQL_MASTER_ENDPOINT> | 主要執行個體的 DNS 名稱或 IP 位址。 |
   | <KNOX_ENDPOINT> | HDFS/Spark 閘道的 DNS 名稱或 IP 位址。 |

   > [!TIP]
   > 使用 [kubectl](cluster-troubleshooting-commands.md) 來尋找 SQL Server 主要執行個體和 Knox 的 IP 位址。 執行 `kubectl get svc -n <your-big-data-cluster-name>` 並查看主要執行個體 (**master-svc-external**) 和 Knox (**gateway-svc-external**) 的外部 IP 位址。 叢集的預設名稱是 **mssql-cluster**。

1. 執行啟動程序指令碼。

   ```bash
   ./bootstrap-sample-db.sh <CLUSTER_NAMESPACE> <SQL_MASTER_ENDPOINT> <KNOX_ENDPOINT>
   ```

## <a name="next-steps"></a>後續步驟

執行啟動程序指令碼之後，您的巨量資料叢集會具有範例資料庫和 HDFS 資料。 下列教學課程使用範例資料來示範巨量資料叢集功能：

資料虛擬化：

- [教學課程：查詢 SQL Server 巨量資料叢集中的 HDFS](tutorial-query-hdfs-storage-pool.md)
- [教學課程：查詢 SQL Server 巨量資料叢集中的 Oracle](tutorial-query-oracle.md)

資料擷取：

- [教學課程：使用 Transact-SQL 將資料內嵌至 SQL Server 資料集區](tutorial-data-pool-ingest-sql.md)
- [教學課程：使用 Spark 作業將資料內嵌至 SQL Server 資料集區](tutorial-data-pool-ingest-spark.md)

Notebooks：

- [教學課程：在 SQL Server 2019 巨量資料叢集上執行範例筆記本](tutorial-notebook-spark.md)
