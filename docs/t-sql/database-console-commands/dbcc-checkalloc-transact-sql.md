---
title: "DBCC CHECKALLOC (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 09/07/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CHECKALLOC_TSQL
- DBCC CHECKALLOC
- DBCC_CHECKALLOC_TSQL
- CHECKALLOC
dev_langs:
- TSQL
helpviewer_keywords:
- DBCC CHECKALLOC statement
- checking database space allocation
- database space allocation [SQL Server]
- consistency [SQL Server], disk space allocations
- space allocation [SQL Server]
- allocation checks
- disk space [SQL Server], allocation consistency checks
- space allocation [SQL Server], checking
ms.assetid: bc1218eb-ffff-44ce-8122-6e4fa7d68a79
caps.latest.revision: 76
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 05976158e43d7dfafaf02289462d1537f5beeb36
ms.openlocfilehash: 4cecbb77add5a9afbde3f69bf17ac2bd11bd592b
ms.contentlocale: zh-tw
ms.lasthandoff: 09/08/2017

---
# <a name="dbcc-checkalloc-transact-sql"></a>DBCC CHECKALLOC (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

檢查指定之資料庫的磁碟空間配置結構是否一致。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
DBCC CHECKALLOC   
[  
    ( database_name | database_id | 0   
      [ , NOINDEX   
      | , { REPAIR_ALLOW_DATA_LOSS | REPAIR_FAST | REPAIR_REBUILD } ]  
    )  
    [ WITH   
        {   
          [ ALL_ERRORMSGS ]  
          [ , NO_INFOMSGS ]   
          [ , TABLOCK ]   
          [ , ESTIMATEONLY ]   
        }  
    ]  
]  
```  
  
## <a name="arguments"></a>引數  
 *database_name* | *database_id* | 0   
 要檢查配置和頁面使用量資料庫的識別碼或名稱。
若未指定，或指定 0，就會使用目前的資料庫。
資料庫名稱必須遵循的規則[識別碼](../../relational-databases/databases/database-identifiers.md)。

 NOINDEX  
 指定不應該檢查使用者資料表的非叢集索引。<br>保留 NOINDEX 的目的，只是為了與舊版相容，不會影響 DBCC CHECKALLOC。

 REPAIR_ALLOW_DATA_LOSS \| REPAIR_FAST \| REPAIR_REBUILD  
 指定 DBCC CHECKALLOC 修復發現的錯誤。 *database_name*必須處於單一使用者模式。

 REPAIR_ALLOW_DATA_LOSS  
 嘗試修復所有找到的錯誤。 這些修復可能會造成某些資料的遺失。 REPAIR_ALLOW_DATA_LOSS 是唯一允許修復配置錯誤的選項。

 REPAIR_FAST  
 保留語法的目的，只是為了與舊版相容。 不會執行任何修復動作。

 REPAIR_REBUILD  
 不適用。  
 最好不要使用這些 REPAIR 選項。 若要修復錯誤，我們建議您從備份中還原。 修復作業並不考慮資料表或資料表之間的任何條件約束。 如果指定的資料表涉及一或多項條件約束，建議您在修復作業之後，執行 DBCC CHECKCONSTRAINTS。 如果您必須使用 REPAIR，請執行不含修復選項的 DBCC CHECKDB 來尋找要使用的修復層級。 如果您使用 REPAIR_ALLOW_DATA_LOSS 層級，建議您在搭配這個選項執行 DBCC CHECKDB 之前，先備份資料庫。

 取代所有提及的  
 啟用要指定的選項。

 ALL_ERRORMSGS  
 顯示所有錯誤訊息。 系統預設會顯示所有錯誤訊息。 指定或省略這個選項沒有任何作用。

 NO_INFOMSGS  
 隱藏所有參考訊息和所用的空間報表。

 TABLOCK  
 使 DBCC 命令取得獨佔資料庫鎖定。

 ESTIMATE ONLY  
 顯示指定所有其他選項時，請執行 DBCC CHECKALLOC 所需的 tempdb 空間估計的的量。
  
## <a name="remarks"></a>備註  
DBCC CHECKALLOC 會檢查資料庫中所有頁面的配置狀況，不論頁面類型或頁面所屬物件的類型為何，都是如此。 另外，它也會驗證用來追蹤這些頁面的各種內部結構及其間的關聯性。
如果未指定 NO_INFOMSGS，DBCC CHECKALLOC 會收集資料庫中所有物件的空間使用方式資訊。 這項資訊被印出所找到的任何錯誤。
  
> [!NOTE]  
>DBCC CHECKALLOC 功能包含在[DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)和[DBCC CHECKFILEGROUP](../../t-sql/database-console-commands/dbcc-checkfilegroup-transact-sql.md)。 這表示您不需要在這些陳述式之外，個別執行 DBCC CHECKALLOC。   DBCC CHECKALLOC 不會檢查 FILESTREAM 資料。 FILESTREAM 會將二進位大型物件 (BLOB) 儲存在檔案系統上。  
  
## <a name="internal-database-snapshot"></a>內部資料庫快照集  
DBCC CHECKALLOC 利用內部資料庫快照集來提供執行這些檢查所需要的交易一致性。 如果無法建立快照集，或指定了 TABLOCK，DBCC CHECKALLOC 會試圖取得資料庫的獨佔 (X) 鎖定，以取得必要的一致性。
  
> [!NOTE]  
> 針對 tempdb 執行 DBCC CHECKALLOC 不會執行任何檢查。 這是因為基於效能的考量，tempdb 並無法使用資料庫快照集。 這表示無法取得必要的交易一致性。 停止並啟動 MSSQLSERVER 服務來解決任何 tempdb 配置問題。 此動作會卸除並重新建立 tempdb 資料庫。  
  
## <a name="understanding-dbcc-error-messages"></a>了解 DBCC 錯誤訊息  
DBCC CHECKALLOC 命令執行完成之後，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔中會寫入一則訊息。 如果 DBCC 命令執行成功，該訊息將指出命令已順利完成，並顯示命令執行的時間量。 如果 DBCC 命令由於發生錯誤而在完成檢查之前停止執行，則訊息中會指出命令已經終止，並顯示狀態值以及命令執行的時間量。 下表列出並描述可以包含在訊息中的狀態值。
  
|State|Description|  
|---|---|  
|0|已引發錯誤號碼 8930。 這表示中繼資料損毀使 DBCC 命令終止。|  
|1|已引發錯誤號碼 8967。 發生內部 DBCC 錯誤。|  
|2|修復緊急模式資料庫期間發生失敗。|  
|3|這表示中繼資料損毀使 DBCC 命令終止。|  
|4|偵測到判斷提示或存取違規。|  
|5|發生使 DBCC 命令終止的未知錯誤。|  
  
## <a name="error-reporting"></a>錯誤報告  
小型傾印檔案 (SQLDUMP*nnnn*.txt) 中建立[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]每當 DBCC CHECKALLOC 偵測到損毀錯誤時的記錄檔目錄。 當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體已啟用「功能使用方式」資料收集及「錯誤報告」功能時，這個檔案會自動轉送到 [!INCLUDE[msCoName](../../includes/msconame-md.md)]。 收集的資料是用來提升 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的功能。
傾印檔案包含 DBCC CHECKALLOC 命令的結果以及其他診斷輸出。 這個檔案具有限制的任意存取控制清單 (DACL)。 存取限於[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]服務帳戶和系統管理員角色的成員。 根據預設，系統管理員角色包含 Windows BUILTIN\Administrators 群組和本機系統管理員群組的所有成員。 如果資料收集程序失敗，DBCC 命令不會失敗。
  
## <a name="resolving-errors"></a>解決錯誤  
如果 DBCC CHECKALLOC 報告任何錯誤，建議您從資料庫備份中還原資料庫，而不要執行修復。 如果備份不存在，執行修復可以更正報告的錯誤；不過，更正錯誤可能需要刪除一些頁面，因而也會刪除資料。
您可以在使用者交易中執行修復。 這可讓您回復變更。 如果回復變更，資料庫仍會包含錯誤，且必須從備份中還原。 修復完成之後，請備份資料庫。
  
## <a name="result-sets"></a>結果集  
下表說明 DBCC CHECKALLOC 傳回的資訊。
  
|項目|Description|  
|---|---|  
|FirstIAM|僅供內部使用。|  
|Root|僅供內部使用。|  
|Dpages|資料頁面計數。|  
|使用的頁面|已配置的頁面。|  
|專用的範圍|配置給物件的範圍。<br /><br /> 如果使用混合的配置頁面，可能會有未以範圍來配置的頁面。|  
  
另外，DBCC CHECKALLOC 也會報告每個檔案中各個索引和資料分割的配置摘要。 這份摘要描述資料的散發。
  
|項目|Description|  
|---|---|  
|保留的頁面|配置給索引的頁面，以及配置範圍中未使用的頁面。|  
|使用的頁面|索引所配置且使用中的頁面。|  
|資料分割識別碼|僅供內部使用。|  
|配置單位識別碼|僅供內部使用。|  
|同資料列資料|頁面包含索引或堆積資料。|  
|LOB 資料|頁面包含**varchar （max)**， **nvarchar （max)**， **varbinary （max)**，**文字**， **ntext**， **xml**，和**映像**資料。|  
|資料列溢位資料|頁面包含已進行 off-row 發送的可變長度資料行資料。|  
  
除非指定了 ESTIMATEONLY 或 NO_INFOMSGS，否則，DBCC CHECKALLOC 會傳回下列結果集 (值可能會不同)。
  
```sql
DBCC results for 'master'.  
***************************************************************  
Table sysobjects                Object ID 1.  
Index ID 1         FirstIAM (1:11)   Root (1:12)    Dpages 22.  
    Index ID 1. 24 pages used in 5 dedicated extents.  
Index ID 2         FirstIAM (1:1368)   Root (1:1362)    Dpages 10.  
    Index ID 2. 12 pages used in 2 dedicated extents.  
Index ID 3         FirstIAM (1:1392)   Root (1:1408)    Dpages 4.  
    Index ID 3. 6 pages used in 0 dedicated extents.  
Total number of extents is 7.  
***************************************************************  
'...'  
***************************************************************  
Table spt_server_info                Object ID 1938105945.  
Index ID 1         FirstIAM (1:520)   Root (1:508)    Dpages 1.  
    Index ID 1. 3 pages used in 0 dedicated extents.  
Total number of extents is 0.  
***************************************************************  
Processed 52 entries in sysindexes for database ID 1.  
File 1. Number of extents = 210, used pages = 1126, reserved pages = 1280.  
           File 1 (number of mixed extents = 73, mixed pages = 184).  
    Object ID 1, Index ID 0, data extents 5, pages 24, mixed extent pages 9.  
'...'  
    Object ID 1938105945, Index ID 0, data extents 0, pages 3, mixed extent pages 3.  
Total number of extents = 210, used pages = 1126, reserved pages = 1280 in this database.  
       (number of mixed extents = 73, mixed pages = 184) in this database.  
CHECKALLOC found 0 allocation errors and 0 consistency errors in database 'master'.  
DBCC results for 'master'.  
***************************************************************  
Table sys.sysrowsetcolumns                Object ID 4.  
Index ID 1, partition ID 262144, alloc unit ID 262144 (type In-row data). FirstIAM (1:98). Root (1:94). Dpages 7.  
Index ID 1, partition ID 262144, alloc unit ID 262144 (type In-row data). 9 pages used in 1 dedicated extents.  
Index ID 1, partition ID 262144, alloc unit ID 262398 (type Row-overflow data). FirstIAM (0:0). Root (0:0). Dpages 0.  
Index ID 1, partition ID 262144, alloc unit ID 262398 (type Row-overflow data). 0 pages used in 0 dedicated extents.  
Total number of extents is 1.  
...  
***************************************************************  
Processed 201 entries in system catalog for database ID 1.  
File 1. Number of extents = 44, used pages = 300, reserved pages = 345.  
           File 1 (number of mixed extents = 29, mixed pages = 225).  
    Object ID 4, index ID 1, partition ID 262144, alloc unit ID 262144 (type In-row data), data extents 1, pages 9, mixed extent pages 8.  
    Object ID 5, index ID 1, partition ID 327680, alloc unit ID 327680 (type In-row data), data extents 0, pages 2, mixed extent pages 2.  
    Object ID 7, index ID 1, partition ID 458752, alloc unit ID 458752 (type In-row data), data extents 0, pages 5, mixed extent pages 5.  
    Object ID 8, index ID 0, partition ID 524288, alloc unit ID 524288 (type In-row data), data extents 0, pages 2, mixed extent pages 2.  
    Object ID 13, index ID 1, partition ID 851968, alloc unit ID 851968 (type In-row data), data extents 1, pages 9, mixed extent pages 8.  
    Object ID 15, index ID 1, partition ID 983040, alloc unit ID 983040 (type In-row data), data extents 0, pages 2, mixed extent pages 2.  
    Object ID 26, index ID 1, partition ID 281474978414592, alloc unit ID 1703937 (type In-row data), data extents 0, pages 3, mixed extent pages 3.  
    Object ID 27, index ID 1, partition ID 281474978480128, alloc unit ID 1769473 (type In-row data), data extents 0, pages 3, mixed extent pages 3.  
    Object ID 27, index ID 2, partition ID 562949955190784, alloc unit ID 1769474 (type In-row data), index extents 0, pages 3, mixed extent pages 3.  
...  
    Object ID 1179151246, index ID 1, partition ID 72057594038845440, alloc unit ID 13435136 (type In-row data), data extents 2, pages 18, mixed extent pages 8.  
    Object ID 1179151246, index ID 2, partition ID 72057594038910976, alloc unit ID 13566208 (type In-row data), index extents 1, pages 16, mixed extent pages 8.  
    Object ID 1911677858, index ID 0, partition ID 72057594039631872, alloc unit ID 15073536 (type In-row data), data extents 0, pages 2, mixed extent pages 2.  
Total number of extents = 41, used pages = 289, reserved pages = 323 in this database.  
       (number of mixed extents = 27, mixed pages = 211) in this database.  
CHECKALLOC found 0 allocation errors and 0 consistency errors in database 'master'.  
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
當指定 ESTIMATEONLY 時，DBCC CHECKALLOC 會傳回下列結果集。
  
```sql
Estimated TEMPDB space needed for CHECKALLOC (KB)   
-------------------------------------------------   
34  
  
(1 row(s) affected)  
  
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>Permissions  
需要 sysadmin 固定伺服器角色或 db_owner 固定資料庫角色的成員資格。
  
## <a name="examples"></a>範例  
下列範例會針對目前資料庫和 `DBCC CHECKALLOC` 資料庫執行 `AdventureWorks2012`。
  
```sql  
-- Check the current database.  
DBCC CHECKALLOC;  
GO  
-- Check the AdventureWorks2012 database.  
DBCC CHECKALLOC (AdventureWorks2012);  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)
  
  


