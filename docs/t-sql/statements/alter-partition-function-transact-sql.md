---
title: "ALTER PARTITION FUNCTION (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER PARTITION FUNCTION
- ALTER_PARTITION_FUNCTION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- splitting partitions [SQL Server]
- partitioned tables [SQL Server], splitting
- ALTER PARTITION FUNCTION statement
- merging partitions [SQL Server]
- partitioned indexes [SQL Server], merging
- partitioned indexes [SQL Server], splitting
- modifying partition functions
- partition functions [SQL Server], modifying
- partitioned tables [SQL Server], merging
ms.assetid: 70866dac-0a8f-4235-8108-51547949ada4
caps.latest.revision: 43
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5969f9487a55437febfba9f6deec7fb1e0df5f02
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="alter-partition-function-transact-sql"></a>ALTER PARTITION FUNCTION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  藉由分割或合併資料分割函數的界限值來變更資料分割函數。 您可以執行 ALTER PARTITION FUNCTION，將使用資料分割函數的任何資料表或索引的一份資料分割分成兩份資料分割，或將兩份資料分割合併成一份較小的資料分割。  
  
> [!CAUTION]  
>  多份資料表或索引可以使用相同的資料分割函數。 ALTER PARTITION FUNCTION 會在單一交易中影響所有的資料表或索引。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
ALTER PARTITION FUNCTION partition_function_name()  
{   
    SPLIT RANGE ( boundary_value )  
  | MERGE RANGE ( boundary_value )   
} [ ; ]  
```  
  
## <a name="arguments"></a>引數  
 *partition_function_name*  
 這是您要修改的資料分割函數名稱。  
  
 SPLIT RANGE ( *boundary_value* )  
 將一個資料分割加入資料分割函數。 *boundary_value*決定新的資料分割的範圍，且必須與不同的資料分割函數的現有界限範圍。 根據*boundary_value*、[!INCLUDE[ssDE](../../includes/ssde-md.md)]分割成兩個的其中一個現有的範圍。 這兩個新*boundary_value*位於視為新的資料分割。  
  
 線上必須有檔案群組存在，且使用資料分割函數的資料分割結構描述必須將它標示為 NEXT USED，以便存放新的資料分割。 您可以在 CREATE PARTITION SCHEME 陳述式中，將檔案群組配置給資料分割。 如果 CREATE PARTITION SCHEME 陳述式配置的檔案群組超出需要 (CREATE PARTITION FUNCTION 陳述式所建立的資料分割數，比用來存放它們的檔案群組少)，就會有未指派的檔案群組，資料分割結構描述會將其中一個標示為 NEXT USED。 這個檔案群組將存放新的資料分割。 如果沒有資料分割結構描述標示為 NEXT USED 的檔案群組，您就必須利用 ALTER PARTITION SCHEME 來加入檔案群組，或指定現有的檔案群組，來存放新的資料分割。 您可以指定已存放資料分割的檔案群組來存放其他資料分割。 由於資料分割函數可以參與多項資料分割結構描述，因此，所有使用要新增資料分割之資料分割函數的資料分割結構描述，都必須有 NEXT USED 檔案群組。 否則，ALTER PARTITION FUNCTION 會失敗，且會出現一則錯誤，顯示一個或多個缺少 NEXT USED 檔案群組的資料分割結構描述。  
  
 如果您在相同的檔案群組中建立所有資料分割，會在一開始時自動將該檔案群組指派為 NEXT USED 檔案群組。 但執行分割作業之後，即不會再有指定的 NEXT USED 檔案群組。 您必須使用 ALTER PARITION SCHEME 將檔案群組明確指派為 NEXT USED 檔案群組，否則後續分割作業將會失敗。  
  
> [!NOTE]  
>  資料行存放區索引的限制： 只有空的資料分割可以分割中，當資料行存放區索引存在於資料表。 您必須卸除或停用資料行存放區索引，才能執行此作業  
  
 合併 [範圍 ( *boundary_value*)]  
 卸除一份資料分割，將這份資料分割中的任何值合併到其餘某份資料分割中。 範圍 (*boundary_value*) 必須是已卸除資料分割中的值會合併到其中的現有界限值。 最初保留的檔案群組*boundary_value*會移除從分割區配置中，除非它正由其餘的資料分割，或標示為 NEXT USED 屬性。 一開始未存放在檔案群組中的合併分割區所在*boundary_value*。 *boundary_value*是常數運算式可以參考變數 （包括使用者定義型別變數） 或函式 （包括使用者定義函數）。 其無法參考 [!INCLUDE[tsql](../../includes/tsql-md.md)] 運算式。 *boundary_value*必須是符合或可隱含轉換成其對應的分割資料行的資料類型和隱含方式轉換期間將無法截斷的大小和小數位數的值不符合的其對應*input_parameter_type*。  
  
> [!NOTE]  
>  資料行存放區索引的限制： 無法合併兩個非空白分割區包含資料行存放區索引。 您必須卸除或停用資料行存放區索引，才能執行此作業  
  
## <a name="best-practices"></a>最佳作法  
 請務必在資料分割範圍的兩端保留空白的資料分割，確保資料分割 (載入新資料之前) 和資料分割合併 (卸載舊資料之後) 不會產生任何資料移動。 請避免分割或合併已擴展的資料分割。 因為這樣做可能會導致記錄產生作業延長四倍以上，也可能會造成嚴重鎖定，所以可能非常沒有效率。  
  
## <a name="limitations-and-restrictions"></a>限制事項  
 ALTER PARTITION FUNCTION 會在單一不可部分完成的作業中，重新分割任何使用函數的資料表和索引。 不過，這項作業是離線進行的，可能非常需要資源，這會隨著重新分割的範圍而不同。  
  
 ALTER PARTITION FUNCTION 只能用來將一份資料分割分成兩份，或將兩份資料分割合併成一份。 若要變更資料表的分割方式 (例如，從 10 份資料分割到 5 份資料分割)，您可以練習任何下列選項。 這些選項的資源消耗程度各異，會隨著系統的組態而不同：  
  
-   利用所需要的資料分割函數來建立新的資料分割資料表，再利用 INSERT INTO...SELECT FROM 陳述式，將舊資料表中的資料插入新資料表中。  
  
-   建立堆積的資料分割叢集索引。  
  
    > [!NOTE]  
    >  卸除資料分割叢集索引會產生資料分割堆積。  
  
-   利用設定了 DROP EXISTING = ON 子句的 [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE INDEX 陳述式來卸除和重建現有的資料分割索引。  
  
-   執行 ALTER PARTITION FUNCTION 陳述式的序列。  
  
 ALTER PARITITION FUNCTION 所影響的所有檔案群組都必須在線上。  
  
 當使用資料分割函數的任何資料表有停用的叢集索引時，ALTER PARTITION FUNCTION 會失敗。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不提供修改資料分割函數的複寫支援。 您必須在訂閱資料庫中，手動套用發行集資料庫中的資料分割函數變更。  
  
## <a name="permissions"></a>Permissions  
 下列中的任何權限都可用來執行 ALTER PARTITION FUNCTION：  
  
-   ALTER ANY DATASPACE 權限。 這個權限預設會授與 **sysadmin** 固定伺服器角色以及 **db_owner** 和 **db_ddladmin** 固定資料庫角色的成員。  
  
-   對於建立資料分割函數之資料庫的 CONTROL 或 ALTER 權限。  
  
-   對於建立資料分割函數之資料庫伺服器的 CONTROL SERVER 或 ALTER ANY DATABASE 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-splitting-a-partition-of-a-partitioned-table-or-index-into-two-partitions"></a>A. 將資料分割或分割資料表或索引的分割分成兩個資料分割  
 下列範例會建立一個資料分割函數，將資料表或索引分割成四個資料分割。 `ALTER PARTITION FUNCTION` 會將其中一個資料分割分成兩個，以建立總計五個的資料分割。  
  
```tsql  
IF EXISTS (SELECT * FROM sys.partition_functions  
    WHERE name = 'myRangePF1')  
DROP PARTITION FUNCTION myRangePF1;  
GO  
CREATE PARTITION FUNCTION myRangePF1 (int)  
AS RANGE LEFT FOR VALUES ( 1, 100, 1000 );  
GO  
--Split the partition between boundary_values 100 and 1000  
--to create two partitions between boundary_values 100 and 500  
--and between boundary_values 500 and 1000.  
ALTER PARTITION FUNCTION myRangePF1 ()  
SPLIT RANGE (500);  
```  
  
### <a name="b-merging-two-partitions-of-a-partitioned-table-into-one-partition"></a>B. 將分割資料表的兩個資料分割合併成一個資料分割  
 下列範例會建立上述中的相同資料分割函數，再將兩份資料分割合併成一份資料分割，總共三份的資料分割。  
  
```tsql  
IF EXISTS (SELECT * FROM sys.partition_functions  
    WHERE name = 'myRangePF1')  
DROP PARTITION FUNCTION myRangePF1;  
GO  
CREATE PARTITION FUNCTION myRangePF1 (int)  
AS RANGE LEFT FOR VALUES ( 1, 100, 1000 );  
GO  
--Merge the partitions between boundary_values 1 and 100  
--and between boundary_values 100 and 1000 to create one partition  
--between boundary_values 1 and 1000.  
ALTER PARTITION FUNCTION myRangePF1 ()  
MERGE RANGE (100);  
```  
  
## <a name="see-also"></a>另請參閱  
 [資料分割的資料表和索引](../../relational-databases/partitions/partitioned-tables-and-indexes.md)   
 [CREATE PARTITION FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-function-transact-sql.md)   
 [DROP PARTITION FUNCTION &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-partition-function-transact-sql.md)   
 [CREATE PARTITION SCHEME &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-scheme-transact-sql.md)   
 [ALTER PARTITION SCHEME &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-partition-scheme-transact-sql.md)   
 [DROP PARTITION SCHEME &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-partition-scheme-transact-sql.md)   
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [sys.partition_functions &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-partition-functions-transact-sql.md)   
 [sys.partition_parameters &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-partition-parameters-transact-sql.md)   
 [sys.partition_range_values &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-partition-range-values-transact-sql.md)   
 [sys.partitions &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)   
 [sys.tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)  
  
  
