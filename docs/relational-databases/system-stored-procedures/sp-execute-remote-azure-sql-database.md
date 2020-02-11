---
title: sp_execute_remote （Azure SQL Database） |Microsoft Docs
ms.custom: ''
ms.date: 02/01/2017
ms.service: sql-database
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- sp_execute_remote
- sp_execute_remote_TSQL
helpviewer_keywords:
- remote execution
- queries, remote execution
ms.assetid: ca89aa4c-c4c1-4c46-8515-a6754667b3e5
author: stevestein
ms.author: sstein
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 021a6e689dfc109f8a58ca080956aec7efc49291
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68124467"
---
# <a name="sp_execute_remote-azure-sql-database"></a>sp_execute_remote (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  在水準[!INCLUDE[tsql](../../includes/tsql-md.md)]資料分割配置中，于單一遠端 Azure SQL Database 或一組資料庫上執行語句，做為分區。  
  
 預存程式是彈性查詢功能的一部分。  請參閱[Azure SQL Database 彈性資料庫查詢總覽](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-overview/)和[分區化的彈性資料庫查詢（水準資料分割）](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-horizontal-partitioning/)。  
  
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
 [ \@data_source_name =]** [的]  
 識別執行語句的外部資料源。 請參閱[CREATE EXTERNAL DATA SOURCE &#40;transact-sql&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)。 外部資料源可以是 "RDBMS" 或 "SHARD_MAP_MANAGER" 類型。  
  
 [ \@stmt =]*語句*  
 這是包含[!INCLUDE[tsql](../../includes/tsql-md.md)]語句或批次的 Unicode 字串。 \@stmt 必須是 Unicode 常數或 Unicode 變數。 不允許使用比較複雜的 Unicode 運算式，如用 + 運算子來串連兩個字串。 不允許使用字元常數。 如果指定了 Unicode 常數，它的前面必須加上**N**。例如，Unicode 常數**N ' sp_who '** 有效，但字元常數 **' sp_who '** 則不是。 字串大小只受到可用資料庫伺服器記憶體的限制。 在64位伺服器上，字串的大小限制為 2 GB，也就是**Nvarchar （max）** 的大小上限。  
  
> [!NOTE]  
>  \@stmt 可以包含具有與變數名稱相同形式的參數，例如：`N'SELECT * FROM HumanResources.Employee WHERE EmployeeID = @IDParameter'`  
  
 包含在 stmt 中\@的\@每個參數在 params 參數定義清單和參數值清單中都必須有對應的專案。  
  
 [ \@params =]N '\@*parameter_name * * data_type* [,.。。*n* ] '  
 這是一個字串，其中包含已內嵌在 stmt 中\@之所有參數的定義。此字串必須是 Unicode 常數或 Unicode 變數。 每個參數定義都由參數名稱和資料類型組成。 *n*是指出其他參數定義的預留位置。 Stmtmust 中指定的\@每個參數都\@是在 params 中定義。 如果 stmt [!INCLUDE[tsql](../../includes/tsql-md.md)]中\@的語句或批次不包含參數， \@則不需要 params。 這個參數的預設值是 NULL。  
  
 [ \@param1 =]'*value1*'  
 這是參數字串所定義的第一個參數的值。 這個值可以是 Unicode 常數或 Unicode 變數。 針對包含在 stmt 中\@的每個參數，都必須提供參數值。當 stmt 中[!INCLUDE[tsql](../../includes/tsql-md.md)] \@的語句或批次沒有參數時，不需要這些值。  
  
 *n*  
 這是其他參數值的預留位置。 這些值只能是常數或變數。 這些值不能是比較複雜的運算式，如函數或利用運算子來建立的運算式。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或非零 (失敗)  
  
## <a name="result-sets"></a>結果集  
 傳回第一個 SQL 語句的結果集。  
  
## <a name="permissions"></a>權限  
 需要 `ALTER ANY EXTERNAL DATA SOURCE` 權限。  
  
## <a name="remarks"></a>備註  
 `sp_execute_remote`參數必須以特定順序輸入，如上述語法一節中所述。 如果未按順序輸入參數，就會出現錯誤訊息。  
  
 `sp_execute_remote`與[執行 &#40;transact-sql&#41;](../../t-sql/language-elements/execute-transact-sql.md)的行為相同，與批次和名稱範圍有關。 在執行 sp_execute_remote 語句之前，不會編譯 sp_execute_remote * \@stmt*參數中的 transact-sql 語句或批次。  
  
 `sp_execute_remote`將額外的資料行加入名為 ' $ShardName ' 的結果集，其中包含產生資料列的遠端資料庫名稱。  
  
 `sp_execute_remote`可以用來與[sp_executesql &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-executesql-transact-sql.md)類似。  
  
## <a name="examples"></a>範例  
### <a name="simple-example"></a>簡單範例  
 下列範例會在遠端資料庫上建立並執行簡單的 SELECT 語句。  
  
```sql  
EXEC sp_execute_remote  
    N'MyExtSrc',  
    N'SELECT COUNT(w_id) AS Count_id FROM warehouse'   
```  
  
### <a name="example-with-multiple-parameters"></a>具有多個參數的範例  
在使用者資料庫中建立資料庫範圍認證，並指定 master 資料庫的系統管理員認證。 建立指向 master 資料庫的外部資料源，並指定資料庫範圍認證。 接著，在使用者資料庫中的範例會執行 master `sp_set_firewall_rule`資料庫中的程式。 `sp_set_firewall_rule`程式需要3個參數，且`@name`參數必須為 Unicode。

```
EXEC sp_execute_remote @data_source_name  = N'PointToMaster', 
@stmt = N'sp_set_firewall_rule @name, @start_ip_address, @end_ip_address', 
@params = N'@name nvarchar(128), @start_ip_address varchar(50), @end_ip_address varchar(50)',
@name = N'TempFWRule', @start_ip_address = '0.0.0.2', @end_ip_address = '0.0.0.2';
```

## <a name="see-also"></a>另請參閱：

[CREATE DATABASE SCOPED CREDENTIAL](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)  
[建立外部資料源（Transact-sql）](../../t-sql/statements/create-external-data-source-transact-sql.md)  
    
