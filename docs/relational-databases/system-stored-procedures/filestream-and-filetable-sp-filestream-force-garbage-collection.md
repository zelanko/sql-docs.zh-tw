---
title: sp_filestream_force_garbage_collection （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 07/22/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: cbf1658fd1567d9cdd3c35e02195435b6e86adcc
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82830393"
---
# <a name="sp_filestream_force_garbage_collection-transact-sql"></a>sp_filestream_force_garbage_collection (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  強制執行 FILESTREAM 記憶體回收行程，刪除任何不必要的 FILESTREAM 檔案。  
  
 在 FILESTREAM 容器內所有已刪除的檔案都已經由記憶體回收行程清除之前，無法移除容器。 FILESTREAM 記憶體回收行程會自動執行。 不過，如果您需要在垃圾收集行程執行之前移除容器，您可以使用 sp_filestream_force_garbage_collection 手動執行垃圾收集行程。  
  
  
## <a name="syntax"></a>語法  
  
```  
sp_filestream_force_garbage_collection
    [ @dbname = ]  'database_name'
    [ , [ @filename = ] 'logical_file_name' ]
```  
  
## <a name="arguments"></a>引數  
 `[ @dbname = ]  'database_name'`  
 表示要執行記憶體回收行程之資料庫的名稱。  
  
> [!NOTE]  
> `@dbname` 為 **sysname**。 如果未指定，則假設目前的資料庫。  
  
 `[ @filename = ] 'logical_file_name'`  
 指定要執行記憶體回收行程之 FILESTREAM 容器的邏輯名稱。 `@filename` 是選擇性的。 如果未指定邏輯檔案名，垃圾收集行程就會清除指定之資料庫中的所有 FILESTREAM 容器。  
  
## <a name="return-code-values"></a>傳回碼值  
  
|||  
|-|-|  
|值|說明|  
|0|作業成功|  
|1|作業失敗|  
  
## <a name="result-sets"></a>結果集  
  
|值|說明|  
|-----------|-----------------|  
|*file_name*|指出 FILESTREAM 容器名稱|  
|*num_collected_items*|指出在這個容器中已進行記憶體回收 (已刪除) 的 FILESTREAM 項目 (檔案/目錄) 的數目。|  
|*num_marked_for_collection_items*|指出在這個容器中已標示為記憶體回收的 FILESTREAM 項目 (檔案/目錄) 的數目。 這些專案尚未刪除，但可能符合垃圾收集階段的刪除資格。|  
|*num_unprocessed_items*|指出在這個 FILESTREAM 容器中適合記憶體回收但未處理的 FILESTREAM 項目 (檔案或目錄) 的數目。 項目可能因各種原因未處理，包括下列：<br /><br /> 因為尚未進行記錄備份或檢查點而需要確定的檔案。<br /><br /> 在 FULL 或 BULK_LOGGED 復原模式中的檔案。<br /><br /> 有長時間執行的使用中交易。<br /><br /> 複寫記錄讀取器工作尚未執行。 如需詳細資訊，請參閱[SQL Server 2008 中的《 FILESTREAM Storage](https://go.microsoft.com/fwlink/?LinkId=209156) 》（技術白皮書）。|  
|*last_collected_xact_seqno*|傳回指定 FILESTREAM 容器中已進行記憶體回收之檔案的最後一個對應記錄序號 (LSN)。|  
  
## <a name="remarks"></a>備註  
 在要求的資料庫 (和 FILESTREAM 容器) 上，明確執行完成 FILESTREAM 記憶體回收行程工作。 記憶體回收處理序會移除不再需要的檔案。 完成此作業的所需時間取決於該資料庫或容器中的 FILESTREAM 資料大小，以及 FILESTREAM 資料上最近發生的資料操作語言 (DML) 活動量。 雖然這項作業可以在資料庫上線時執行，但因為記憶體回收處理序進行各種 I/O 活動，這可能會影響資料庫執行期間的效能。  
  
> [!NOTE]  
>  建議您只在必要時和一般作業時間以外執行這項作業。  
  
只能在不同的容器或不同的資料庫上同時執行此預存程序的多個引動過程。  

由於2個階段的作業，應該執行兩次預存程式，以實際刪除基礎 Filestream 檔案。  

垃圾收集（GC）依賴記錄截斷。 因此，如果最近使用完整復原模式在資料庫上刪除檔案，只有在取得這些交易記錄部分的記錄備份，且記錄部分標示為非作用中時，才會成為 GC。 在使用簡單復原模式的資料庫上，對資料庫發出之後，會發生記錄截斷 `CHECKPOINT` 。  


## <a name="permissions"></a>權限  
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
[檔案資料流](../../relational-databases/blob/filestream-sql-server.md)
<br>[Filetable](../../relational-databases/blob/filetables-sql-server.md)
<br>[Filestream 及 FileTable 動態管理檢視 (Transact-SQL)](../system-dynamic-management-views/filestream-and-filetable-dynamic-management-views-transact-sql.md)
<br>[Filestream 和 FileTable 目錄檢視 (Transact-SQL)](../system-catalog-views/filestream-and-filetable-catalog-views-transact-sql.md)
<br>[sp_kill_filestream_non_transacted_handles (Transact-SQL)](filestream-and-filetable-sp-kill-filestream-non-transacted-handles.md)
  
  
