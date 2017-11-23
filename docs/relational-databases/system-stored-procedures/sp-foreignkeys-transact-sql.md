---
title: "sp_foreignkeys (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_foreignkeys_TSQL
- sp_foreignkeys
dev_langs: TSQL
helpviewer_keywords: sp_foreignkeys
ms.assetid: 935fe385-19ff-41a4-8d0b-30618966991d
caps.latest.revision: "39"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 41b391d4e445df9cb62434013db8b9433e8d4f13
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="spforeignkeys-transact-sql"></a>sp_foreignkeys (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回外部索引鍵，這個外部索引鍵參考連結伺服器中之資料表上的主索引鍵。  
  
||  
|-|  
|**適用於**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [目前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658))。|  
  
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
 [  **@table_server =** ] **'***table_server***'**  
 這是傳回資料表資訊所屬的連結伺服器名稱。 *table_server*是**sysname**，沒有預設值。  
  
 [  **@pktab_name =** ] **'***pktab_name***'**  
 這是含主索引鍵的資料表名稱。 *pktab_name*是**sysname**，預設值是 NULL。  
  
 [  **@pktab_schema =** ] **'***pktab_schema***'**  
 這是含主索引鍵的結構描述名稱。 *pktab_schema*是**sysname**，預設值是 NULL。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，這包含擁有者名稱。  
  
 [  **@pktab_catalog =** ] **'***pktab_catalog***'**  
 這是含主索引鍵的目錄名稱。 *pktab_catalog*是**sysname**，預設值是 NULL。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，這包含資料庫名稱。  
  
 [  **@fktab_name =** ] **'***fktab_name***'**  
 這是含外部索引鍵的資料表名稱。 *fktab_name*是**sysname**，預設值是 NULL。  
  
 [  **@fktab_schema =** ] **'***fktab_schema***'**  
 這是含外部索引鍵的結構描述名稱。 *fktab_schema*是**sysname**，預設值是 NULL。  
  
 [  **@fktab_catalog =** ] **'***fktab_catalog***'**  
 這是含外部索引鍵的目錄名稱。 *fktab_catalog*是**sysname**，預設值是 NULL。  
  
## <a name="return-code-values"></a>傳回碼值  
 無  
  
## <a name="result-sets"></a>結果集  
 各種 DBMS 產品都支援三部分的資料表命名 (*目錄***。***結構描述***。***資料表*)，它會呈現在結果集中。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**PKTABLE_CAT**|**sysname**|主索引鍵所在之資料表的目錄。|  
|**PKTABLE_SCHEM**|**sysname**|主索引鍵所在之資料表的結構描述。|  
|**B L E _**|**sysname**|資料表 (含主索引鍵) 的名稱。 這個欄位一律會傳回值。|  
|**PKCOLUMN_NAME**|**sysname**|主索引鍵資料行或資料行，每個資料行名稱的**TABLE_NAME**傳回。 這個欄位一律會傳回值。|  
|**FKTABLE_CAT**|**sysname**|外部索引鍵所在之資料表的目錄。|  
|**FKTABLE_SCHEM**|**sysname**|外部索引鍵所在之資料表的結構描述。|  
|**B L E _**|**sysname**|資料表 (含外部索引鍵) 的名稱。 這個欄位一律會傳回值。|  
|**FKCOLUMN_NAME**|**sysname**|針對傳回之 TABLE_NAME 的每個資料行而言，這是外部索引鍵資料行的名稱。 這個欄位一律會傳回值。|  
|**KEY_SEQ 來排序**|**smallint**|資料行在多重資料行主索引鍵中的序號。 這個欄位一律會傳回值。|  
|**UPDATE_RULE**|**smallint**|當 SQL 作業是更新時，外部索引鍵所套用的動作。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會針對這些資料行傳回 0、1 或 2：<br /><br /> 0=外部索引鍵的 CASCADE 變更。<br /><br /> 1=如果外部索引鍵存在，則是 NO ACTION 變更。<br /><br /> 2=SET_NULL；將外部索引鍵設為 NULL。|  
|**DELETE_RULE**|**smallint**|當 SQL 作業是刪除時，外部索引鍵所套用的動作。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會針對這些資料行傳回 0、1 或 2：<br /><br /> 0=外部索引鍵的 CASCADE 變更。<br /><br /> 1=如果外部索引鍵存在，則是 NO ACTION 變更。<br /><br /> 2=SET_NULL；將外部索引鍵設為 NULL。|  
|**FK_NAME**|**sysname**|外部索引鍵識別碼。 如果不適用於資料來源的話，它便是 NULL。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會傳回 FOREIGN KEY 條件約束名稱。|  
|**PK_NAME**|**sysname**|主索引鍵識別碼。 如果不適用於資料來源的話，它便是 NULL。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會傳回 PRIMARY KEY 條件約束名稱。|  
|**延遲性**|**smallint**|指出條件約束檢查是否可以延後。|  
  
 在結果集中，FK_NAME 和 PK_NAME 資料行一律傳回 NULL。  
  
## <a name="remarks"></a>備註  
 **sp_foreignkeys**查詢的 FOREIGN_KEYS 資料列集**IDBSchemaRowset**對應至 OLE DB 提供者介面*table_server*。 *Table_name*， *table_schema*， *table_catalog 排列*，和*資料行*參數傳遞給這個介面來限制的資料列傳回。  
  
## <a name="permissions"></a>Permissions  
 需要結構描述的 SELECT 權限。  
  
## <a name="examples"></a>範例  
 下列範例會傳回有關連結伺服器 `Department` 之 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫中 `Seattle1` 資料表的外部索引鍵資訊。  
  
```  
EXEC sp_foreignkeys @table_server = N'Seattle1',   
   @pktab_name = N'Department',   
   @pktab_catalog = N'AdventureWorks2012';  
```  
  
## <a name="see-also"></a>請參閱＜  
 [sp_catalogs &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-catalogs-transact-sql.md)   
 [sp_column_privileges &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-column-privileges-transact-sql.md)   
 [< sp_indexes &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-indexes-transact-sql.md)   
 [sp_linkedservers &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-linkedservers-transact-sql.md)   
 [sp_primarykeys &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-primarykeys-transact-sql.md)   
 [sp_tables_ex &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-tables-ex-transact-sql.md)   
 [sp_table_privileges &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-table-privileges-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
