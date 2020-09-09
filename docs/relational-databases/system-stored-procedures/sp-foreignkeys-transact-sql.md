---
description: sp_foreignkeys (Transact-SQL)
title: sp_foreignkeys (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_foreignkeys_TSQL
- sp_foreignkeys
dev_langs:
- TSQL
helpviewer_keywords:
- sp_foreignkeys
ms.assetid: 935fe385-19ff-41a4-8d0b-30618966991d
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 8a87d51fff7179ece3442e2459d8d2c5a96c8029
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543393"
---
# <a name="sp_foreignkeys-transact-sql"></a>sp_foreignkeys (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  傳回外部索引鍵，這個外部索引鍵參考連結伺服器中之資料表上的主索引鍵。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_foreignkeys [ @table_server = ] 'table_server'   
     [ , [ @pktab_name = ] 'pktab_name' ]   
     [ , [ @pktab_schema = ] 'pktab_schema' ]   
     [ , [ @pktab_catalog = ] 'pktab_catalog' ]   
     [ , [ @fktab_name = ] 'fktab_name' ]   
     [ , [ @fktab_schema = ] 'fktab_schema' ]   
     [ , [ @fktab_catalog = ] 'fktab_catalog' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @table_server = ] 'table_server'` 這是傳回資料表資訊之連結伺服器的名稱。 *table_server* 是 **sysname**，沒有預設值。  
  
`[ @pktab_name = ] 'pktab_name'` 這是具有主鍵的資料表名稱。 *pktab_name* 是 **sysname**，預設值是 Null。  
  
`[ @pktab_schema = ] 'pktab_schema'` 這是具有主鍵的架構名稱。 *pktab_schema*是 **sysname**，預設值是 Null。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，這包含擁有者名稱。  
  
`[ @pktab_catalog = ] 'pktab_catalog'` 這是具有主鍵的目錄名稱。 *pktab_catalog*是 **sysname**，預設值是 Null。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，這包含資料庫名稱。  
  
`[ @fktab_name = ] 'fktab_name'` 這是具有外鍵之資料表的名稱。 *fktab_name*是 **sysname**，預設值是 Null。  
  
`[ @fktab_schema = ] 'fktab_schema'` 這是含外鍵的架構名稱。 *fktab_schema*是 **sysname**，預設值是 Null。  
  
`[ @fktab_catalog = ] 'fktab_catalog'` 這是含外鍵的目錄名稱。 *fktab_catalog*是 **sysname**，預設值是 Null。  
  
## <a name="return-code-values"></a>傳回碼值  
 無  
  
## <a name="result-sets"></a>結果集  
 各種 DBMS 產品可針對 (_目錄_的資料表，支援三部分的命名 **。**_架構_**。**_資料表_) ，在結果集中表示。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**PKTABLE_CAT**|**sysname**|主索引鍵所在之資料表的目錄。|  
|**PKTABLE_SCHEM**|**sysname**|主索引鍵所在之資料表的結構描述。|  
|**PKTABLE_NAME**|**sysname**|資料表 (含主索引鍵) 的名稱。 這個欄位一律會傳回值。|  
|**PKCOLUMN_NAME**|**sysname**|傳回之 **TABLE_NAME** 的每個資料行的主鍵資料行名稱。 這個欄位一律會傳回值。|  
|**FKTABLE_CAT**|**sysname**|外部索引鍵所在之資料表的目錄。|  
|**FKTABLE_SCHEM**|**sysname**|外部索引鍵所在之資料表的結構描述。|  
|**FKTABLE_NAME**|**sysname**|資料表 (含外部索引鍵) 的名稱。 這個欄位一律會傳回值。|  
|**FKCOLUMN_NAME**|**sysname**|針對傳回之 TABLE_NAME 的每個資料行而言，這是外部索引鍵資料行的名稱。 這個欄位一律會傳回值。|  
|**KEY_SEQ**|**smallint**|資料行在多重資料行主索引鍵中的序號。 這個欄位一律會傳回值。|  
|**UPDATE_RULE**|**smallint**|當 SQL 作業是更新時，外部索引鍵所套用的動作。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會針對這些資料行傳回 0、1 或 2：<br /><br /> 0=外部索引鍵的 CASCADE 變更。<br /><br /> 1=如果外部索引鍵存在，則是 NO ACTION 變更。<br /><br /> 2=SET_NULL；將外部索引鍵設為 NULL。|  
|**DELETE_RULE**|**smallint**|當 SQL 作業是刪除時，外部索引鍵所套用的動作。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會針對這些資料行傳回 0、1 或 2：<br /><br /> 0=外部索引鍵的 CASCADE 變更。<br /><br /> 1=如果外部索引鍵存在，則是 NO ACTION 變更。<br /><br /> 2=SET_NULL；將外部索引鍵設為 NULL。|  
|**FK_NAME**|**sysname**|外部索引鍵識別碼。 如果不適用於資料來源的話，它便是 NULL。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會傳回 FOREIGN KEY 條件約束名稱。|  
|**PK_NAME**|**sysname**|主索引鍵識別碼。 如果不適用於資料來源的話，它便是 NULL。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會傳回 PRIMARY KEY 條件約束名稱。|  
|**DEFERRABILITY**|**smallint**|指出條件約束檢查是否可以延後。|  
  
 在結果集中，FK_NAME 和 PK_NAME 資料行一律傳回 NULL。  
  
## <a name="remarks"></a>備註  
 **sp_foreignkeys**查詢對應至*table_server*之 OLE DB 提供者之**IDBSchemaRowset**介面的 FOREIGN_KEYS 資料列集。 *Table_name*、 *table_schema*、 *table_catalog*和資料行參數會傳遞至這個介面，以限制傳回的資料*列*。  
  
## <a name="permissions"></a>權限  
 需要結構描述的 SELECT 權限。  
  
## <a name="examples"></a>範例  
 下列範例會傳回有關連結伺服器 `Department` 之 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫中 `Seattle1` 資料表的外部索引鍵資訊。  
  
```  
EXEC sp_foreignkeys @table_server = N'Seattle1',   
   @pktab_name = N'Department',   
   @pktab_catalog = N'AdventureWorks2012';  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_catalogs &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-catalogs-transact-sql.md)   
 [sp_column_privileges &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-column-privileges-transact-sql.md)   
 [sp_indexes &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-indexes-transact-sql.md)   
 [sp_linkedservers &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-linkedservers-transact-sql.md)   
 [sp_primarykeys &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-primarykeys-transact-sql.md)   
 [sp_tables_ex &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-tables-ex-transact-sql.md)   
 [sp_table_privileges &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-table-privileges-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
