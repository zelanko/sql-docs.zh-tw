---
title: sp_statistics (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_statistics_TSQL
- sp_statistics
dev_langs:
- TSQL
helpviewer_keywords:
- sp_statistics
ms.assetid: 0bb6495f-258a-47ec-9f74-fd16671d23b8
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: fdf0984f172657ad45ee6da0a09de5e0e457b003
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63004210"
---
# <a name="spstatistics-transact-sql"></a>sp_statistics (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  傳回指定資料表或索引檢視的所有索引和統計資料的清單。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
sp_statistics [ @table_name = ] 'table_name'    
     [ , [ @table_owner = ] 'owner' ]   
     [ , [ @table_qualifier = ] 'qualifier' ]   
     [ , [ @index_name = ] 'index_name' ]   
     [ , [ @is_unique = ] 'is_unique' ]  
     [ , [ @accuracy = ] 'accuracy' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @table_name = ] 'table_name'` 指定用來傳回目錄資訊的資料表。 *table_name*已**sysname**，沒有預設值。 不支援萬用字元的模式比對。  
  
`[ @table_owner = ] 'owner'` 是用來傳回目錄資訊之資料表的資料表擁有者名稱。 *table_owner*已**sysname**，預設值是 NULL。 不支援萬用字元的模式比對。 如果*擁有者*未指定，套用基礎 dbms 的預設資料表可見性規則。  
  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，如果目前使用者擁有一份含指定名稱的資料表，就會傳回這份資料表的索引。 如果*擁有者*未指定且目前使用者並未擁有指定的資料表*名稱*，此程序會尋找具有指定的資料表*名稱*所擁有資料庫擁有者。 如果資料表存在，就會傳回這份資料表的索引。  
  
`[ @table_qualifier = ] 'qualifier'` 是資料表限定詞的名稱。 *限定詞*已**sysname**，預設值是 NULL。 各種 DBMS 產品都支援三部分的資料表命名 (_限定詞_ **。** _擁有者_ **。** _名稱_)。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，這個參數代表資料庫名稱。 在某些產品中，它代表資料表之資料庫環境的伺服器名稱。  
  
`[ @index_name = ] 'index_name'` 這是索引名稱。 *index_name*已**sysname**，預設值是 %。 支援萬用字元的模式比對。  
  
`[ @is_unique = ] 'is_unique'` 是是否唯一索引 (如果**Y**) 要傳回。 *is_unique*已**char(1)** ，預設值是**N**。  
  
`[ @accuracy = ] 'accuracy'` 是基數和頁面精確度的統計資料的層級。 *精確度*已**char(1)** ，預設值是**Q**。指定**E**以確定會更新統計資料，以便基數和頁面都精確。  
  
 該值**E** (SQL_ENSURE) 會要求驅動程式無條件地擷取統計資料。  
  
 該值**Q** (SQL_QUICK) 會要求驅動程式擷取基數和頁面才可以從伺服器提供。 在這個情況下，驅動程式無法確保這些值是否為最新的。 撰寫成 Open Group 標準的應用程式，永遠會透過 ODBC 3.x 相容的驅動程式取得 SQL_QUICK 行為。  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**TABLE_QUALIFIER**|**sysname**|資料表限定詞名稱。 這個資料行可以是 NULL。|  
|**TABLE_OWNER**|**sysname**|資料表擁有者名稱。 這個資料行一律會傳回值。|  
|**TABLE_NAME**|**sysname**|資料表名稱。 這個資料行一律會傳回值。|  
|**NON_UNIQUE**|**smallint**|NOT NULL。<br /><br /> 0 = 唯一<br /><br /> 1 = 不是唯一|  
|**INDEX_QUALIFIER**|**sysname**|索引擁有者名稱。 部分 DBMS 產品允許資料表擁有者以外的使用者建立索引。 在  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，此資料行一律是相同**TABLE_NAME**。|  
|**INDEX_NAME**|**sysname**|這是索引的名稱。 這個資料行一律會傳回值。|  
|**TYPE**|**smallint**|這個資料行一律會傳回值：<br /><br /> 0 = 資料表的統計資料<br /><br /> 1 = 叢集<br /><br /> 2 = 雜湊<br /><br /> 3 = 非叢集|  
|**SEQ_IN_INDEX**|**smallint**|索引內資料行的位置。|  
|**COLUMN_NAME**|**sysname**|每個資料行的資料行名稱**TABLE_NAME**傳回。 這個資料行一律會傳回值。|  
|**COLLATION**|**char(1)**|定序中使用的順序。 可為以下項目：<br /><br /> A = 遞增<br /><br /> D = 遞減<br /><br /> NULL = 不適用|  
|**基數**|**int**|資料表中的資料列數，或索引中的唯一值數目。|  
|**PAGES**|**int**|用來儲存索引或資料表的頁數。|  
|**FILTER_CONDITION**|**varchar(128)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不會傳回值。|  
  
## <a name="return-code-values"></a>傳回碼值  
 None  
  
## <a name="remarks"></a>備註  
 在結果集中的索引會出現在資料行依遞增順序排列**NON_UNIQUE**，**型別**， **INDEX_NAME**，以及**SEQ_IN_INDEX**。  
  
 叢集化的索引類型會參考依照索引順序來儲存資料表資料的索引。 這會對應至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]叢集索引。  
  
 雜湊的索引類型接受完全相符或範圍搜尋，但模式比對搜尋不會使用索引。  
  
 **sp_statistics**相當於**SQLStatistics** ODBC 中。 傳回的結果都會按照**NON_UNIQUE**，**型別**， **INDEX_QUALIFIER**， **INDEX_NAME**，和**SEQ_IN_索引**。 如需詳細資訊，請參閱 < [ODBC API 參考](https://go.microsoft.com/fwlink/?LinkId=68323)。  
  
## <a name="permissions"></a>Permissions  
 需要結構描述的 SELECT 權限。  
  
## <a name="example-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 下列範例會傳回資訊的相關`DimEmployee`資料表。  
  
```  
-- Uses AdventureWorks  
  
EXEC sp_statistics DimEmployee;  
```  
  
## <a name="see-also"></a>另請參閱  
 [目錄預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/catalog-stored-procedures-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

