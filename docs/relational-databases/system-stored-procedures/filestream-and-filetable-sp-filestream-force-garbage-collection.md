---
title: s (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 07/22/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_filestream_force_garbage_collection
- sp_filestream_force_garbage_collection_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- FILESTREAM [SQL Server]
- sp_filestream_force_garbage_collection
ms.assetid: 9d1efde6-8fa4-42ac-80e5-37456ffebd0b
caps.latest.revision: 28
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b567ffa4ac9b56074742999c602914ebe7d3934d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="spfilestreamforcegarbagecollection-transact-sql"></a>sp_filestream_force_garbage_collection (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  強制執行 FILESTREAM 記憶體回收行程，刪除任何不必要的 FILESTREAM 檔案。  
  
 在 FILESTREAM 容器內所有已刪除的檔案都已經由記憶體回收行程清除之前，無法移除容器。 FILESTREAM 記憶體回收行程會自動執行。 不過，如果您需要在記憶體回收行程之前移除容器已執行，您可以手動執行記憶體回收行程使用 s。  
  
  
## <a name="syntax"></a>語法  
  
```  
sp_filestream_force_garbage_collection  
    [ @dbname = ]  'database_name',  
    [ @filename = ] 'logical_file_name' ]  
```  
  
## <a name="arguments"></a>引數  
 **@dbname** = *database_name***'**  
 表示要執行記憶體回收行程之資料庫的名稱。  
  
> [!NOTE]  
>  *dbname*是**sysname**。 如果未指定，則假設目前的資料庫。  
  
 **@filename** = *logical_file_name*  
 指定要執行記憶體回收行程之 FILESTREAM 容器的邏輯名稱。 **@filename** 是選擇性的。 如果未不指定任何邏輯檔名，則記憶體回收行程會清除指定之資料庫中的所有 FILESTREAM 容器。  
  
## <a name="return-code-values"></a>傳回碼值  
  
|||  
|-|-|  
|Value|설명|  
|0|作業成功|  
|1|作業失敗|  
  
## <a name="result-sets"></a>結果集  
  
|Value|Description|  
|-----------|-----------------|  
|*file_name*|指出 FILESTREAM 容器名稱|  
|*num_collected_items*|指出在這個容器中已進行記憶體回收 (已刪除) 的 FILESTREAM 項目 (檔案/目錄) 的數目。|  
|*num_marked_for_collection_items*|指出在這個容器中已標示為記憶體回收的 FILESTREAM 項目 (檔案/目錄) 的數目。 這些項目未被刪除，但可能可刪除下列記憶體回收階段。|  
|*num_unprocessed_items*|指出在這個 FILESTREAM 容器中適合記憶體回收但未處理的 FILESTREAM 項目 (檔案或目錄) 的數目。 項目可能因各種原因未處理，包括下列：<br /><br /> 因為尚未進行記錄備份或檢查點而需要確定的檔案。<br /><br /> 在 FULL 或 BULK_LOGGED 復原模式中的檔案。<br /><br /> 有長時間執行的使用中交易。<br /><br /> 複寫記錄讀取器作業尚未執行。 請參閱下列白皮書[SQL Server 2008 中的 FILESTREAM 儲存體](http://go.microsoft.com/fwlink/?LinkId=209156)如需詳細資訊。|  
|*last_collected_xact_seqno*|傳回指定 FILESTREAM 容器中已進行記憶體回收之檔案的最後一個對應記錄序號 (LSN)。|  
  
## <a name="remarks"></a>備註  
 在要求的資料庫 (和 FILESTREAM 容器) 上，明確執行完成 FILESTREAM 記憶體回收行程工作。 記憶體回收處理序會移除不再需要的檔案。 完成此作業的所需時間取決於該資料庫或容器中的 FILESTREAM 資料大小，以及 FILESTREAM 資料上最近發生的資料操作語言 (DML) 活動量。 雖然這項作業可以在資料庫上線時執行，但因為記憶體回收處理序進行各種 I/O 活動，這可能會影響資料庫執行期間的效能。  
  
> [!NOTE]  
>  建議您只在必要時和一般作業時間以外執行這項作業。  
  
只能在不同的容器或不同的資料庫上同時執行此預存程序的多個引動過程。  

因為 2 階段作業，預存程序應執行兩次，實際上會刪除基礎 Filestream 檔案。  

記憶體回收 (GC) 會依賴截斷記錄。 因此，如果使用完整復原模式在資料庫上最近刪除的檔案，它們是 GC ed 之後才會從這些交易記錄部分的記錄備份的記錄部分標示為非作用中。 在資料庫上使用簡單復原模式，記錄截斷就會發生之後`CHECKPOINT`已針對資料庫發出。  


## <a name="permissions"></a>Permissions  
 需要 db_owner 資料庫角色中的成員資格。  
  
## <a name="examples"></a>範例  
 下列範例會針對 `FSDB` 資料庫中的 FILESTREAM 容器執行記憶體回收行程。  
  
### <a name="a-specifying-no-container"></a>A. 未指定容器  
  
```sql  
USE FSDB;  
GO  
EXEC sp_filestream_force_garbage_collection @dbname = N'FSDB';  
```  
  
### <a name="b-specifying-a-container"></a>B. 指定容器  
  
```sql  
USE FSDB;  
GO  
EXEC sp_filestream_force_garbage_collection @dbname = N'FSDB',
    @filename = N'FSContainer';  
```  
  
## <a name="see-also"></a>另請參閱  
[Filestream](../../relational-databases/blob/filestream-sql-server.md)
<br>[Filetable](../../relational-databases/blob/filetables-sql-server.md)
<br>[Filestream 和 FileTable 動態管理檢視 (TRANSACT-SQL)](../system-dynamic-management-views/filestream-and-filetable-dynamic-management-views-transact-sql.md)
<br>[Filestream 和 FileTable 目錄檢視 (TRANSACT-SQL)](../system-catalog-views/filestream-and-filetable-catalog-views-transact-sql.md)
<br>[sp_kill_filestream_non_transacted_handles (TRANSACT-SQL)](filestream-and-filetable-sp-kill-filestream-non-transacted-handles.md)
  
  
