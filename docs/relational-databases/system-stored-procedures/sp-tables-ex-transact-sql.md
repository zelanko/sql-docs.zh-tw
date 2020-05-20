---
title: sp_tables_ex （Transact-sql） |Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 5ebb27860d7b7da46680a61486c59de3929117ce
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82834190"
---
# <a name="sp_tables_ex-transact-sql"></a>sp_tables_ex (Transact-SQL)
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
`[ @table_server = ] 'table_server'`這是傳回資料表資訊的連結伺服器名稱。 *table_server*是**sysname**，沒有預設值。  
  
``[ , [ @table_name = ] 'table_name']``這是傳回資料類型資訊的資料表名稱。 *table_name*是**sysname**，預設值是 Null。  
  
`[ @table_schema = ] 'table_schema']`這是資料表架構。 *table_schema*是**sysname**，預設值是 Null。  
  
`[ @table_catalog = ] 'table_catalog'`這是指定之*table_name*所在的資料庫名稱。 *table_catalog*是**sysname**，預設值是 Null。  
  
`[ @table_type = ] 'table_type'`這是要傳回之資料表的類型。 *table_type*是**sysname**，預設值是 Null，而且可以有下列其中一個值。  
  
|值|說明|  
|-----------|-----------------|  
|**鋸齒**|別名的名稱。|  
|**GLOBAL TEMPORARY**|全系統所能使用之暫存資料表的名稱。|  
|**LOCAL TEMPORARY**|只供目前作業使用之暫存資料表的名稱。|  
|**SYNONYM**|同義字的名稱。|  
|**系統資料表**|系統資料表的名稱。|  
|**系統檢視**|系統檢視表的名稱。|  
|**目錄**|使用者資料表的名稱。|  
|**VIEW**|檢視表的名稱。|  
  
`[ @fUsePattern = ] 'fUsePattern'`判斷 **_**、 **%** 、 **[** 和 **]** 字元是否會被視為萬用字元。 有效值是 0 (關閉模式比對) 和 1 (開啟模式比對)。 *fUsePattern*是**bit**，預設值是1。  
  
## <a name="return-code-values"></a>傳回碼值  
 無  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**TABLE_CAT**|**sysname**|資料表限定詞名稱。 各種 DBMS 產品都支援三部分的資料表命名（辨識_符號_**。**_擁有_者 **。**_名稱_）。 在中 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，這個資料行代表資料庫名稱。 在某些其他產品中，它代表資料表之資料庫環境的伺服器名稱。 這個欄位可以是 NULL。|  
|**TABLE_SCHEM**|**sysname**|資料表擁有者名稱。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，這個資料行代表建立資料表的資料庫使用者名稱。 這個欄位一律會傳回值。|  
|**TABLE_NAME**|**sysname**|資料表名稱。 這個欄位一律會傳回值。|  
|**TABLE_TYPE**|**Varchar （32）**|資料表、系統資料表或檢視表。|  
|**備註**|**Varchar （254）**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不會傳回這個資料行的值。|  
  
## <a name="remarks"></a>備註  
 **sp_tables_ex**是藉由查詢對應至*table_server*之 OLE DB 提供者之**IDBSchemaRowset**介面的資料表資料列集來執行。 *Table_name*、 *table_schema*、 *table_catalog*和資料行參數會傳遞至這個介面，以限制傳回的資料*列*。  
  
 如果指定連結伺服器的 OLE DB 提供者不支援**IDBSchemaRowset**介面的資料表資料列集， **sp_tables_ex**會傳回空的結果集。  
  
## <a name="permissions"></a>權限  
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
 [分散式查詢預存程式 &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/distributed-queries-stored-procedures-transact-sql.md)   
 [sp_catalogs &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-catalogs-transact-sql.md)   
 [sp_columns_ex &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-columns-ex-transact-sql.md)   
 [sp_column_privileges &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-column-privileges-transact-sql.md)   
 [sp_foreignkeys &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-foreignkeys-transact-sql.md)   
 [sp_indexes &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-indexes-transact-sql.md)   
 [sp_linkedservers &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-linkedservers-transact-sql.md)   
 [sp_table_privileges &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-table-privileges-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
