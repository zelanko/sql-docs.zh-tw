---
title: sp_kill_filestream_non_transacted_handles （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_kill_filestream_non_transacted_handles_TSQL
- sp_kill_filestream_non_transacted_handles
dev_langs:
- TSQL
helpviewer_keywords:
- sp_kill_filestream_non_transacted_handles
ms.assetid: 7188353e-ab29-49a0-8f25-7fb8ab122589
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: c26cfb617809c3e7019e279a8da06a4008d08abb
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85717412"
---
# <a name="sp_kill_filestream_non_transacted_handles-transact-sql"></a>sp_kill_filestream_non_transacted_handles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  關閉 FileTable 資料的非交易式檔案控制代碼。  
  
## <a name="syntax"></a>語法  
  
```sql  
sp_kill_filestream_non_transacted_handles [[ @table_name = ] 'table_name', [[ @handle_id = ] @handle_id]]  
```  
  
## <a name="arguments"></a>引數  
 *table_name*  
 關閉非交易式控制代碼所在之資料表的名稱。  
  
 您可以在沒有*handle_id*的情況下傳遞*table_name* ，以關閉 FileTable 的所有開啟的非交易式控制碼。  
  
 您可以傳遞 Null 做為*table_name*的值，以關閉目前資料庫中所有 filetable 的所有開啟的非交易式控制碼。 NULL 是預設值。  
  
 *handle_id*  
 要關閉之個別控制代碼的選擇性識別碼。 您可以從[dm_filestream_non_transacted_handles &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-filestream-non-transacted-handles-transact-sql.md)動態管理檢視中取得*handle_id* 。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體中，每個識別碼都是唯一的。 如果您指定*handle_id*，則也必須提供*table_name*的值。  
  
 您可以傳遞 Null 做為*handle_id*的值，以關閉*table_name*所指定之 FileTable 的所有開啟的非交易式控制碼。 NULL 是預設值。  
  
## <a name="return-code-value"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="result-set"></a>結果集  
 無。  
  
## <a name="general-remarks"></a>一般備註  
 **Sp_kill_filestream_non_transacted_handles**所需的*handle_id*與其他**kill**命令中使用的 session_id 或工作單位無關。  
  
 如需詳細資訊，請參閱 [管理作業步驟](../../relational-databases/blob/manage-filetables.md)。  
  
## <a name="metadata"></a>中繼資料  
 如需開啟非交易式檔案控制代碼的相關資訊，請查詢動態管理檢視[sys.databases dm_filestream_non_transacted_handles &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-filestream-non-transacted-handles-transact-sql.md)。  
  
## <a name="security"></a>安全性  
  
### <a name="permissions"></a>權限  
 您必須具有**VIEW DATABASE STATE**許可權，才能從**sys. dm_FILESTREAM_non_transacted_handles**動態管理檢視取得檔案控制代碼，以及執行**sp_kill_filestream_non_transacted_handles**。  
  
## <a name="examples"></a>範例  
 下列範例示範如何呼叫**sp_kill_filestream_non_transacted_handles** ，以關閉 FileTable 資料的非交易式檔案控制代碼。  
  
```sql  
-- Close all open handles in the current database.  
sp_kill_filestream_non_transacted_handles  
  
-- Close all open handles in myFileTable.  
sp_kill_filestream_non_transacted_handles @table_name = 'myFileTable'  
  
-- Close a specific handle in myFileTable.  
sp_kill_filestream_non_transacted_handles @table_name = 'myFileTable', @handle_id = 0xFFFAAADD  
```  
  
 下列範例顯示如何使用腳本來取得*handle_id*並將它關閉。  
  
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
 [Filestream 和 FileTable 動態管理 Views （Transact-sql）](../system-dynamic-management-views/filestream-and-filetable-dynamic-management-views-transact-sql.md)
 <br>[Filestream 和 FileTable 目錄檢視（Transact-sql）](../system-catalog-views/filestream-and-filetable-catalog-views-transact-sql.md)
 <br>[sp_filestream_force_garbage_collection (Transact-SQL)](filestream-and-filetable-sp-filestream-force-garbage-collection.md)
  
