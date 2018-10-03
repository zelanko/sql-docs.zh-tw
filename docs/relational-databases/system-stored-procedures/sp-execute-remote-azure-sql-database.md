---
title: sp_execute_remote (Azure SQL Database) |Microsoft Docs
ms.custom: ''
ms.date: 02/01/2017
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- sp_execute_remote
- sp_execute_remote_TSQL
helpviewer_keywords:
- remote execution
- queries, remote execution
ms.assetid: ca89aa4c-c4c1-4c46-8515-a6754667b3e5
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: c61098eabfe58cb1e791dd379cafb5f91d50f247
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47837086"
---
# <a name="spexecuteremote-azure-sql-database"></a>sp_execute_remote (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  執行[!INCLUDE[tsql](../../includes/tsql-md.md)]單一遠端 Azure SQL Database 或一組資料庫做為分區中的水平資料分割配置上的陳述式。  
  
 預存程序是彈性查詢功能的一部分。  請參閱[Azure SQL Database 彈性資料庫查詢概觀](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-overview/)並[彈性資料庫查詢 （水平資料分割） 的分區化的](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-horizontal-partitioning/)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
sp_execute_remote [ @data_source_name = ] datasourcename  
[ , @stmt = ] statement  
[   
  { , [ @params = ] N'@parameter_name data_type [,...n ]' }   
     { , [ @param1 = ] 'value1' [ ,...n ] }  
]  
```  
  
## <a name="arguments"></a>引數  
 [ \@data_source_name =] *datasourcename*  
 識別執行陳述式的外部資料來源。 請參閱[建立外部資料來源&#40;TRANSACT-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)。 外部資料來源可以是類型的"RDBMS"或"SHARD_MAP_MANAGER"。  
  
 [ \@stmt =]*陳述式*  
 是 Unicode 字串，包含[!INCLUDE[tsql](../../includes/tsql-md.md)]陳述式或批次。 \@陳述式必須是 Unicode 常數或 Unicode 變數。 不允許使用比較複雜的 Unicode 運算式，如用 + 運算子來串連兩個字串。 不允許使用字元常數。 如果指定了 Unicode 常數，它必須在前面加上**N**。比方說，Unicode 常數**N'SP_WHO '** 有效，但字元常數 **'sp_who'** 不是。 字串大小只受到可用資料庫伺服器記憶體的限制。 在 64 位元伺服器上字串的大小會限制為 2 GB，最大的大小**nvarchar （max)**。  
  
> [!NOTE]  
>  \@陳述式可以包含參數擁有相同的格式，做為變數的名稱，例如： `N'SELECT * FROM HumanResources.Employee WHERE EmployeeID = @IDParameter'`  
  
 包含在每個參數\@陳述式必須有對應的項目中都\@params 參數定義清單和參數值清單。  
  
 [ \@params =] N'\@*parameter_name * * data_type* [，...*n* ] '  
 是一個字串，其中包含之所有參數的已內嵌在定義\@陳述式。此字串必須是 Unicode 常數或 Unicode 變數。 每個參數定義都由參數名稱和資料類型組成。 *n*是指出其他參數定義的預留位置。 每個指定的參數\@stmtmust 定義在\@params。 如果[!INCLUDE[tsql](../../includes/tsql-md.md)]陳述式或批次都在\@陳述式不包含參數， \@params 並非必要。 這個參數的預設值是 NULL。  
  
 [ \@param1 =] '*value1*'  
 這是參數字串所定義的第一個參數的值。 這個值可以是 Unicode 常數或 Unicode 變數。 必須提供每個參數中包含的參數值\@陳述式。值不是必要的時機[!INCLUDE[tsql](../../includes/tsql-md.md)]陳述式或批次都在\@陳述式沒有任何參數。  
  
 *n*  
 這是其他參數值的預留位置。 這些值只能是常數或變數。 這些值不能是比較複雜的運算式，如函數或利用運算子來建立的運算式。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或非零 (失敗)  
  
## <a name="result-sets"></a>結果集  
 傳回的結果集第一個 SQL 陳述式。  
  
## <a name="permissions"></a>Permissions  
 需要 `ALTER ANY EXTERNAL DATA SOURCE` 權限。  
  
## <a name="remarks"></a>備註  
 `sp_execute_remote` 上述語法 」 一節中所述，必須以特定順序輸入參數。 如果未按順序輸入參數，就會出現錯誤訊息。  
  
 `sp_execute_remote` 具有相同的行為[EXECUTE &#40;TRANSACT-SQL&#41; ](../../t-sql/language-elements/execute-transact-sql.md)批次和名稱的範圍。 TRANSACT-SQL 陳述式或批次都在 sp_execute_remote  *\@stmt* sp_execute_remote 陳述式執行之前，不會編譯參數。  
  
 `sp_execute_remote` 將額外的資料行加入至名為 '$ShardName'，其中包含遠端資料庫產生的資料列名稱的結果集。  
  
 `sp_execute_remote` 可以使用類似[sp_executesql &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-executesql-transact-sql.md)。  
  
## <a name="examples"></a>範例  
### <a name="simple-example"></a>簡單範例  
 下列範例會建立與遠端資料庫上執行簡單的 SELECT 陳述式。  
  
```sql  
EXEC sp_execute_remote  
    N'MyExtSrc',  
    N'SELECT COUNT(w_id) AS Count_id FROM warehouse'   
```  
  
### <a name="example-with-multiple-parameters"></a>具有多個參數的範例  
在使用者資料庫中，指定系統管理員認證，master 資料庫中建立資料庫範圍認證。 建立指向 master 資料庫，並指定資料庫範圍認證的外部資料來源。 然後執行下列命令，在使用者資料庫中，範例`sp_set_firewall_rule`master 資料庫中的程序。 `sp_set_firewall_rule`程序需要 3 個參數，並要求`@name`參數必須為 Unicode。

```
EXEC sp_execute_remote @data_source_name  = N'PointToMaster', 
@stmt = N'sp_set_firewall_rule @name, @start_ip_address, @end_ip_address', 
@params = N'@name nvarchar(128), @start_ip_address varchar(50), @end_ip_address varchar(50)',
@name = N'TempFWRule', @start_ip_address = '0.0.0.2', @end_ip_address = '0.0.0.2';
```

## <a name="see-also"></a>另請參閱：

[建立資料庫範圍認證](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)  
[建立外部資料來源 (TRANSACT-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md)  
    
