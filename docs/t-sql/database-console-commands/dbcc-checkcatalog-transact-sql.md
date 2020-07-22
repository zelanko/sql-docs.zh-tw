---
title: DBCC CHECKCATALOG (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DBCC_CHECKCATALOG_TSQL
- DBCC CHECKCATALOG
- CHECKCATALOG_TSQL
- CHECKCATALOG
dev_langs:
- TSQL
helpviewer_keywords:
- catalogs [SQL Server], consistency checks
- checking catalog consistency
- DBCC CHECKCATALOG statement
- integrity [SQL Server], catalogs
- consistency [SQL Server], catalogs
ms.assetid: 8076eb4e-f049-44bf-9a35-45cdd6ef0105
author: pmasl
ms.author: umajay
ms.openlocfilehash: 0a19aa7e89494d27d073c1305a75c531cf3ffda0
ms.sourcegitcommit: edba1c570d4d8832502135bef093aac07e156c95
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/20/2020
ms.locfileid: "86485089"
---
# <a name="dbcc-checkcatalog-transact-sql"></a>DBCC CHECKCATALOG (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  檢查指定資料庫內的目錄一致性。 資料庫必須在線上。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
DBCC CHECKCATALOG   
[   
    (   
    database_name | database_id | 0  
    )  
]  
    [ WITH NO_INFOMSGS ]   
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引數
 *database_name* | *database_id* | 0  
 這是要檢查目錄一致性的資料庫名稱或識別碼。 若未指定，或指定 0，就會使用目前的資料庫。 資料庫名稱必須符合[識別碼](../../relational-databases/databases/database-identifiers.md)的規則。  
  
 WITH NO_INFOMSGS  
 隱藏所有參考訊息。  
  
## <a name="remarks"></a>備註  
DBCC CATALOG 命令執行完成之後，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔中會寫入一則訊息。 如果 DBCC 命令執行成功，該訊息將指出命令已順利完成，並顯示命令執行的時間量。 如果 DBCC 命令由於發生錯誤而在完成檢查之前停止執行，則訊息中會指出命令已經終止，並顯示狀態值以及命令執行的時間量。 下表列出並描述可以包含在訊息中的狀態值。
  
|State|描述|  
|-----------|-----------------|  
|0|已引發錯誤號碼 8930。 這表示中繼資料損毀使 DBCC 命令終止。|  
|1|已引發錯誤號碼 8967。 發生內部 DBCC 錯誤。|  
|2|修復緊急模式資料庫期間發生失敗。|  
|3|這表示中繼資料損毀使 DBCC 命令終止。|  
|4|偵測到判斷提示或存取違規。|  
|5|發生使 DBCC 命令終止的未知錯誤。|  
  
DBCC CHECKCATALOG 會在系統中繼資料表之間，執行各種一致性檢查。 DBCC CHECKCATALOG 利用內部資料庫快照集來提供執行這些檢查所需要的交易一致性。 如需詳細資訊，請參閱[檢視資料庫快照集的疏鬆檔案大小 &#40;Transact-SQL&#41;](../../relational-databases/databases/view-the-size-of-the-sparse-file-of-a-database-snapshot-transact-sql.md) 和 [DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md) 中的＜DBCC 內部資料庫快照集使用方式＞一節。
如果無法建立快照集，DBCC CHECKCATALOG 會獲取獨佔資料庫鎖定來取得必要的一致性。 如果偵測到任何不一致的情況，它們無法修復，您必須從備份中還原資料庫。
  
> [!NOTE]  
> 針對 **tempdb** 執行 DBCC CHECKCATALOG 並不會執行任何檢查。 這是因為基於效能的考量，**tempdb** 並無法使用資料庫快照集。 這表示無法取得必要的交易一致性。 請回收伺服器來解決任何 **tempdb** 中繼資料問題。  
  
> [!NOTE]  
> DBCC CHECKCATALOG 不會檢查 FILESTREAM 資料。 FILESTREAM 會將二進位大型物件 (BLOB) 儲存在檔案系統上。  
  
DBCC CHECKCATALOG 也是作為 [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) 的一部分來執行。
  
## <a name="result-sets"></a>結果集  
如果未指定任何資料庫，DBCC CHECKCATALOG 會傳回：
  
```
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
如果將 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 指定為資料庫名稱，則 DBCC CHECKCATALOG 會傳回：
  
```
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>權限  
 需要系統管理員 **sysadmin** 固定伺服器角色或 **db_owner** 固定資料庫角色中的成員資格。  
  
## <a name="examples"></a>範例  
下列範例會檢查目前資料庫和 `AdventureWorks` 資料庫中的目錄完整性。
  
```sql
-- Check the current database.  
DBCC CHECKCATALOG;  
GO  
-- Check the AdventureWorks2012 database.  
DBCC CHECKCATALOG (AdventureWorks2012);  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[系統資料表 &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)
  
