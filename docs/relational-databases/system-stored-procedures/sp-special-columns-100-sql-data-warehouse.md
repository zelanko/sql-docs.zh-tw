---
title: sp_special_columns_100 （SQL 資料倉儲） |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 5774fadc-77cc-46f8-8f9f-a0f9efe95e21
caps.latest.revision: 9
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: f63087431cfca9578d4af19c7a213a08806f97c8
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="spspecialcolumns100-sql-data-warehouse"></a>sp_special_columns_100 （SQL 資料倉儲）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  傳回一組用來唯一識別資料表中某個資料列的最佳資料行。 另外，也傳回交易更新資料列中的任何值時，所自動更新的資料行。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例 &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
sp_special_columns_100 [ @table_name = ] 'table_name'     
     [ , [ @table_owner = ] 'table_owner' ]   
     [ , [ @qualifier = ] 'qualifier' ]   
     [ , [ @col_type = ] 'col_type' ]   
     [ , [ @scope = ] 'scope' ]  
     [ , [ @nullable = ] 'nullable' ]   
     [ , [ @ODBCVer = ] 'ODBCVer' ]   
[ ; ]  
```  
  
## <a name="arguments"></a>引數  
 [ @table_name=] '*table_name*'  
 這是用來傳回目錄資訊的資料表名稱。 *名稱*是**sysname**，沒有預設值。 不支援萬用字元的模式比對。  
  
 [ @table_owner=] '*table_owner*'  
 這是用來傳回目錄資訊之資料表的資料表擁有者。 *擁有者*是**sysname**，預設值是 NULL。 不支援萬用字元的模式比對。 如果*擁有者*未指定，套用基礎 dbms 的預設資料表可見性規則。  
  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，如果目前使用者擁有一份含指定之名稱的資料表，就會傳回該資料表的資料行。 如果*擁有者*未指定目前使用者並未擁有指定的資料表和*名稱*，此程序會尋找指定的資料表*名稱*擁有的資料庫擁有者。 如果資料表存在，就會傳回它的資料行。  
  
 [ @qualifier=] '*限定詞*'  
 這是資料表限定詞的名稱。 *限定詞*是**sysname**，預設值是 NULL。 各種 DBMS 產品都支援三部分的資料表命名 (*q*)。 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，這個資料行代表資料庫名稱。 在某些產品中，它代表資料表之資料庫環境的伺服器名稱。  
  
 [ @col_type=] '*col_type*'  
 這是資料行類型。 *col_type*是**char (**1**)**，預設值是。 類型 R 會傳回最佳資料行或資料行集合，從資料行或資料行擷取值，允許對於指定的任何資料列用來唯一識別資料表。 資料行可以是專為了這個目的而設計的虛擬資料行，也可以是資料表任何唯一索引的一個或多個資料行。 類型 V 會傳回在指定的資料表中 (如果有的話)，當任何交易更新資料列中的任何值時，資料來源所自動更新的一個或多個資料行。  
  
 [ @scope=] '*範圍*'  
 這是 ROWID 的最小必要範圍。 *範圍*是**char (**1**)**，預設值是 t。 範圍 C 指定 ROWID 只有在位於這個資料列時才有效。 範圍 T 指定 ROWID 只對交易有效。  
  
 [ @nullable=] '*可為 null*'  
 這是指特殊資料行是否能夠接受 Null 值。 *可為 null*是**char (**1**)**，預設值是 u。 O 指定不允許 null 值的特殊資料行。 U 指定部分可為 Null 的資料行。  
  
 [ @ODBCVer=] '*ODBCVer*'  
 這是正在使用的 ODBC 版本。 *ODBCVer*是**int (**4**)**，預設值是 2。 這表示 ODBC 2.0 版。 如需有關 ODBC 2.0 版和 ODBC 3.0 版之差異的詳細資訊，請參閱 ODBC 3.0 版的 ODBC SQLSpecialColumns 規格。  
  
## <a name="return-code-values"></a>傳回碼值  
 無  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|SCOPE|**smallint**|資料列識別碼的實際範圍。 可以是 0、1 或 2。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 一律傳回 0。 這個欄位一律會傳回值。<br /><br /> 0 = SQL_SCOPE_CURROW。 只有在定位於資料列時，才能夠確保資料列識別碼有效。 如果有另一項交易更新或刪除這個資料列，後來再利用資料列識別碼來重新選取時，便不會傳回資料列。<br /><br /> 1 = SQL_SCOPE_TRANSACTION。 確保在目前交易的持續時間裡，資料列識別碼有效。<br /><br /> 2 = SQL_SCOPE_SESSION。 確保在工作階段的持續時間裡，資料列識別碼有效 (跨越交易界限)。|  
|COLUMN_NAME|**sysname**|每個資料行的資料行名稱*資料表*傳回。 這個欄位一律會傳回值。|  
|DATA_TYPE|**smallint**|ODBC SQL 資料類型。|  
|TYPE_NAME|**sysname**|資料來源相關的資料型別名稱。例如， **char**， **varchar**， **money**，或**文字**。|  
|PRECISION|**整數**|資料來源之資料行的有效位數。 這個欄位一律會傳回值。|  
|LENGTH|**整數**|長度，以位元組為單位，所需的資料來源，其二進位形式的資料類型，例如 10 **char (**10**)**、 4 的**整數**，和 2 **smallint**.|  
|SCALE|**smallint**|資料來源之資料行的小數位數。 小數位數不適用的資料類型會傳回 NULL。|  
|PSEUDO_COLUMN|**smallint**|指出資料行是否為虛擬資料行。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 一律會傳回 1：<br /><br /> 0 = SQL_PC_UNKNOWN<br /><br /> 1 = SQL_PC_NOT_PSEUDO<br /><br /> 2 = SQL_PC_PSEUDO|  
  
## <a name="remarks"></a>備註  
 sp_special_columns 相當於 ODBC 中的 SQLSpecialColumns。 傳回的結果依 SCOPE 來排序。  
  
## <a name="permissions"></a>Permissions  
 需要結構描述的 SELECT 權限。  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 下列範例會傳回用來唯一識別 `FactFinance` 資料表中資料列之資料行的相關資訊。  
  
```  
-- Uses AdventureWorks  
  
EXEC sp_special_columns_100 @table_name = 'FactFinance';  
```  
  
## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲預存程序](../../relational-databases/system-stored-procedures/sql-data-warehouse-stored-procedures.md)  
  
  

