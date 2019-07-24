---
title: 載入範例資料
titleSuffix: SQL Server big data clusters
description: 本教學課程示範如何將範例資料載入 SQL Server big data 叢集中。 範例資料包含 SQL Server 主要實例中的關聯式資料。 它也會在存放集區中包含 HDFS 資料。 此資料支援本節中的其他教學課程。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 5b35eccece4df47cb483932386cf6a38e45d2dc8
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419283"
---
# <a name="tutorial-load-sample-data-into-a-sql-server-big-data-cluster"></a>教學課程：將範例資料載入 SQL Server big data 叢集中

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本教學課程說明如何使用腳本, 將範例資料載入 SQL Server 2019 big data cluster (預覽)。 檔中的許多其他教學課程都使用此範例資料。

> [!TIP]
> 您可以在[SQL Server 範例](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster)GitHub 存放庫中找到 SQL Server 2019 big data cluster (預覽) 的其他範例。 它們位於**sql server 範例/samples/features/sql-big--cluster/** path 中。

## <a name="prerequisites"></a>先決條件

- [已部署的 big data 叢集](deployment-guidance.md)
- [海量資料工具](deploy-big-data-tools.md)
   - **azdata**
   - **kubectl**
   - **sqlcmd**
   - **curl**

## <a id="sampledata"></a>載入範例資料

下列步驟會使用啟動程式腳本來下載 SQL Server 資料庫備份, 並將資料載入您的 big data 叢集中。 為了方便使用, 這些步驟已細分成[Windows](#windows)和[Linux](#linux)區段。

## <a id="windows"></a> Windows

下列步驟說明如何使用 Windows 用戶端, 將範例資料載入至您的 big data 叢集中。

1. 開啟新的 Windows 命令提示字元。

   > [!IMPORTANT]
   > 請勿使用 Windows PowerShell 執行這些步驟。 在 PowerShell 中, 腳本將會失敗, 因為它會使用已**捲曲**的 PowerShell 版本。

1. 使用**捲曲**來下載範例資料的啟動程式腳本。

   ```cmd
   curl -o bootstrap-sample-db.cmd "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.cmd"
   ```

1. 下載**bootstrap-sample-db sql** transact-sql 腳本。 此腳本是由啟動程式腳本所呼叫。

   ```cmd
   curl -o bootstrap-sample-db.sql "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.sql"
   ```

1. 啟動程式腳本需要您的 big data 叢集的下列位置參數:

   | 參數 | 描述 |
   |---|---|
   | <CLUSTER_NAMESPACE> | 您為 big data cluster 提供的名稱。 |
   | <SQL_MASTER_IP> | 主要實例的 IP 位址。 |
   | <SQL_MASTER_SA_PASSWORD> | 主要實例的 SA 密碼。 |
   | <KNOX_IP> | HDFS/Spark 閘道的 IP 位址。 |
   | <KNOX_PASSWORD> | HDFS/Spark 閘道的密碼。 |

   > [!TIP]
   > 使用[kubectl](cluster-troubleshooting-commands.md)來尋找 SQL Server 主要實例和 KNOX 的 IP 位址。 執行`kubectl get svc -n <your-big-data-cluster-name>`並查看主要實例 (**主要-svc-外部**) 和 Knox (**閘道-svc-外部**) 的外部 IP 位址。 叢集的預設名稱是**mssql-cluster**。

1. 執行啟動程式腳本。

   ```cmd
   .\bootstrap-sample-db.cmd <CLUSTER_NAMESPACE> <SQL_MASTER_IP> <SQL_MASTER_SA_PASSWORD> <KNOX_IP> <KNOX_PASSWORD>
   ```

## <a id="linux"></a> Linux

下列步驟說明如何使用 Linux 用戶端, 將範例資料載入至您的 big data 叢集中。

1. 下載啟動程式腳本, 並為其指派可執行檔許可權。

   ```bash
   curl -o bootstrap-sample-db.sh "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.sh"
   chmod +x bootstrap-sample-db.sh
   ```

1. 下載**bootstrap-sample-db sql** transact-sql 腳本。 此腳本是由啟動程式腳本所呼叫。

   ```bash
   curl -o bootstrap-sample-db.sql "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.sql"
   ```

1. 啟動程式腳本需要您的 big data 叢集的下列位置參數:

   | 參數 | 描述 |
   |---|---|
   | <CLUSTER_NAMESPACE> | 您為 big data cluster 提供的名稱。 |
   | <SQL_MASTER_IP> | 主要實例的 IP 位址。 |
   | <SQL_MASTER_SA_PASSWORD> | 主要實例的 SA 密碼。 |
   | <KNOX_IP> | HDFS/Spark 閘道的 IP 位址。 |
   | <KNOX_PASSWORD> | HDFS/Spark 閘道的密碼。 |

   > [!TIP]
   > 使用[kubectl](cluster-troubleshooting-commands.md)來尋找 SQL Server 主要實例和 KNOX 的 IP 位址。 執行`kubectl get svc -n <your-big-data-cluster-name>`並查看主要實例 (**主要-svc-外部**) 和 Knox (**閘道-svc-外部**) 的外部 IP 位址。 叢集的預設名稱是**mssql-cluster**。

1. 執行啟動程式腳本。

   ```bash
   sudo env "PATH=$PATH" ./bootstrap-sample-db.sh <CLUSTER_NAMESPACE> <SQL_MASTER_IP> <SQL_MASTER_SA_PASSWORD> <KNOX_IP> <KNOX_PASSWORD>
   ```

## <a name="next-steps"></a>後續步驟

執行啟動程式腳本之後, 您的 big data 叢集就會有範例資料庫和 HDFS 資料。 下列教學課程會使用範例資料來示範 big data cluster 功能:

資料虛擬化:

- [教學課程：查詢 SQL Server big data 叢集中的 HDFS](tutorial-query-hdfs-storage-pool.md)
- [教學課程：從 SQL Server big data cluster 查詢 Oracle](tutorial-query-oracle.md)

資料內嵌:

- [教學課程：使用 Transact-sql 將資料內嵌至 SQL Server 資料集區](tutorial-data-pool-ingest-sql.md)
- [教學課程：使用 Spark 作業將資料內嵌至 SQL Server 資料集區](tutorial-data-pool-ingest-spark.md)

Notebook

- [教學課程：在 SQL Server 2019 big data 叢集上執行範例筆記本](tutorial-notebook-spark.md)