---
description: sp_pkeys (Transact-SQL)
title: sp_pkeys (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_pkeys
- sp_pkeys_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_pkeys
ms.assetid: e614c75d-847b-4726-8f6f-cd18de688eda
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6a55bcdd0df9f288daa22c5f4f1454b14305ec6a
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97478939"
---
# <a name="sp_pkeys-transact-sql"></a>sp_pkeys (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  傳回目前環境中單一資料表的主索引鍵資訊。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```syntaxsql  
-- Syntax for SQL Server, Azure SQL Database, Azure Synapse Analytics, Parallel Data Warehouse  
  
sp_pkeys [ @table_name = ] 'name'       
    [ , [ @table_owner = ] 'owner' ]   
    [ , [ @table_qualifier = ] 'qualifier' ]  
```  
  
## <a name="arguments"></a>引數  
 [ @table_name =] '*name*'  
 這是要傳回信息的資料表。 *名稱* 是 **sysname**，沒有預設值。 不支援萬用字元的模式比對。  
  
 [ @table_owner =] '*owner*'  
 指定已指定資料表的資料表擁有者。 *owner* 是 **sysname**，預設值是 Null。 不支援萬用字元的模式比對。 如果未指定 *owner* ，則適用基礎 DBMS 的預設資料表可見度規則。  
  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，如果目前使用者擁有一份含指定之名稱的資料表，就會傳回該資料表的資料行。 如果未指定 *擁有* 者，且目前的使用者未擁有具有指定 *名稱* 的資料表，這個程式就會尋找資料庫擁有者所擁有之指定 *名稱* 的資料表。 如果資料表存在，就會傳回這份資料表的資料行。  
  
 [ @table_qualifier =] '*限定詞*'  
 這是資料表限定詞。 *限定詞* 是 **sysname**，預設值是 Null。 各種 DBMS 產品都支援資料表 (辨識 _符號_ 的三部分命名 **。**_擁有_ 者 **。**) _名稱_。 在中 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，這個資料行代表資料庫名稱。 在某些產品中，它代表資料表之資料庫環境的伺服器名稱。  
  
## <a name="return-code-values"></a>傳回碼值  
 無  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|TABLE_QUALIFIER|**sysname**|資料表限定詞的名稱。 這個欄位可以是 NULL。|  
|TABLE_OWNER|**sysname**|資料表擁有者的名稱。 這個欄位一律會傳回值。|  
|TABLE_NAME|**sysname**|資料表的名稱。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，這個資料行代表符合 sysobjects 資料表所列出的資料表名稱。 這個欄位一律會傳回值。|  
|COLUMN_NAME|**sysname**|傳回的 TABLE_NAME 之各個資料行的資料行名稱。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，這個資料行代表符合 sys.columns 資料表所列出的資料行名稱。 這個欄位一律會傳回值。|  
|KEY_SEQ|**smallint**|資料行在多重資料行主索引鍵中的序號。|  
|PK_NAME|**sysname**|主索引鍵識別碼。 如果不適用於資料來源，便傳回 NULL。|  
  
## <a name="remarks"></a>備註  
 sp_pkeys 會傳回 PRIMARY KEY 條件約束所明確定義之資料行的相關資訊。 由於不是所有系統都支援明確具名的主索引鍵，因此，閘道實作者會判斷主索引鍵的構成要素。 請注意，主索引鍵一詞是指資料表的邏輯主索引鍵。 依照預期，列為邏輯主索引鍵的每個索引鍵都會定義一個唯一索引。 sp_statistics 也會傳回這個唯一索引。  
  
 sp_pkeys 預存程序相當於 ODBC 中的 SQLPrimaryKeys。 傳回的結果依 TABLE_QUALIFIER、TABLE_OWNER、TABLE_NAME 和 KEY_SEQ 來排序。  
  
## <a name="permissions"></a>權限  
 需要結構描述的 SELECT 權限。  
  
## <a name="examples"></a>範例  
 下列範例會擷取 `HumanResources.Department` 資料庫之 `AdventureWorks2012` 資料表的主索引鍵。  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_pkeys @table_name = N'Department'  
    ,@table_owner = N'HumanResources';  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 下列範例會擷取 `DimAccount` 資料庫之 `AdventureWorksPDW2012` 資料表的主索引鍵。 它會傳回零個數據列，表示資料表沒有主鍵。  
  
```sql  
-- Uses AdventureWorks  
  
EXEC sp_pkeys @table_name = N'DimAccount';  
```  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的目錄預存程式 ](../../relational-databases/system-stored-procedures/catalog-stored-procedures-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

