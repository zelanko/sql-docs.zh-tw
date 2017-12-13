---
title: "建立分割區配置 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 04/10/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE PARTITION SCHEME
- SCHEME
- PARTITION SCHEME
- CREATE_PARTITION_SCHEME_TSQL
- SCHEME_TSQL
- PARTITION_SCHEME_TSQL
dev_langs: TSQL
helpviewer_keywords:
- partitioned indexes [SQL Server], schemes
- partitioned tables [SQL Server], schemes
- CREATE PARTITION SCHEME statement
- partition schemes [SQL Server], creating
- filegroups [SQL Server], partitions
- partitioned indexes [SQL Server], filegroups
- partitioned tables [SQL Server], filegroups
- mapping partitions [SQL Server]
ms.assetid: 5b21c53a-b4f4-4988-89a2-801f512126e4
caps.latest.revision: "39"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 98abb06746c88d7876505033f5b209c30812fc5d
ms.sourcegitcommit: 721ad1cbc10e8147c087ae36b36296d72cbb0de8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/07/2017
---
# <a name="create-partition-scheme-transact-sql"></a>CREATE PARTITION SCHEME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  在目前資料庫建立一項配置，將資料分割資料表或索引的資料分割，對應至檔案群組。 資料分割資料表或索引的資料分割數目和網域，由資料分割函數來決定。 資料分割函式必須先建立在[CREATE PARTITION FUNCTION](../../t-sql/statements/create-partition-function-transact-sql.md)陳述式後再建立資料分割配置。  

>[!NOTE]
>在 Azure SQL Database 支援只有主要檔案群組。  

 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
CREATE PARTITION SCHEME partition_scheme_name  
AS PARTITION partition_function_name  
[ ALL ] TO ( { file_group_name | [ PRIMARY ] } [ ,...n ] )  
[ ; ]  
```  
  
## <a name="arguments"></a>引數  
 *partition_scheme_name*  
 這是資料分割結構描述的名稱。 資料分割配置名稱必須在資料庫內是唯一的且必須符合的規則[識別碼](../../relational-databases/databases/database-identifiers.md)。  
  
 *partition_function_name*  
 這是使用資料分割結構描述的資料分割函數名稱。 資料分割函數所建立的資料分割會對應至資料分割結構描述所指定的檔案群組。 *partition_function_name*必須已存在於資料庫。 單一資料分割無法同時包含 FILESTREAM 和非 FILESTREAM 檔案群組。  
  
 ALL  
 指定所有資料分割對應至檔案群組中提供*file_group_name*，或主要檔案群組若**[**主要**]**指定。 如果指定 ALL 時，只有一個*file_group_name*可以指定。  
  
 *file_group_name* | **[**主要**]** [ **，***...n*]  
 指定存放所指定的分割區的檔案群組的名稱*partition_function_name*。 *file_group_name*必須已存在於資料庫。  
  
 如果**[**主要**]**指定時，資料分割儲存在主要檔案群組上。 如果指定 ALL 時，只有一個*file_group_name*可以指定。 資料分割會指派給檔案群組與檔案群組列於中順序的資料分割 1，啟動 [**，***...n*]。 相同*file_group_name*可以指定一個以上的時間，以 [**，***...n*]。 如果 *n* 不足以保存在指定的資料分割數目*partition_function_name*，CREATE PARTITION SCHEME 失敗並發生錯誤。  
  
 如果*partition_function_name*產生小於資料分割數目比檔案群組，第一個未指派的檔案群組標示為 NEXT USED，並將資訊訊息顯示命名 NEXT USED 檔案群組。 如果指定 ALL 時，唯一*file_group_name*這個維護其 NEXT USED 屬性*partition_function_name*。 如果在 ALTER PARTITION FUNCTION 陳述式中建立資料分割，NEXT USED 檔案群組便會收到其他資料分割。 若要建立其他未指派的檔案群組來存放新的資料分割，請使用 ALTER PARTITION SCHEME。  
  
 當您指定主要檔案群組中的*file_group_name* [1**，***...n*]，主要必須是分隔的、 與**[**主要**]**，因為它是關鍵字。  
  
 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]只支援使用 PRIMARY。 請參閱範例 E 下方。 
  
## <a name="permissions"></a>Permissions  
 下列權限可用來執行 CREATE PARTITION SCHEME：  
  
-   ALTER ANY DATASPACE 權限。 這個權限預設會授與 **sysadmin** 固定伺服器角色以及 **db_owner** 和 **db_ddladmin** 固定資料庫角色的成員。  
  
-   建立資料分割結構描述之資料庫的 CONTROL 或 ALTER 權限。  
  
-   在建立資料分割結構描述的資料庫中，其伺服器的 CONTROL SERVER 或 ALTER ANY DATABASE 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-creating-a-partition-scheme-that-maps-each-partition-to-a-different-filegroup"></a>A. 建立將每個資料分割對應至不同檔案群組的資料分割結構描述  
 下列範例會建立一個資料分割函數，將資料表或索引分割成四個資料分割。 之後，會建立資料分割結構描述來指定分別存放這四份資料分割的檔案群組。 這個範例假設這些檔案群組已在資料庫中。  
  
```  
CREATE PARTITION FUNCTION myRangePF1 (int)  
AS RANGE LEFT FOR VALUES (1, 100, 1000);  
GO  
CREATE PARTITION SCHEME myRangePS1  
AS PARTITION myRangePF1  
TO (test1fg, test2fg, test3fg, test4fg);  
```  
  
 使用資料分割函數的資料表資料分割`myRangePF1`上分割資料行**col1** ，指派給下表所示。  
  
||||||  
|-|-|-|-|-|  
|**檔案群組**|`test1fg`|`test2fg`|`test3fg`|`test4fg`|  
|**資料分割**|1|2|3|4|  
|**值**|**col1** <= `1`|**col1**  >  `1` AND **col1** <= `100`|**col1**  >  `100` AND **col1** <= `1000`|**col1** > `1000`|  
  
### <a name="b-creating-a-partition-scheme-that-maps-multiple-partitions-to-the-same-filegroup"></a>B. 建立將多個資料分割對應至相同檔案群組的資料分割結構描述  
 如果所有資料分割都對應至相同的檔案群組，請使用 ALL 關鍵字。 但如果不是全部，而只是多個資料分割對應至相同的檔案群組，就必須依照下列範例所示來重複檔案群組名稱。  
  
```  
CREATE PARTITION FUNCTION myRangePF2 (int)  
AS RANGE LEFT FOR VALUES (1, 100, 1000);  
GO  
CREATE PARTITION SCHEME myRangePS2  
AS PARTITION myRangePF2  
TO ( test1fg, test1fg, test1fg, test2fg );  
```  
  
 使用資料分割函數的資料表資料分割`myRangePF2`上分割資料行**col1** ，指派給下表所示。  
  
||||||  
|-|-|-|-|-|  
|**檔案群組**|`test1fg`|`test1fg`|`test1fg`|`test2fg`|  
|**資料分割**|1|2|3|4|  
|**值**|**col1** <= `1`|**col1** > 1 AND **col1** <= `100`|**col1**  >  `100` AND **col1** <= `1000`|**col1** > `1000`|  
  
### <a name="c-creating-a-partition-scheme-that-maps-all-partitions-to-the-same-filegroup"></a>C. 建立將所有資料分割對應至相同檔案群組的資料分割結構描述  
 下列範例會建立上述各範例的相同資料分割函數，且會建立一項資料分割結構描述，將所有資料分割對應至相同的檔案群組。  
  
```  
CREATE PARTITION FUNCTION myRangePF3 (int)  
AS RANGE LEFT FOR VALUES (1, 100, 1000);  
GO  
CREATE PARTITION SCHEME myRangePS3  
AS PARTITION myRangePF3  
ALL TO ( test1fg );  
```  
  
### <a name="d-creating-a-partition-scheme-that-specifies-a-next-used-filegroup"></a>D. 建立指定 'NEXT USED' 檔案群組的資料分割結構描述  
 下列範例會建立上述各範例的相同資料分割函數，且會建立一項資料分割結構描述來列出數量超出相關聯資料分割函數所建立之資料分割的檔案群組。  
  
```  
CREATE PARTITION FUNCTION myRangePF4 (int)  
AS RANGE LEFT FOR VALUES (1, 100, 1000);  
GO  
CREATE PARTITION SCHEME myRangePS4  
AS PARTITION myRangePF4  
TO (test1fg, test2fg, test3fg, test4fg, test5fg)  
```  
  
 執行這個陳述式會傳回下列訊息。  
  
已成功建立資料分割配置 'myRangePS4'。 'test5fg' 會標示為分割區配置 'myRangePS4' 中下一個使用的檔案群組。  
  
  
 如果將資料分割函數 `myRangePF4` 改成加入資料分割，`test5fg` 檔案群組會收到新建立的資料分割。  

### <a name="e-creating-a-partition-schema-only-on-primary---only-primary-is-supported-for-includesqldbesaincludessqldbesa-mdmd"></a>E. 建立資料分割結構描述只在主要-只有主要被支援[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]

 下列範例會建立一個資料分割函數，將資料表或索引分割成四個資料分割。 資料分割配置然後就會建立指定主要檔案群組中建立的所有資料分割。  
  
```  
CREATE PARTITION FUNCTION myRangePF1 (int)  
AS RANGE LEFT FOR VALUES (1, 100, 1000);  
GO  
CREATE PARTITION SCHEME myRangePS1  
AS PARTITION myRangePF1  
ALL TO ( [PRIMARY] );  
```
   
## <a name="see-also"></a>請參閱  
 [CREATE PARTITION FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-function-transact-sql.md)   
 [ALTER PARTITION SCHEME &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-partition-scheme-transact-sql.md)   
 [DROP PARTITION SCHEME &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-partition-scheme-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [建立資料分割的資料表及索引](../../relational-databases/partitions/create-partitioned-tables-and-indexes.md)   
 [sys.partition_schemes &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-partition-schemes-transact-sql.md)   
 [sys.data_spaces &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)   
 [sys.destination_data_spaces &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-destination-data-spaces-transact-sql.md)   
 [sys.partitions &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)   
 [sys.tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)  
  
  
