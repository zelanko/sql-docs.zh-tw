---
title: 在 Linux 上設定 SQL Server 複寫 |Microsoft Docs
description: 本文說明如何在 Linux 上設定 SQL Server 複寫。
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 03/20/2018
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 29c8dd4ef4898796722e1c54eeaff94afef1c0c6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66705332"
---
# <a name="configure-sql-server-replication-on-linux"></a>在 Linux 上設定 SQL Server 複寫

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] 介紹 SQL Server 複寫的 Linux 上的 SQL Server 執行個體。

如需複寫的詳細資訊，請參閱 < [SQL Server 複寫的文件](../relational-databases/replication/sql-server-replication.md)。

在 Linux 上使用 SQL Server Management Studio (SSMS) 或 TRANSACT-SQL 預存程序設定複寫。

* 若要使用 SSMS，請遵循這篇文章中的指示。

  使用 Windows 作業系統上的 SSMS 連線到 SQL Server 執行個體。 如需背景和指示，請參閱[使用 SSMS 管理 SQL Server on Linux](./sql-server-linux-manage-ssms.md)。
  
* 如需預存程序的範例，請遵循[在 Linux 上的設定 SQL Server 複寫](sql-server-linux-replication-tutorial-tsql.md)教學課程。

## <a name="prerequisites"></a>先決條件

設定 「 發行者 」、 「 散發者 」 和 「 訂閱者 」 時，您需要完成幾個 SQL Server 執行個體的組態步驟。

1. 啟用 SQL Server Agent 使用複寫代理程式。 所有 Linux 伺服器上，請在終端機中執行下列命令。

  ```bash
  sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true
  sudo systemctl restart mssql-server
  ```

1. 設定複寫的 SQL Server 執行個體。 若要設定複寫的 SQL Server 執行個體，執行`sys.sp_MSrepl_createdatatypemappings`參與複寫的所有執行個體上。

  ```sql
  USE msdb
  GO
  exec sys.sp_MSrepl_createdatatypemappings;
  GO
  ```

1. 建立快照集資料夾。 SQL Server 代理程式還需要讀取/寫入的快照集資料夾。 散發者上建立快照集資料夾。

  若要建立快照集資料夾，然後授與存取權`mssql`使用者，請執行下列命令：

  ```bash
  sudo mkdir /var/opt/mssql/data/ReplData/
  sudo chown mssql /var/opt/mssql/data/ReplData/
  sudo chgrp mssql /var/opt/mssql/data/ReplData/
  ```

## <a name="configure-and-monitor-replication-with-sql-server-management-studio-ssms"></a>設定和監視複寫使用 SQL Server Management Studio (SSMS)

### <a name="configure-the-distributor"></a>設定散發者
  
若要設定 「 散發者 」: 

1. 在 SSMS 中，連接到您的 [物件總管] 中的 SQL Server 執行個體。

1. 以滑鼠右鍵按一下**複寫**，然後按一下**設定散發...** .

1. 遵循上的指示**設定散發精靈 」** 。

### <a name="create-publication-and-articles"></a>建立發行集和文件

若要建立發行集和發行項：

1. 在 [物件總管] 中，按一下**複寫** > **本機發行集**> **新增發行集...** .

1. 依照指令**新的發行集精靈 」** 設定複寫，以及屬於發行集之發行項的類型。

### <a name="configure-the-subscription"></a>設定訂用帳戶

若要在 [物件總管] 中設定訂用帳戶，請按一下**複寫** > **本機訂用帳戶**> **新訂用帳戶...** .

### <a name="monitor-replication-jobs"></a>監視複寫作業

您可以使用複寫監視器來監視複寫作業。

在 [物件總管] 中，以滑鼠右鍵按一下**複寫**，然後按一下**啟動複寫監視器**。

## <a name="next-steps"></a>後續步驟

[概念：在 Linux 上的 SQL Server 複寫](sql-server-linux-replication.md)

[複寫預存程序](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)。
