---
title: sp_tables_ex (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_tables_ex
- sp_tables_ex_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_tables_ex
ms.assetid: 33755c33-7e1e-4ef7-af14-a9cebb1e2ed4
caps.latest.revision: 33
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 6ee56221f4ea21c1b1845d526992e27cf1f42893
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="sptablesex-transact-sql"></a>sp_tables_ex (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回指定之連結伺服器中資料表的資料表相關資訊。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_tables_ex [ @table_server = ] 'table_server'   
     [ , [ @table_name = ] 'table_name' ]   
     [ , [ @table_schema = ] 'table_schema' ]  
     [ , [ @table_catalog = ] 'table_catalog' ]   
     [ , [ @table_type = ] 'table_type' ]   
     [ , [@fUsePattern = ] 'fUsePattern' ]  
```  
  
## <a name="arguments"></a>引數  
 [  **@table_server=** ] **'***table_server***'**  
 這是傳回資料表資訊所屬的連結伺服器名稱。 *table_server*是**sysname**，沒有預設值。  
  
 [ **，** [  **@table_name=** ] **'***table_name***'**]  
 這是傳回資料類型資訊所屬的資料表名稱。 *table_name*是**sysname**，預設值是 NULL。  
  
 [  **@table_schema=** ] **'***table_schema***'**]  
 這是資料表結構描述。 *table_schema*是**sysname**，預設值是 NULL。  
  
 [  **@table_catalog=** ] **'***table_catalog 排列***'**  
 在其中的資料庫名稱指定*table_name*所在。 *table_catalog 排列*是**sysname**，預設值是 NULL。  
  
 [  **@table_type=** ] **'***table_type***'**  
 這是要傳回的資料表類型。 *table_type*是**sysname**，預設值是 NULL，而且可以有下列值之一。  
  
|Value|Description|  
|-----------|-----------------|  
|**別名**|別名的名稱。|  
|**全域暫存**|全系統所能使用之暫存資料表的名稱。|  
|**本機暫存**|只供目前作業使用之暫存資料表的名稱。|  
|**SYNONYM**|同義字的名稱。|  
|**系統資料表**|系統資料表的名稱。|  
|**系統檢視表**|系統檢視表的名稱。|  
|**TABLE**|使用者資料表的名稱。|  
|**VIEW**|檢視表的名稱。|  
  
 [  **@fUsePattern=** ] **'***fUsePattern***'**  
 決定是否字元 **_**， **%**， **[**，和 **]** 解譯成萬用字元。 有效值是 0 (關閉模式比對) 和 1 (開啟模式比對)。 *fUsePattern*是**元**，預設值是 1。  
  
## <a name="return-code-values"></a>傳回碼值  
 無  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**TABLE_CAT**|**sysname**|資料表限定詞名稱。 各種 DBMS 產品都支援三部分的資料表命名 (*限定詞 ***。*** 擁有者 ***。*** 名稱*)。 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，這個資料行代表資料庫名稱。 在某些其他產品中，它代表資料表之資料庫環境的伺服器名稱。 這個欄位可以是 NULL。|  
|**再依據 TABLE_SCHEM 排列**|**sysname**|資料表擁有者名稱。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，這個資料行代表建立資料表的資料庫使用者名稱。 這個欄位一律會傳回值。|  
|**TABLE_NAME**|**sysname**|資料表名稱。 這個欄位一律會傳回值。|  
|**TABLE_TYPE**|**varchar （32)**|資料表、系統資料表或檢視表。|  
|**註解**|**varchar(254)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不會傳回這個資料行的值。|  
  
## <a name="remarks"></a>備註  
 **sp_tables_ex**執行查詢的資料表資料列集**IDBSchemaRowset**相對應的 OLE DB 提供者介面*table_server*。 *Table_name*， *table_schema*， *table_catalog 排列*，和*資料行*參數傳遞給這個介面來限制的資料列傳回。  
  
 **sp_tables_ex**傳回空的結果集，如果指定連結伺服器的 OLE DB 提供者不支援的資料表資料列集中**IDBSchemaRowset**介面。  
  
## <a name="permissions"></a>Permissions  
 需要結構描述的 SELECT 權限。  
  
## <a name="examples"></a>範例  
 下列範例會傳回 `HumanResources` 連結伺服器 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫中的 `LONDON2` 結構描述所包含之資料表的相關資訊。  
  
```  
EXEC sp_tables_ex @table_server = 'LONDON2',   
@table_catalog = 'AdventureWorks2012',   
@table_schema = 'HumanResources',   
@table_type = 'TABLE';  
```  
  
## <a name="see-also"></a>另請參閱  
 [分散式查詢預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/distributed-queries-stored-procedures-transact-sql.md)   
 [sp_catalogs &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-catalogs-transact-sql.md)   
 [sp_columns_ex &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-columns-ex-transact-sql.md)   
 [sp_column_privileges &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-column-privileges-transact-sql.md)   
 [sp_foreignkeys &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-foreignkeys-transact-sql.md)   
 [< sp_indexes &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-indexes-transact-sql.md)   
 [sp_linkedservers & #40;TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-linkedservers-transact-sql.md)   
 [sp_table_privileges &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-table-privileges-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
