---
title: "卸除資料庫 (TRANSACT-SQL) |Microsoft 文件"
ms.custom:
- SQL2016_New_Updated
ms.date: 09/15/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP DATABASE
- DROP_DATABASE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- snapshots [SQL Server database snapshots], deleting
- removing databases
- database snapshots [SQL Server], removing
- deleting databases
- dropping databases
- databases [SQL Server], dropping
- DROP DATABASE statement
- database removal [SQL Server], DROP DATABASE statement
ms.assetid: 477396a9-92dc-43c9-9b97-42c8728ede8e
caps.latest.revision: 83
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: a9397f427cac18d0c8bfc663f6bd477b0440b8a3
ms.openlocfilehash: 4dedcfa3e055e9f3b6d71bc14aed71f07260d323
ms.contentlocale: zh-tw
ms.lasthandoff: 09/15/2017

---
# <a name="drop-database-transact-sql"></a>DROP DATABASE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw_md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

  可從一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，移除一個或多個使用者資料庫或資料庫快照集。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- SQL Server Syntax  
DROP DATABASE [ IF EXISTS ] { database_name | database_snapshot_name } [ ,...n ] [;]  
```  
  
```  
-- Azure SQL Database, Azure SQL Data Warehouse and Parallel Data Warehouse Syntax   
DROP DATABASE database_name [;]  
```  
  
## <a name="arguments"></a>引數  
 *如果存在*  
 **適用於**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 至 [目前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658))。  
  
 只有當它已經存在有條件地卸除資料庫。  
  
 *database_name*  
 這是要移除的資料庫名稱。 若要顯示資料庫的清單，請使用[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)目錄檢視。  
  
 *database_snapshot_name*  
 **適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 這是要移除的資料庫快照集名稱。  
  
## <a name="general-remarks"></a>一般備註  
 無論資料庫的狀態為離線、唯讀或受到質疑等，都可以卸除該資料庫。 若要顯示資料庫的目前狀態，請使用**sys.databases**目錄檢視。  
  
 若要重新建立已經卸除的資料庫，只有還原備份一途。 資料庫快照集無法備份，因此也無法還原。  
  
 當資料庫已卸除時， [master 資料庫](../../relational-databases/databases/master-database.md)應該進行備份。  
  
 卸除資料庫時，不但會從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體中刪除該資料庫，同時也會刪除該資料庫所用的實體磁碟檔。 如果資料庫或其任何一個檔案在卸除時離線，磁碟檔就不會被刪除。 這些檔案可以利用 [Windows 檔案總管]，以手動方式刪除。 若要從目前的伺服器移除資料庫，而不刪除在檔案系統中，使用[sp_detach_db](../../relational-databases/system-stored-procedures/sp-detach-db-transact-sql.md)。  
  
> [!WARNING]  
>  卸除資料庫具有 FILE_SNAPSHOT 與其相關聯的備份將會成功，但不是會刪除資料庫檔案具有相關聯的快照集以避免使無效參考這些資料庫檔案的備份。 檔案將會被截斷，但不是會實際刪除為了 FILE_SNAPSHOT 備份的保留不變。 如需詳細資訊，請參閱 [使用 Microsoft Azure Blob 儲存體服務進行 SQL Server 備份及還原](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)。 **適用於**:[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]透過[新版](http://go.microsoft.com/fwlink/p/?LinkId=299658)。  
  
### [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 卸除資料庫快照集時，會刪除的執行個體的資料庫快照集[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]並刪除快照集所使用的實體 NTFS 檔案系統疏鬆檔案。 使用受資料庫快照集的疏鬆檔案的相關資訊，請參閱[資料庫快照集 &#40;SQL Server &#41;](../../relational-databases/databases/database-snapshots-sql-server.md). 卸除資料庫快照集會清除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的計畫快取。 清除計畫快取會導致重新編譯所有後續執行計畫，而且可能會導致查詢效能突然暫時下降。 針對每次清除計畫快取的快取存放區，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔會包含下列參考訊息：「由於某些資料庫維護或重新設定作業，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 '%s' 快取存放區 (計畫快取的一部分) 發生 %d 次快取存放區排清」。 只要在該時間間隔內快取發生排清，這個訊息就會每五分鐘記錄一次。  
  
## <a name="interoperability"></a>互通性  
  
### <a name="sql-server"></a>SQL Server  
 若要卸除針對異動複寫而發行的資料庫，或是針對合併式複寫而發行或訂閱的資料庫，必須先從該資料庫移除複寫。 如果資料庫損毀，或者無法先移除複寫，或者兩種情況都有，多半還是能夠卸除資料庫，方法是利用 ALTER DATABASE，將資料庫設為離線，然後再卸除它。  
  
 如果資料庫有涉及記錄傳送，請在卸除資料庫之前移除記錄傳送。 如需詳細資訊，請參閱[關於記錄傳送 &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)。  
  
  
## <a name="limitations-and-restrictions"></a>限制事項  
 [系統資料庫](../../relational-databases/databases/system-databases.md)無法卸除。  
  
 DROP DATABASE 陳述式必須執行自動認可模式，且不能在明確或隱含的交易中。 自動認可模式是預設的交易管理模式。  
  
 您無法卸除目前正在使用的資料庫。 也就是開放給任何使用者讀取或寫入的資料庫。 若要從資料庫移除使用者，請使用 ALTER DATABASE，將資料庫設為 SINGLE_USER。  
  
### [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 在卸除資料庫之前，必須先卸除該資料庫上的任何資料庫快照集。  
  
 卸除針對 Stretch Database 的資料庫啟用並不會移除的遠端資料。 如果您想要刪除遠端資料，您必須手動將它移除。  
  
### [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
 您必須連接至 master 資料庫，才能卸除資料庫。
  
 DROP DATABASE 陳述式必須是 SQL 批次中的唯一陳述式，而且您一次只能卸除一個資料庫。
  
### [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]  
 您必須連接至 master 資料庫，才能卸除資料庫。
  
 DROP DATABASE 陳述式必須是 SQL 批次中的唯一陳述式，而且您一次只能卸除一個資料庫。

## <a name="permissions"></a>Permissions  
  
### [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 需要**控制項**資料庫的權限或**ALTER ANY DATABASE**權限或成員資格**db_owner**固定的資料庫角色。  
  
### [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
 只有伺服器層級主體登入 （透過佈建程序所建立） 或成員的**dbmanager**資料庫角色可以卸除資料庫。  
  
### [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 需要**控制項**資料庫的權限或**ALTER ANY DATABASE**權限或成員資格**db_owner**固定的資料庫角色。  
  
## <a name="examples"></a>範例  
  
### <a name="a-dropping-a-single-database"></a>A. 卸除單一資料庫  
 下列範例會移除 `Sales` 資料庫。  
  
```  
DROP DATABASE Sales;  
```  
  
### <a name="b-dropping-multiple-databases"></a>B. 卸除多個資料庫  
  
**適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 下列範例會移除每一個列出的資料庫。  
  
```  
DROP DATABASE Sales, NewSales;  
```  
  
### <a name="c-dropping-a-database-snapshot"></a>C. 卸除資料庫快照集  
  
**適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 下列範例會移除名為 `sales`_`snapshot0600` 的資料庫快照集，而不會影響來源資料庫。  
  
```  
DROP DATABASE sales_snapshot0600;  
```  
  
## <a name="see-also"></a>另請參閱  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)  
  
  

