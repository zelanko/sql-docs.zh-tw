---
title: 設定複寫 (SSMS)
description: 了解如何設定 Linux 上的 SQL Server 複寫。 使用 SQL Server Management Studio (SSMS) 或 Transact-SQL 預存程序來設定複寫。
ms.custom: seo-dt-2019
author: VanMSFT
ms.author: vanto
ms.reviewer: vanto
ms.date: 03/20/2018
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.technology: linux
titleSuffix: SQL Server on Linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 0c4a22b43650292055a7b1c48b9408b4d8e85f6c
ms.sourcegitcommit: 610e3ebe21ac6575850a29641a32f275e71557e3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/07/2020
ms.locfileid: "91785055"
---
# <a name="configure-sql-server-replication-on-linux"></a>在 Linux 上設定 SQL Server 複寫

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] 推出對 Linux 上的 SQL Server 執行個體進行 SQL Server 複寫的功能。

如需複寫的詳細資訊，請參閱 [SQL Server 複寫文件](../relational-databases/replication/sql-server-replication.md)。

使用 SQL Server Management Studio (SSMS) 或 Transact-SQL 預存程序，在 Linux 上設定複寫。

* 若要使用 SSMS，請依照本文中的指示進行。

  在 Windows 作業系統上使用 SSMS 連線到 SQL Server 執行個體。 如需背景和指示，請參閱[使用 SSMS 管理 Linux 上的 SQL Server](./sql-server-linux-manage-ssms.md)。
  
* 如需預存程序的範例，請遵循[在 Linux 上設定 SQL Server 複寫](sql-server-linux-replication-tutorial-tsql.md)教學課程。

## <a name="prerequisites"></a>必要條件

在設定發行者、散發者和訂閱者之前，您必須完成幾個 SQL Server 執行個體的設定步驟。

1. 啟用 SQL Server Agent，使用複寫代理程式。 在所有 Linux 伺服器上，從終端執行下列命令。

  ```bash
  sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true
  sudo systemctl restart mssql-server
  ```

1. 設定用於複寫的 SQL Server 執行個體。 若要設定用於複寫的 SQL Server 執行個體，請在參與複寫的所有執行個體上執行 `sys.sp_MSrepl_createdatatypemappings`。

  ```sql
  USE msdb
  GO
  exec sys.sp_MSrepl_createdatatypemappings;
  GO
  ```

1. 建立快照集資料夾。 SQL Server Agent 需要可讀取/寫入的快照集資料夾。 在散發者上建立快照集資料夾。

  若要建立快照集資料夾，並授與 `mssql` 使用者存取權，請執行下列命令：

  ```bash
  sudo mkdir /var/opt/mssql/data/ReplData/
  sudo chown mssql /var/opt/mssql/data/ReplData/
  sudo chgrp mssql /var/opt/mssql/data/ReplData/
  ```

## <a name="configure-and-monitor-replication-with-sql-server-management-studio-ssms"></a>使用 SQL Server Management Studio (SSMS) 設定和監視複寫

### <a name="configure-the-distributor"></a>設定散發者
  
若要設定散發者： 

1. 在 SSMS 的物件總管中，連線到您的 SQL Server 執行個體。

1. 以滑鼠右鍵按一下 [複寫]****，然後按一下 [設定散發...]****。

1. 依照「設定散發精靈」**** 的指示進行。

### <a name="create-publication-and-articles"></a>建立發行集和發行項

若要建立發行集和發行項：

1. 在物件總管中，按一下 [複寫] > [本機發行集]> [新增發行集...]。

1. 依照「新增發行集精靈」**** 的指示設定複寫類型，以及屬於發行集的發行項。

### <a name="configure-the-subscription"></a>設定訂閱

若要設定物件總管中的訂閱，請按一下 [複寫] > [本機訂閱]> [新增訂閱...]。

### <a name="monitor-replication-jobs"></a>監視複寫作業

使用複寫監視器，監視複寫作業。

在物件總管中，以滑鼠右鍵按一下 [複寫]****，然後按一下 [啟動複寫監視器]****。

## <a name="next-steps"></a>後續步驟

[概念：Linux 上的 SQL Server 複寫](sql-server-linux-replication.md)

[複寫預存程序](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)。
