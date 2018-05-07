---
title: sp_kill_filestream_non_transacted_handles (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_kill_filestream_non_transacted_handles_TSQL
- sp_kill_filestream_non_transacted_handles
dev_langs:
- TSQL
helpviewer_keywords:
- sp_kill_filestream_non_transacted_handles
ms.assetid: 7188353e-ab29-49a0-8f25-7fb8ab122589
caps.latest.revision: 13
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: de6599caa4881800063a47d6adb25651a4c92f2c
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="spkillfilestreamnontransactedhandles-transact-sql"></a>sp_kill_filestream_non_transacted_handles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  關閉 FileTable 資料的非交易式檔案控制代碼。  
  
## <a name="syntax"></a>語法  
  
```sql  
sp_kill_filestream_non_transacted_handles [[ @table_name = ] ‘table_name’, [[ @handle_id = ] @handle_id]]  
```  
  
## <a name="arguments"></a>引數  
 *table_name*  
 關閉非交易式控制代碼所在之資料表的名稱。  
  
 您可以傳遞*table_name*沒有*handle_id*關閉所有開啟的非交易式控制代碼的 FileTable。  
  
 您可以傳遞 NULL 值的*table_name*關閉所有開啟的目前資料庫中的所有 Filetable 非交易式控制代碼。 NULL 是預設值。  
  
 *handle_id*  
 要關閉之個別控制代碼的選擇性識別碼。 您可以取得*handle_id*從[sys.dm_filestream_non_transacted_handles &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-filestream-non-transacted-handles-transact-sql.md)動態管理檢視。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體中，每個識別碼都是唯一的。 如果您指定*handle_id*，則也必須提供值給*table_name*。  
  
 您可以傳遞 NULL 值的*handle_id*關閉所有開啟的非交易式控制代碼所指定之 filetable *table_name*。 NULL 是預設值。  
  
## <a name="return-code-value"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="result-set"></a>結果集  
 無。  
  
## <a name="general-remarks"></a>一般備註  
 *Handle_id*所**sp_kill_filestream_non_transacted_handles** session_id 或使用其他的工作單位無關**kill**命令。  
  
 如需詳細資訊，請參閱 [管理作業步驟](../../relational-databases/blob/manage-filetables.md)。  
  
## <a name="metadata"></a>中繼資料  
 如需開啟的非交易式檔案控制代碼，查詢動態管理檢視[sys.dm_filestream_non_transacted_handles &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-filestream-non-transacted-handles-transact-sql.md)。  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>Permissions  
 您必須擁有**VIEW DATABASE STATE**權限，以取得檔案控制代碼，從**sys.dm_FILESTREAM_non_transacted_handles**動態管理檢視以及執行**sp_kill_filestream_non_transacted_handles**。  
  
## <a name="examples"></a>範例  
 下列範例示範如何呼叫**sp_kill_filestream_non_transacted_handles**關閉 FileTable 資料的非交易式檔案控制代碼。  
  
```sql  
-- Close all open handles in the current database.  
sp_kill_filestream_non_transacted_handles  
  
-- Close all open handles in myFileTable.  
sp_kill_filestream_non_transacted_handles @table_name = ’myFileTable’  
  
-- Close a specific handle in myFileTable.  
sp_kill_filestream_non_transacted_handles @table_name = ’myFileTable’, @handle_id = 0xFFFAAADD  
```  
  
 下列範例示範如何使用指令碼來取得*handle_id*並將它關閉。  
  
```sql  
DECLARE @handle_id varbinary(16);  
DECLARE @table_name sysname;  
  
SELECT TOP 1 @handle_id = handle_id, @table_name = Object_name(table_id)  
FROM sys.dm_FILESTREAM_non_transacted_handles;  
  
EXEC sp_kill_filestream_non_transacted_handles @dbname, @table_name, @handle_id;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [管理 FileTable](../../relational-databases/blob/manage-filetables.md)  
 [Filestream 和 FileTable 動態管理檢視 (TRANSACT-SQL)](../system-dynamic-management-views/filestream-and-filetable-dynamic-management-views-transact-sql.md)
 <br>[Filestream 和 FileTable 目錄檢視 (TRANSACT-SQL)](../system-catalog-views/filestream-and-filetable-catalog-views-transact-sql.md)
 <br>[s (TRANSACT-SQL)](filestream-and-filetable-sp-filestream-force-garbage-collection.md)
  
