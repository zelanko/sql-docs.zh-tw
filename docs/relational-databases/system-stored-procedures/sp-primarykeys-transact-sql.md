---
title: sp_primarykeys （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_primarykeys_TSQL
- sp_primarykeys
dev_langs:
- TSQL
helpviewer_keywords:
- sp_primarykeys
ms.assetid: 0f76dd31-5b7b-4209-9e2e-b9ed5cac164d
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b7b4abd30b4fb62a6f9983fc0dd12348cca52467
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82830958"
---
# <a name="sp_primarykeys-transact-sql"></a>sp_primarykeys (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回指定的遠端資料表之主索引鍵資料行，每個索引鍵資料行一個資料列。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_primarykeys [ @table_server = ] 'table_server'   
     [ , [ @table_name = ] 'table_name' ]   
     [ , [ @table_schema = ] 'table_schema' ]   
     [ , [ @table_catalog = ] 'table_catalog' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @table_server = ] 'table_server'_`這是傳回主鍵資訊的連結伺服器名稱。 *table_server*是**sysname**，沒有預設值。  
  
`[ @table_name = ] 'table_name'`這是要提供主鍵資訊的資料表名稱。 *table_name*是**sysname**，預設值是 Null。  
  
`[ @table_schema = ] 'table_schema'`這是資料表架構。 *table_schema*是**sysname**，預設值是 Null。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 環境中，這相當於資料表擁有者。  
  
`[ @table_catalog = ] 'table_catalog'`這是指定之*table_name*所在的目錄名稱。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 環境中，這相當於資料庫名稱。 *table_catalog*是**sysname**，預設值是 Null。  
  
## <a name="return-code-values"></a>傳回碼值  
 無  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**TABLE_CAT**|**sysname**|資料表目錄。|  
|**TABLE_SCHEM**|**sysname**|資料表結構描述。|  
|**TABLE_NAME**|**sysname**|資料表的名稱。|  
|**COLUMN_NAME**|**sysname**|資料行的名稱。|  
|**KEY_SEQ**|**int**|資料行在多重資料行主索引鍵中的序號。|  
|**PK_NAME**|**sysname**|主索引鍵識別碼。 如果不適用於資料來源，便傳回 NULL。|  
  
## <a name="remarks"></a>備註  
 **sp_primarykeys**是藉由查詢對應至*table_server*之 OLE DB 提供者之**IDBSchemaRowset**介面的 PRIMARY_KEYS 資料列集來執行。 *Table_name*、 *table_schema*、 *table_catalog*和資料行參數會傳遞至這個介面，以限制傳回的資料*列*。  
  
 如果指定連結伺服器的 OLE DB 提供者不支援**IDBSchemaRowset**介面的 PRIMARY_KEYS 資料列集， **sp_primarykeys**會傳回空的結果集。  
  
## <a name="permissions"></a>權限  
 需要結構描述的 SELECT 權限。  
  
## <a name="examples"></a>範例  
 下列範例會從 `LONDON1` 伺服器，傳回 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫中 `HumanResources.JobCandidate` 資料表的主索引鍵資料行。  
  
```  
EXEC sp_primarykeys @table_server = N'LONDON1',   
   @table_name = N'JobCandidate',  
   @table_catalog = N'AdventureWorks2012',   
   @table_schema = N'HumanResources';  
```  
  
## <a name="see-also"></a>另請參閱  
 [分散式查詢預存程式 &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/distributed-queries-stored-procedures-transact-sql.md)   
 [sp_catalogs &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-catalogs-transact-sql.md)   
 [sp_column_privileges &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-column-privileges-transact-sql.md)   
 [sp_foreignkeys &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-foreignkeys-transact-sql.md)   
 [sp_indexes &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-indexes-transact-sql.md)   
 [sp_linkedservers &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-linkedservers-transact-sql.md)   
 [sp_tables_ex &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-tables-ex-transact-sql.md)   
 [sp_table_privileges &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-table-privileges-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
