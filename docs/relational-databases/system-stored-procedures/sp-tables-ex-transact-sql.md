---
title: sp_tables_ex (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_tables_ex
- sp_tables_ex_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_tables_ex
ms.assetid: 33755c33-7e1e-4ef7-af14-a9cebb1e2ed4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f034b1247f9865b83077ed11f644d6fdbbc4cecd
ms.sourcegitcommit: 37310da0565c2792aae43b3855bd3948fd13e044
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/18/2018
ms.locfileid: "53589383"
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
 [  **@table_server=** ] **'**_table_server&lt_**'**  
 這是傳回資料表資訊所屬的連結伺服器名稱。 *table_server&lt*已**sysname**，沒有預設值。  
  
 [ **，** [  **@table_name=** ] **'**_table_name_**'**]  
 這是傳回資料類型資訊所屬的資料表名稱。 *table_name*已**sysname**，預設值是 NULL。  
  
 [  **@table_schema=** ] **'**_table_schema_**'**]  
 這是資料表結構描述。 *table_schema*已**sysname**，預設值是 NULL。  
  
 [  **@table_catalog=** ] **'**_table_catalog 排列_**'**  
 在其中的資料庫名稱指定*table_name*所在。 *table_catalog 排列*已**sysname**，預設值是 NULL。  
  
 [  **@table_type=** ] **'**_table_type_**'**  
 這是要傳回的資料表類型。 *table_type*已**sysname**，預設值是 NULL，而且可以有下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**別名**|別名的名稱。|  
|**全域暫存**|全系統所能使用之暫存資料表的名稱。|  
|**本機暫存**|只供目前作業使用之暫存資料表的名稱。|  
|**SYNONYM**|同義字的名稱。|  
|**系統資料表**|系統資料表的名稱。|  
|**系統檢視表**|系統檢視表的名稱。|  
|**TABLE**|使用者資料表的名稱。|  
|**VIEW**|檢視表的名稱。|  
  
 [  **@fUsePattern=** ] **'**_fUsePattern_**'**  
 決定是否將字元 **_**， **%**， **[**，並 **]** 解譯成萬用字元。 有效值是 0 (關閉模式比對) 和 1 (開啟模式比對)。 *fUsePattern*已**元**，預設值是 1。  
  
## <a name="return-code-values"></a>傳回碼值  
 None  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**TABLE_CAT**|**sysname**|資料表限定詞名稱。 各種 DBMS 產品都支援三部分的資料表命名 (_限定詞_**。**_擁有者_**。**_名稱_)。 在  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，這個資料行代表資料庫名稱。 在某些其他產品中，它代表資料表之資料庫環境的伺服器名稱。 這個欄位可以是 NULL。|  
|**再依據 TABLE_SCHEM 排列**|**sysname**|資料表擁有者名稱。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，這個資料行代表建立資料表的資料庫使用者名稱。 這個欄位一律會傳回值。|  
|**TABLE_NAME**|**sysname**|資料表名稱。 這個欄位一律會傳回值。|  
|**TABLE_TYPE**|**varchar(32)**|資料表、系統資料表或檢視表。|  
|**註解**|**varchar(254)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不會傳回這個資料行的值。|  
  
## <a name="remarks"></a>備註  
 **sp_tables_ex**執行查詢的資料表資料列集**IDBSchemaRowset**對應至 OLE DB 提供者介面*table_server&lt*。 *Table_name*， *table_schema*， *table_catalog 排列*，以及*資料行*參數傳遞給這個介面來限制的資料列傳回此項目。  
  
 **sp_tables_ex**會傳回空的結果集，如果指定連結伺服器的 OLE DB 提供者不支援的資料表資料列集**IDBSchemaRowset**介面。  
  
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
 [sp_catalogs &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-catalogs-transact-sql.md)   
 [sp_columns_ex &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-columns-ex-transact-sql.md)   
 [sp_column_privileges &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-column-privileges-transact-sql.md)   
 [sp_foreignkeys &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-foreignkeys-transact-sql.md)   
 [< sp_indexes &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-indexes-transact-sql.md)   
 [sp_linkedservers &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-linkedservers-transact-sql.md)   
 [sp_table_privileges &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-table-privileges-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
