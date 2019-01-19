---
title: 載入範例資料
titleSuffix: SQL Server 2019 big data clusters
description: 本教學課程會示範如何將範例資料載入 SQL Server 的巨量資料叢集。 範例資料包含在 SQL Server 的主要執行個體中的關聯式資料。 它也會包含在存放集區中的 HDFS 資料。 這項資料會支援其他教學課程，這一節。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 01/17/2019
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 207d2d01278d96456bcec44814efe76fdae70fdf
ms.sourcegitcommit: e3f5b70bbb4c66294df8c7b2c70186bdf2365af9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/18/2019
ms.locfileid: "54397507"
---
# <a name="tutorial-load-sample-data-into-a-sql-server-2019-big-data-cluster"></a>教學課程：將範例資料載入 SQL Server 2019 巨量資料叢集

本教學課程說明如何使用指令碼將範例資料載入 SQL Server 2019 巨量資料叢集 （預覽）。 許多文件中的其他教學課程都使用此範例資料。

> [!TIP]
> 您可以在中找到其他範例可供 SQL Server 2019 巨量資料叢集 （預覽） [sql server 範例](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster)GitHub 存放庫。 它們位於**sql-server-samples/samples/features/sql-big-data-cluster/** 路徑。

## <a name="prerequisites"></a>先決條件

- [已部署的巨量資料叢集](deployment-guidance.md)
- [巨量資料工具](deploy-big-data-tools.md)
   - **mssqlctl**
   - **kubectl**
   - **sqlcmd**
   - **curl**

## <a id="sampledata"></a> 載入範例資料

下列步驟會使用啟動程序的指令碼，下載 SQL Server 資料庫備份，並將資料載入至您的巨量資料叢集。 為了方便使用，這些步驟已細分[Windows](#windows)並[Linux](#linux)區段。

## <a id="windows"></a> Windows

下列步驟說明如何使用 Windows 用戶端的範例資料載入您的巨量資料叢集。

1. 開啟新的 Windows 命令提示字元。

   > [!IMPORTANT]
   > 請勿使用 Windows PowerShell 的步驟執行。 在 PowerShell 中，指令碼會失敗，因為它會使用的 PowerShell 版本**curl**。

1. 使用**curl**下載範例資料的啟動程序的指令碼。

   ```cmd
   curl -o bootstrap-sample-db.cmd "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.cmd"
   ```

1. 下載**啟動程序-範例-db.sql** Transact SQL 指令碼。 啟動程序的指令碼會呼叫此指令碼。

   ```cmd
   curl -o bootstrap-sample-db.sql "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.sql"
   ```

1. 啟動程序的指令碼需要下列位置的參數，為您的巨量資料叢集：

   | 參數 | 描述 |
   |---|---|
   | <CLUSTER_NAMESPACE> | 您給予您的巨量資料叢集的名稱。 |
   | <SQL_MASTER_IP> | 主要執行個體的 IP 位址。 |
   | <SQL_MASTER_SA_PASSWORD> | 主要執行個體的 SA 密碼。 |
   | <KNOX_IP> | HDFS/Spark 閘道 IP 位址。 |
   | <KNOX_PASSWORD> | HDFS/Spark 閘道的密碼。 |

   > [!TIP]
   > 使用[kubectl](cluster-troubleshooting-commands.md)來尋找 IP 位址的 SQL Server 的主要執行個體和 Knox。 執行`kubectl get svc -n <your-cluster-name>`並查看主要執行個體的外部 IP 位址 (**端點主要集區**) 和 Knox (**服務-安全性-lb**或**服務-安全性-nodeport**).

1. 執行啟動程序的指令碼。

   ```cmd
   .\bootstrap-sample-db.cmd <CLUSTER_NAMESPACE> <SQL_MASTER_IP> <SQL_MASTER_SA_PASSWORD> <KNOX_IP> <KNOX_PASSWORD>
   ```

## <a id="linux"></a> Linux

下列步驟說明如何將範例資料載入您的巨量資料叢集使用 Linux 用戶端。

1. 下載的啟動程序的指令碼，並將可執行檔的權限指派給它。

   ```bash
   curl -o bootstrap-sample-db.sh "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.sh"
   chmod +x bootstrap-sample-db.sh
   ```

1. 下載**啟動程序-範例-db.sql** Transact SQL 指令碼。 啟動程序的指令碼會呼叫此指令碼。

   ```bash
   curl -o bootstrap-sample-db.sql "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.sql"
   ```

1. 啟動程序的指令碼需要下列位置的參數，為您的巨量資料叢集：

   | 參數 | 描述 |
   |---|---|
   | <CLUSTER_NAMESPACE> | 您給予您的巨量資料叢集的名稱。 |
   | <SQL_MASTER_IP> | 主要執行個體的 IP 位址。 |
   | <SQL_MASTER_SA_PASSWORD> | 主要執行個體的 SA 密碼。 |
   | <KNOX_IP> | HDFS/Spark 閘道 IP 位址。 |
   | <KNOX_PASSWORD> | HDFS/Spark 閘道的密碼。 |

   > [!TIP]
   > 使用[kubectl](cluster-troubleshooting-commands.md)來尋找 IP 位址的 SQL Server 的主要執行個體和 Knox。 執行`kubectl get svc -n <your-cluster-name>`並查看主要執行個體的外部 IP 位址 (**端點主要集區**) 和 Knox (**服務-安全性-lb**或**服務-安全性-nodeport**).

1. 執行啟動程序的指令碼。

   ```bash
   sudo env "PATH=$PATH" ./bootstrap-sample-db.sh <CLUSTER_NAMESPACE> <SQL_MASTER_IP> <SQL_MASTER_SA_PASSWORD> <KNOX_IP> <KNOX_PASSWORD>
   ```

## <a name="next-steps"></a>後續步驟

啟動程序的指令碼執行之後，您的巨量資料叢集具有 HDFS 資料與範例資料庫。 若要開始探索此資料與巨量資料叢集，請參閱[教學課程](tutorial-query-hdfs-storage-pool.md)這一節。
