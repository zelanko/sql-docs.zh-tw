---
title: "OBJECT_SCHEMA_NAME (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- OBJECT_SCHEMA_NAME
- OBJECT_SCHEMA_NAME_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- objects [SQL Server], names
- schemas [SQL Server], names
- displaying schema names
- database objects [SQL Server], names
- OBJECT_SCHEMA_NAME function
ms.assetid: 5ba90bb9-d045-4164-963e-e9e96c0b1e8b
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: aba132353ef5ff75f8968957cb9e98f8c9e1ce45
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="objectschemaname-transact-sql"></a>OBJECT_SCHEMA_NAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回結構描述範圍物件的資料庫結構描述名稱。 如需結構描述範圍物件的清單，請參閱[sys.objects &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md).  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
OBJECT_SCHEMA_NAME ( object_id [, database_id ] )  
```  
  
## <a name="arguments"></a>引數  
 *object_id*  
 這是所要使用的物件識別碼。 *object_id*是**int**和假設為指定的資料庫，或目前資料庫內容中的結構描述範圍物件。  
  
 *database_id*  
 這是要在其中查閱物件之資料庫的識別碼。 *database_id*是**int**。  
  
## <a name="return-types"></a>傳回類型  
 **sysname**  
  
## <a name="exceptions"></a>例外狀況  
 當發生錯誤，或呼叫端沒有檢視物件的權限時，便會傳回 NULL。 如果目標資料庫將 AUTO_CLOSE 選項設為 ON，函數會開啟資料庫。  
  
 使用者只能檢視使用者擁有或被授與某些權限之安全性實體的中繼資料。 這表示發出中繼資料的內建函數 (例如 OBJECT_SCHEMA_NAME) 會在使用者不具有該物件任何權限時傳回 NULL。 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="permissions"></a>Permissions  
 需要物件的 ANY 權限。 若要指定資料庫識別碼，也需要資料庫的 CONNECT 權限，或必須啟用 Guest 帳戶。  
  
## <a name="remarks"></a>備註  
 系統函數可以用於選取清單、WHERE 子句以及任何可以使用運算式的位置。 如需詳細資訊，請參閱[運算式](../../t-sql/language-elements/expressions-transact-sql.md)和[其中](../../t-sql/queries/where-transact-sql.md)。  
  
 這個系統函數傳回的結果集會使用目前資料庫的定序。  
  
 如果*database_id*未指定，[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]假設*object_id*位於目前資料庫的內容。 參考的查詢*object_id*在另一個資料庫中會傳回 NULL 或不正確的結果。 例如，在下列查詢中，目前資料庫內容便是 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 會嘗試傳回這個資料庫 (而不是查詢之 FROM 子句中所指定的資料庫) 中指定之物件識別碼的物件結構描述名稱。 因此，會傳回不正確的資訊。  
  
```  
SELECT DISTINCT OBJECT_SCHEMA_NAME(object_id)  
FROM master.sys.objects;  
  
```  
  
 下列範例會在 `master` 中指定 `OBJECT_SCHEMA_NAME` 資料庫的資料庫識別碼，並傳回正確的結果。  
  
```  
SELECT DISTINCT OBJECT_SCHEMA_NAME(object_id, 1) AS schema_name  
FROM master.sys.objects;  
  
```  
  
## <a name="examples"></a>範例  
  
### <a name="a-returning-the-object-schema-name-and-object-name"></a>A. 傳回物件結構描述名稱和物件名稱  
 下列範例會針對不是特定或準備陳述式的所有快取查詢計畫，傳回物件結構描述名稱、物件名稱和 SQL 文字。  
  
```  
SELECT DB_NAME(st.dbid) AS database_name,   
    OBJECT_SCHEMA_NAME(st.objectid, st.dbid) AS schema_name,  
    OBJECT_NAME(st.objectid, st.dbid) AS object_name,   
    st.text AS query_statement  
FROM sys.dm_exec_query_stats AS qs  
CROSS APPLY sys.dm_exec_sql_text(qs.sql_handle) AS st  
WHERE st.objectid IS NOT NULL;  
GO  
```  
  
### <a name="b-returning-three-part-object-names"></a>B. 傳回三部分物件名稱  
 下列範例會針對所有資料庫中的所有物件，傳回資料庫、結構描述和物件名稱，以及 `sys.dm_db_index_operational_stats` 動態管理檢視中的所有其他資料行。  
  
```  
SELECT QUOTENAME(DB_NAME(database_id))   
    + N'.'   
    + QUOTENAME(OBJECT_SCHEMA_NAME(object_id, database_id))   
    + N'.'   
    + QUOTENAME(OBJECT_NAME(object_id, database_id))  
    , *   
FROM sys.dm_db_index_operational_stats(null, null, null, null);  
GO  
```  
  
## <a name="see-also"></a>請參閱＜  
 [中繼資料函數 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [OBJECT_DEFINITION &#40;Transact-SQL&#41;](../../t-sql/functions/object-definition-transact-sql.md)   
 [OBJECT_ID &#40;TRANSACT-SQL &#41;](../../t-sql/functions/object-id-transact-sql.md)   
 [OBJECT_NAME &#40;TRANSACT-SQL &#41;](../../t-sql/functions/object-name-transact-sql.md)   
 [安全性實體](../../relational-databases/security/securables.md)  
  
  
