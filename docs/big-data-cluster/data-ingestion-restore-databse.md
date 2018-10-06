---
title: 將資料庫還原到 SQL Server 的巨量資料叢集 |Microsoft Docs
description: ''
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/01/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 04514fb0184fa28e0ba959f3dd33cb2e1ec945cb
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48796105"
---
# <a name="restore-a-database-into-the-sql-server-big-data-cluster-master-instance"></a>將資料庫還原到 SQL Server 巨量資料叢集主要執行個體

要帶入主要執行個體中現有的 SQL Server 資料庫，我們會建議使用的備份、 複製和還原的方法。  在此範例中，我們將說明如何還原 AdventureWorks 資料庫中，但您可以使用任何您擁有的資料庫備份。  您可以下載 AdventureWorks 備份[此處](https://www.microsoft.com/en-us/download/details.aspx?id=49502)。

首先，備份您現有的 SQL Server 資料庫，在 Windows 上 SQL Server 或 Linux 使用任何建立的資料庫備份的一般方法。

將備份檔案複製到 SQL Server 容器的 Kubernetes 叢集的主要執行個體 pod 中。

```bash
kubectl cp <path to .bak file> mssql-data-pool-master-0:/tmp/ -c mssql-data-pool-data -n <name of your cluster>
```

範例

```bash
kubectl cp ~/Downloads/AdventureWorks2016CTP3.bak mssql-data-pool-master-0:/tmp/ -c mssql-data-pool-data -n clustertest
```

然後，確認備份檔案已複製到 pod 容器。

```bash
kubectl exec -it mssql-data-pool-master-0 -n <name of your cluster> -c mssql-data-pool-data -- bin/bash
root@mssql-data-pool-master-0:/# ls /tmp
root@mssql-data-pool-master-0:/# exit
```

範例

```bash
kubectl exec -it mssql-data-pool-master-0 -n clustertest -c mssql-data-pool-data -- bin/bash
root@mssql-data-pool-master-0:/# ls /tmp
```

接下來，在主要執行個體 SQL Server 還原資料庫備份。  如果您要還原的資料庫備份，建立在 Windows 上，您必須取得檔案的名稱。  在 Ops Studio 連線至主要執行個體執行此 SQL 指令碼：

```sql
RESTORE FILELISTONLY FROM DISK='/tmp/<db file name>.bak'
```

範例

```sql
RESTORE FILELISTONLY FROM DISK='/tmp/AdventureWorks2016CTP3.bak'
```

![備份的檔案清單](media/restore-database/database-restore-file-list.png)

現在，將資料庫還原使用像這樣，指令碼以取代所需視您資料庫的備份名稱/路徑。

```sql
RESTORE DATABASE AdventureWorks2016CTP3
FROM DISK='/tmp/AdventureWorks2016CTP3.bak'
WITH MOVE 'AdventureWorks2016CTP3_Data' TO '/var/opt/mssql/data/AdventureWorks2016CTP3_Data.mdf',
        MOVE 'AdventureWorks2016CTP3_Log' TO '/var/opt/mssql/data/AdventureWorks2016CTP3_Log.ldf',
        MOVE 'AdventureWorks2016CTP3_mod' TO '/var/opt/mssql/data/AdventureWorks2016CTP3_mod'
```

現在，如果您想要有高價值資料庫能夠存取資料集區，您將需要的設定資料集區預存程序所開啟，並從 GitHub 存放庫執行這些指令碼。

執行**高值-db configuration\data_pool_ddl_install。SQL**指令碼。

- 安裝程式可支援性的預存程序

執行**高值-db configuration\supportability。SQL**指令碼。
