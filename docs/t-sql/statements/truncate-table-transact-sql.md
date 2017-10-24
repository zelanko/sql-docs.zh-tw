---
title: "TRUNCATE TABLE (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- TRUNCATE
- TRUNCATE TABLE
- TRUNCATE_TSQL
- TRUNCATE_TABLE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- row removal [SQL Server], TRUNCATE TABLE statement
- table truncating [SQL Server]
- removing rows
- TRUNCATE TABLE statement
- deleting rows
- dropping rows
ms.assetid: 3d544eed-3993-4055-983d-ea334f8c5c58
caps.latest.revision: 41
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: dd20fe12af6f1dcaf378d737961bc2ba354aabe5
ms.openlocfilehash: 1d393c67c8489765aa92c861bc28c8e4d0e2eea4
ms.contentlocale: zh-tw
ms.lasthandoff: 10/04/2017

---
# <a name="truncate-table-transact-sql"></a>TRUNCATE TABLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  移除所有資料列的資料表或指定的分割區資料表，而不記錄個別資料列刪除。 TRUNCATE TABLE 類似於不含 WHERE 子句的 DELETE 陳述式；不過，TRUNCATE TABLE 比較快，使用的系統資源和交易記錄資源也比較少。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```tsql  
-- Syntax for SQL Server and Azure SQL Database  
  
TRUNCATE TABLE   
    [ { database_name .[ schema_name ] . | schema_name . } ]  
    table_name  
    [ WITH ( PARTITIONS ( { <partition_number_expression> | <range> }   
    [ , ...n ] ) ) ]  
[ ; ]  
  
<range> ::=  
<partition_number_expression> TO <partition_number_expression>  
```  
  
```tsql  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
TRUNCATE TABLE [ { database_name . [ schema_name ] . | schema_name . ] table_name  
[;]  
```  
  
## <a name="arguments"></a>引數  
 *database_name*  
 這是資料庫的名稱。  
  
 *schema_name*  
 這是資料表所屬的結構描述名稱。  
  
 *table_name*  
 這是要截斷之資料表，或要從中移除所有資料列之資料表的名稱。 *table_name*必須是常值。 *table_name*不可**object_id （)**函式或變數。  
  
 與 (資料分割 ({ \<*編號運算式*> |\<*範圍*>} [，.....n]))  
**適用於**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]透過[新版](http://go.microsoft.com/fwlink/p/?LinkId=299658))
  
 指定要截斷的資料分割，或要移除所有資料列的部分。 如果資料表未分割，**與資料分割**引數會產生錯誤。 如果**與資料分割**未提供子句，整個資料表將會被截斷。  
  
 *\<編號運算式 >*可以下列方式指定： 
  
-   提供資料分割的數目，例如：`WITH (PARTITIONS (2))`  
  
-   提供分割區編號為數個個別分割區以逗號分隔，例如：`WITH (PARTITIONS (1, 5))`  
  
-   同時提供範圍和個別分割區，例如：`WITH (PARTITIONS (2, 4, 6 TO 8))`  
  
-   *\<範圍 >*可以指定為分隔的資料分割編號**TO**，例如：`WITH (PARTITIONS (6 TO 8))`  
  
 要截斷的資料分割的資料表，資料表和索引必須對齊 （資料分割在相同的資料分割函數上）。  
  
## <a name="remarks"></a>備註  
 相較於 DELETE 陳述式，TRUNCATE TABLE 的優點如下：  
  
-   使用的交易記錄空間較少。  
  
     DELETE 陳述式每次會移除一個資料列，在交易記錄中，每個刪除的資料列都會記錄一個項目。 TRUNCATE TABLE 會取消配置用來儲存資料表資料的資料頁，以移除資料，而且交易記錄只會記錄頁面的取消配置。  
  
-   通常會使用較少鎖定。  
  
     當利用資料列鎖定來執行 DELETE 陳述式時，會鎖定資料表中的每個資料列，以便進行刪除。 TRUNCATE TABLE 一律會鎖定資料表 (包括結構描述 (SCH-M) 鎖定) 和頁面，但不會鎖定每個資料列。  
  
-   零頁面會保留在資料表中，沒有例外。  
  
     在執行 DELETE 陳述式之後，資料表仍可以包含空白頁。 例如，當沒有至少一項獨佔 (LCK_M_X) 資料表鎖定時，無法取消配置堆積中的空白頁。 如果刪除作業並未使用資料表鎖定，資料表 (堆積) 會包含許多空白頁。 對於索引，刪除作業可能會留下空白頁，不過，背景清除處理序很快就會取消配置這些頁面。  
  
 TRUNCATE TABLE 會移除資料表中的所有資料列，但會保留資料表結構及其資料行、條件約束、索引等。 若要移除資料表的資料之外，還要移除資料表定義，請使用 DROP TABLE 陳述式。  
  
 如果資料表包含識別欄位，該資料行的計數器會重設為資料行定義的種子值。 如果未定義任何初始值，就會使用預設值 1。 若要保留識別計數器，請改用 DELETE。  
  
## <a name="restrictions"></a>限制  
 下列狀況的資料表不能使用 TRUNCATE TABLE：  
  
-   FOREIGN KEY 條件約束所參考的資料表。 (您可以截斷具有外部索引鍵 (參考其本身) 的資料表)。  
  
-   參與索引檢視表的資料表。  
  
-   利用異動複寫或合併式複寫來發行的資料表。  
  
 如果資料表含有一個或多個這些特性，請改用 DELETE 陳述式。  
  
 TRUNCATE TABLE 無法啟動觸發程序，因為作業不會記錄個別的資料列刪除動作。 如需詳細資訊，請參閱 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)。 
 
 在[!INCLUDE[sssdwfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[sspdw](../../includes/sspdw-md.md)]:

- TRUNCATE TABLE 解釋陳述式內不允許。

- TRUNCATE TABLE 無法執行交易內。
  
## <a name="truncating-large-tables"></a>截斷大型資料表  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]能夠卸除或截斷擁有超過 128 個範圍，而不會卸除所需的所有範圍中保持同步鎖定的資料表。  
  
## <a name="permissions"></a>Permissions  
 所需的最低權限為 ALTER 上*table_name*。 TRUNCATE TABLE 權限預設會授與資料表擁有者、系統管理員 (sysadmin) 固定伺服器角色成員，以及 db_owner 和 db_ddladmin 固定資料庫角色的成員，這些權限不能轉讓。 不過，您可以將 TRUNCATE TABLE 陳述式納入模組 (如預存程序) 中，再利用 EXECUTE AS 子句，將適當的權限授與模組。  
  
## <a name="examples"></a>範例  
  
### <a name="a-truncate-a-table"></a>A. 截斷資料表  
 下列範例會移除 `JobCandidate` 資料表的所有資料。 `SELECT` 陳述式前後會包含在 `TRUNCATE TABLE` 陳述式前後，以比較結果。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT COUNT(*) AS BeforeTruncateCount   
FROM HumanResources.JobCandidate;  
GO  
TRUNCATE TABLE HumanResources.JobCandidate;  
GO  
SELECT COUNT(*) AS AfterTruncateCount   
FROM HumanResources.JobCandidate;  
GO  
```  
  
### <a name="b-truncate-table-partitions"></a>B. 截斷資料表資料分割  
  
**適用於**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]透過[新版](http://go.microsoft.com/fwlink/p/?LinkId=299658))
  
 下列範例會截斷分割資料表的指定資料分割。 `WITH (PARTITIONS (2, 4, 6 TO 8))` 語法會導致資料分割編號 2、 4、 6、 7 和 8 被截斷。  
  
```  
TRUNCATE TABLE PartitionTable1   
WITH (PARTITIONS (2, 4, 6 TO 8));  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [DROP TABLE &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-table-transact-sql.md)   
 [IDENTITY &#40;屬性&#41; &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql-identity-property.md)  
  
  


