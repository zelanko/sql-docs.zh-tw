---
title: sp_indexes （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_indexes_TSQL
- sp_indexes
dev_langs:
- TSQL
helpviewer_keywords:
- sp_indexes
ms.assetid: 25469e72-9d95-463f-912a-193471c8f5e2
author: stevestein
ms.author: sstein
ms.openlocfilehash: 625b1b5bca3c76a0433e0b887d2c291a714c6f54
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68139923"
---
# <a name="sp_indexes-transact-sql"></a>sp_indexes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回指定遠端資料表的索引資訊。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_indexes [ @table_server = ] 'table_server'   
     [ , [ @table_name = ] 'table_name' ]   
     [ , [ @table_schema = ] 'table_schema' ]   
     [ , [ @table_catalog = ] 'table_db' ]   
     [ , [ @index_name = ] 'index_name' ]   
     [ , [ @is_unique = ] 'is_unique' ]  
```  
  
## <a name="arguments"></a>引數  
 [ @table_server= ]'*table_server*'  
 這是連結的伺服器名稱，此伺服器執行所要求之資料表資訊所屬的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 *table_server*是**sysname**，沒有預設值。  
  
 [ @table_name= ]'*table_name*'  
 這是要為其提供索引資訊的遠端資料表名稱。 *table_name*是**sysname**，預設值是 Null。 如果是 NULL，便會傳回指定資料庫中的所有資料表。  
  
 [ @table_schema= ]'*table_schema*'  
 指定資料表結構描述。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 環境中，這相當於資料表擁有者。 *table_schema*是**sysname**，預設值是 Null。  
  
 [ @table_catalog= ]'*table_db*'  
 這是*table_name*所在的資料庫名稱。 *table_db*是**sysname**，預設值是 Null。 如果是 Null， *table_db*預設為**master**。  
  
 [ @index_name= ]'*index_name*'  
 這是要求之資訊所屬的索引名稱。 *index*是**sysname**，預設值是 Null。  
  
 [ @is_unique= ]'*is_unique*'  
 這是要傳回資訊的索引類型。 *is_unique*是**bit**，預設值是 Null，它可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|1|傳回唯一索引的相關資訊。|  
|0|傳回不是唯一索引的相關資訊。|  
|NULL|傳回所有索引的相關資訊。|  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|TABLE_CAT|**sysname**|指定資料表所在的資料庫名稱。|  
|TABLE_SCHEM|**sysname**|資料表的結構描述。|  
|TABLE_NAME|**sysname**|遠端資料表的名稱。|  
|NON_UNIQUE|**smallint**|索引是否唯一：<br /><br /> 0 = 唯一<br /><br /> 1 = 不是唯一|  
|INDEX_QUALIFER|**sysname**|索引擁有者的名稱。 部分 DBMS 產品允許資料表擁有者以外的使用者建立索引。 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中，這個資料行一律與**TABLE_NAME**相同。|  
|INDEX_NAME|**sysname**|索引的名稱。|  
|TYPE|**smallint**|索引的類型：<br /><br /> 0 = 資料表的統計資料<br /><br /> 1 = 叢集<br /><br /> 2 = 雜湊<br /><br /> 3 = 其他|  
|ORDINAL_POSITION|**int**|資料行在索引中的序數位置。 索引中的第一個資料行是 1。 這個資料行一律會傳回值。|  
|COLUMN_NAME|**sysname**|這是傳回的 TABLE_NAME 的各個資料行之對應資料行名稱。|  
|ASC_OR_DESC|**varchar**|這是定序所用的順序：<br /><br /> A = 遞增<br /><br /> D = 遞減<br /><br /> NULL = 不適用<br /><br /> 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 一律傳回 A。|  
|CARDINALITY|**int**|這是資料表中的資料列數，或索引中的唯一值數目。|  
|PAGES|**int**|這是用來儲存索引或資料表的頁數。|  
|FILTER_CONDITION|**Nvarchar （** 4000 **）**|
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不會傳回值。|  
  
## <a name="permissions"></a>權限  
 需要結構描述的 SELECT 權限。  
  
## <a name="examples"></a>範例  
 下列範例會從 `Employees` 連結伺服器 `AdventureWorks2012` 資料庫之 `Seattle1` 資料表中，傳回所有索引資訊。  
  
```  
EXEC sp_indexes @table_server = 'Seattle1',   
   @table_name = 'Employee',   
   @table_schema = 'HumanResources',  
   @table_catalog = 'AdventureWorks2012';  
```  
  
## <a name="see-also"></a>另請參閱  
 [分散式查詢預存程式 &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/distributed-queries-stored-procedures-transact-sql.md)   
 [sp_catalogs &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-catalogs-transact-sql.md)   
 [sp_column_privileges &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-column-privileges-transact-sql.md)   
 [sp_foreignkeys &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-foreignkeys-transact-sql.md)   
 [sp_linkedservers &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-linkedservers-transact-sql.md)   
 [sp_tables_ex &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-tables-ex-transact-sql.md)   
 [sp_table_privileges &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-table-privileges-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
