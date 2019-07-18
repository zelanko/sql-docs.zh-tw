---
title: OBJECT_NAME (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- OBJECT_NAME
- OBJECT_NAME_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- OBJECT_NAME function
- viewing database object names
- objects [SQL Server], names
- database objects [SQL Server], names
- displaying database object names
- database objects [SQL Server]
- names [SQL Server], database objects
ms.assetid: 7d5b923f-0c3e-4af9-b39b-132807a6d5b3
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1f27628a944c8df1d27bf05f9eb5fbade28aa30b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65948990"
---
# <a name="objectname-transact-sql"></a>OBJECT_NAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  傳回結構描述範圍物件的資料庫物件名稱。 如需結構描述範圍物件的清單，請參閱 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
OBJECT_NAME ( object_id [, database_id ] )  
```  
  
## <a name="arguments"></a>引數  
 *object_id*  
 這是所要使用的物件識別碼。 *object_id* 為 **int**，而且會假設為指定資料庫或目前資料庫內容中的結構描述範圍物件。  
  
 *database_id*  
 這是要在其中查閱物件之資料庫的識別碼。 *database_id* 為 **int**。  
  
## <a name="return-types"></a>傳回類型  
 **sysname**  
  
## <a name="exceptions"></a>例外狀況  
 當發生錯誤，或呼叫端沒有檢視物件的權限時，便會傳回 NULL。 如果目標資料庫將 AUTO_CLOSE 選項設為 ON，函數會開啟資料庫。  
  
 使用者只能檢視使用者擁有或被授與某些權限之安全性實體的中繼資料。 這表示發出中繼資料的內建函數 (例如，OBJECT_NAME) 會在使用者不具有該物件任何權限時傳回 NULL。 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="permissions"></a>權限  
 需要物件的 ANY 權限。 若要指定資料庫識別碼，也需要資料庫的 CONNECT 權限，或必須啟用 Guest 帳戶。  
  
## <a name="remarks"></a>Remarks  
 系統函數可以用於選取清單、WHERE 子句以及任何可以使用運算式的位置。 如需詳細資訊，請參閱[運算式](../../t-sql/language-elements/expressions-transact-sql.md) 及 [WHERE](../../t-sql/queries/where-transact-sql.md)。  
  
 這個系統函數傳回的值會使用目前資料庫的定序。  
  
 根據預設，[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 會假設 *object_id* 在目前資料庫的內容中。 參考另一資料庫中之 *object_id* 的查詢會傳回 NULL 或不正確的結果。 例如，在下列查詢中，目前資料庫內容便是 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 會嘗試傳回這個資料庫 (而不是查詢之 FROM 子句中所指定的資料庫) 中指定之物件識別碼的物件名稱。 因此，會傳回不正確的資訊。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT DISTINCT OBJECT_NAME(object_id)  
FROM master.sys.objects;  
GO  
```  
  
 您可以指定資料庫識別碼，在另一個資料庫的內容中解析物件名稱。 下列範例會在 `master` 中指定 `OBJECT_SCHEMA_NAME` 資料庫的資料庫識別碼，並傳回正確的結果。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT DISTINCT OBJECT_SCHEMA_NAME(object_id, 1) AS schema_name  
FROM master.sys.objects;  
GO  
```  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-objectname-in-a-where-clause"></a>A. 在 WHERE 子句中使用 OBJECT_NAME  
 下列範例會從 `sys.objects` 目錄檢視中，傳回 `OBJECT_NAME` 陳述式 `WHERE` 子句中的 `SELECT` 所指定之物件的資料行。  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @MyID int;  
SET @MyID = (SELECT OBJECT_ID('AdventureWorks2012.Production.Product',  
    'U'));  
SELECT name, object_id, type_desc  
FROM sys.objects  
WHERE name = OBJECT_NAME(@MyID);  
GO  
```  
  
### <a name="b-returning-the-object-schema-name-and-object-name"></a>B. 傳回物件結構描述名稱和物件名稱  
 下列範例會針對不是特定或準備陳述式的所有快取查詢計畫，傳回物件結構描述名稱、物件名稱和 SQL 文字。  
  
```  
SELECT DB_NAME(st.dbid) AS database_name,   
    OBJECT_SCHEMA_NAME(st.objectid, st.dbid) AS schema_name,  
    OBJECT_NAME(st.objectid, st.dbid) AS object_name,   
    st.text AS query_text  
FROM sys.dm_exec_query_stats AS qs  
CROSS APPLY sys.dm_exec_sql_text(qs.sql_handle) AS st  
WHERE st.objectid IS NOT NULL;  
GO  
```  
  
### <a name="c-returning-three-part-object-names"></a>C. 傳回三部分物件名稱  
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
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-using-objectname-in-a-where-clause"></a>D. 在 WHERE 子句中使用 OBJECT_NAME  
 下列範例會從 `sys.objects` 目錄檢視中，傳回 `OBJECT_NAME` 陳述式 `WHERE` 子句中的 `SELECT` 所指定之物件的資料行。 (您的物件數目 (下列範例中為 274100017) 會不同。  若要測試此範例，請藉由在您的資料庫中執行 `SELECT name, object_id FROM sys.objects;` 來查看有效物件的數目。)  
  
```  
SELECT name, object_id, type_desc  
FROM sys.objects  
WHERE name = OBJECT_NAME(274100017);  
```  
  
## <a name="see-also"></a>另請參閱  
 [中繼資料函數 &#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [OBJECT_DEFINITION &#40;Transact-SQL&#41;](../../t-sql/functions/object-definition-transact-sql.md)   
 [OBJECT_ID &#40;Transact-SQL&#41;](../../t-sql/functions/object-id-transact-sql.md)  
  
  

