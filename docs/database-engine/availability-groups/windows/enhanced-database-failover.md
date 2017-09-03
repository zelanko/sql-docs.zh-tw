---
title: "將增強資料庫容錯移轉新增至可用性群組 (SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 05/10/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Availability Groups [SQL Server], enhanced database failover
- Availability Groups [SQL Server], failover
ms.assetid: 
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: ff670b7dd9ece16e281d9d0944a5d66d1529b726
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---

# <a name="add-enhanced-database-failover-to-an-availability-group-sql-server"></a>將增強資料庫容錯移轉新增至可用性群組 (SQL Server)

在 SQL Server 2012 和 2014 中，如果參與主要複本上可用性群組的資料庫無法寫入交易，就不會觸發容錯移轉，即使同步處理並設定複本以進行自動容錯移轉也是一樣。

SQL Server 2016 引進名為「增強資料庫容錯移轉」的新選擇性行為，可透過精靈或使用 Transact-SQL 進行傳送。 如果啟用此選項，並設定自動容錯移轉，則一個參與可用性群組的資料庫無法再寫入交易時，這樣會觸發容錯移轉至同步處理的次要複本。

**案例 1**

可用性群組設定於執行個體 A 與執行個體 B 之間，包含名為 DB1 的單一資料庫。 DB1 的資料檔案是在磁碟機 E 上，而其交易記錄檔是在磁碟機 F 上。可用性模式設定為具有自動容錯移轉的同步認可。 新的增強資料庫容錯移轉選項設定於可用性群組上。 兩個複本目前都處於已同步處理狀態。 發生問題，導致磁碟機 E 失敗。 因為磁碟機 E 未包含交易記錄，所以此案例不會導致增強資料庫容錯移轉。  

**案例 2**

這具有的可用性群組組態與案例 1 相同。 這次交易記錄磁碟機 F 會失敗，而不是磁碟機 E 失敗。 這會觸發容錯移轉，因為它符合增強資料庫容錯移轉所涵蓋的條件：找不到交易記錄，這表示資料庫無法寫入交易。

**案例 3**

可用性群組設定於執行個體 A 與執行個體 B 之間，包含兩個資料庫：DB1 和 DB2。 可用性模式設定為具有自動容錯移轉模式的同步認可，並啟用增強資料庫容錯移轉。 遺失包含 DB2 資料和交易記錄檔之磁碟的存取權。 偵測到問題時，可用性群組會自動容錯移轉至執行個體 B。

## <a name="configuring-and-viewing-the-enhanced-database-failover-option"></a>設定和檢視增強資料庫容錯移轉選項

增強資料庫容錯移轉可以使用 SQL Server Management Studio 或 Transact-SQL 進行設定。 PowerShell Cmdlet 目前沒有這項功能。 預設會停用增強資料庫容錯移轉。

### <a name="sql-server-management-studio"></a>Transact-SQL

在使用 SQL Server Management Studio 建立協助工具群組期間，可以啟用增強資料庫容錯移轉。 可用性群組在建立之後的唯一停用或啟用方式是使用 Transact-SQL。

建立手動可用性群組

使用[使用新增可用性群組對話方塊 (SQL Server Management Studio)](use-the-new-availability-group-dialog-box-sql-server-management-studio.md) 主題中找到的指示，以建立可用性群組。 若要啟用增強資料庫容錯移轉，請選取它在「資料庫層級健全狀況偵測」旁邊的核取方塊。

使用可用性群組精靈

使用[使用可用性群組精靈 (SQL Server Management Studio)](use-the-availability-group-wizard-sql-server-management-studio.md) 主題中找到的指示。 在 [指定可用性群組名稱] 對話方塊上，可以找到啟用增強資料庫容錯移轉的選項。 若要啟用它，請核取「資料庫層級健全狀況偵測」旁邊的方塊。

### <a name="transact-sql"></a>Transact-SQL

若要在建立可用性群組期間設定增強資料庫容錯移轉行為，DB_FAILOVER 必須設定為 ON，如下所示：
```
CREATE AVAILABILITY GROUP [AGNAME]
WITH ( DB_FAILOVER = ON)
...
```
若要在設定可用性群組之後新增此行為，請使用 ALTER AVAILABILITY GROUP 命令：
```
ALTER AVAILABILITY GROUP [AGNAME] SET (DB_FAILOVER = ON)
```
若要停用此行為，請發出下列 ALTER AVAILABILITY GROUP 命令：
```
ALTER AVAILABILITY GROUP [AGNAME] SET (DB_FAILOVER = OFF)
```
### <a name="dynamic-management-view"></a>動態管理檢視
若要查看可用性群組是否已啟用增強資料庫容錯移轉，請查詢動態管理檢視 `sys.availablity_groups`。 如果停用，資料行 `db_failover` 會是零，如果啟用，則是 1。 

## <a name="next-steps"></a>後續的步驟 

- [設定資料庫健全狀況偵測](sql-server-always-on-database-health-detection-failover-option.md)

- [使用可用性群組精靈 (SQL Server Management Studio)](use-the-availability-group-wizard-sql-server-management-studio.md)

- [使用新增可用性群組對話方塊 (SQL Server Management Studio)](use-the-new-availability-group-dialog-box-sql-server-management-studio.md)
 
- [使用 Transact-SQL 建立可用性群組](create-an-availability-group-transact-sql.md)

>此內容的作者：[Allan Hirt](http://mvp.microsoft.com/en-us/PublicProfile/4025254?fullName=Allan%20%20Hirt)，Microsoft 最有價值專家。

