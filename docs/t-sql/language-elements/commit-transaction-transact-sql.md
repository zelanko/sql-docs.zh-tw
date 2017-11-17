---
title: "認可交易 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 09/09/2016
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, database-engine, pdw, sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- COMMIT
- COMMIT TRANSACTION
- COMMIT_TSQL
- COMMIT_TRANSACTION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ending transactions [SQL Server]
- user-defined transactions [SQL Server]
- committed transactions
- transactions [SQL Server], ending
- marking end of transactions [SQL Server]
- implicit transactions
- distributed transactions [SQL Server], committed
- transactions [SQL Server], committed
- COMMIT TRANSACTION statement
- rolling back transactions, COMMIT TRANSACTION
ms.assetid: f8fe26a9-7911-497e-b348-4e69c7435dc1
caps.latest.revision: 53
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 84ca8221700d3eabd443b84d97dea4f698e9f945
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="commit-transaction-transact-sql"></a>COMMIT TRANSACTION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

  標示順利完成的隱含或明確的交易結束。 如果 @@TRANCOUNT為 1，COMMIT TRANSACTION 會執行所有資料修改，因為交易在資料庫中，永久的一部分的開頭會釋出的交易，而 @ 遞減所持有的資源@TRANCOUNT設為 0。 如果 @@TRANCOUNT大於 1，COMMIT TRANSACTION 會遞減 @@TRANCOUNT只能由 1，而且交易會維持作用中。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- Applies to SQL Server (starting with 2008) and Azure SQL Database
  
COMMIT [ { TRAN | TRANSACTION }  [ transaction_name | @tran_name_variable ] ] [ WITH ( DELAYED_DURABILITY = { OFF | ON } ) ]  
[ ; ]  
```  
 
```  
-- Applies to Azure SQL Data Warehouse and Parallel Data Warehouse Database
  
COMMIT [ TRAN | TRANSACTION ] 
[ ; ]  
``` 
 
  
## <a name="arguments"></a>引數  
 *transaction_name*  
 **適用於：** SQL Server 和 Azure SQL Database
 
 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 會忽略這個項目。 *transaction_name*指定先前的 BEGIN TRANSACTION 所指派的交易名稱。 *transaction_name*必須符合識別碼規則，但不能超出 32 個字元。 *transaction_name*可用來當做可讀性的輔助由程式設計人員指出哪個巢狀 BEGIN TRANSACTION 認可的交易相關聯。  
  
 *@tran_name_variable*  
 **適用於：** SQL Server 和 Azure SQL Database  
 
這是包含有效交易名稱之使用者定義變數的名稱。 變數必須宣告 char、 varchar、 nchar 或 nvarchar 資料類型。 如果超出 32 個字元傳給變數，只會使用 32 個字元；其餘字元會截斷。  
  
 DELAYED_DURABILITY  
 **適用於：** SQL Server 和 Azure SQL Database   

 要求這筆交易以延遲持久性認可的選項。 如果資料庫已經使用 `DELAYED_DURABILITY = DISABLED` 或 `DELAYED_DURABILITY = FORCED` 更改，則會忽略要求。 請參閱主題[控制交易持久性](../../relational-databases/logs/control-transaction-durability.md)如需詳細資訊。  
  
## <a name="remarks"></a>備註  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 程式設計人員負責只在交易所參考的所有資料都邏輯正確時，才發出 COMMIT TRANSACTION。  
  
 如果認可的交易是一項 [!INCLUDE[tsql](../../includes/tsql-md.md)] 分散式交易，COMMIT TRANSACTION 會觸發 MS DTC 利用兩階段認可通訊協定來認可交易所涉及的所有伺服器。 如果本機交易跨越相同 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體的兩個或更多資料庫，執行個體會利用內部兩階段認可，以認可交易所涉及的所有資料庫。  
  
 當在巢狀交易內使用時，認可內部交易並不會釋出資源，或使它們的修改成為永久的。 只有在認可外部交易時，才會使資料修改永久化及釋出資源。 每個 COMMIT TRANSACTION 發出時 @@TRANCOUNT大於 1 只會遞減 @@TRANCOUNT 1。 當 @@TRANCOUNT是最後減量到 0，整個外部交易已認可。 因為*transaction_name*會忽略[!INCLUDE[ssDE](../../includes/ssde-md.md)]，發出 COMMIT TRANSACTION 時有未處理的內部交易 @ 只會參考名稱為外部交易的@TRANCOUNT1。  
  
 發出 COMMIT TRANSACTION 時 @@TRANCOUNT 0 會導致錯誤; 沒有對應的 BEGIN TRANSACTION。  
  
 您不能在發出 COMMIT TRANSACTION 陳述式之後回復交易，因為資料修改已成為資料庫的永久部份。  
  
 只有在陳述式開始時交易計數是 0 時，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 才會在單一陳述式內遞增交易。  
  
## <a name="permissions"></a>Permissions  
 需要 **public** 角色的成員資格。  
  
## <a name="examples"></a>範例  
  
### <a name="a-committing-a-transaction"></a>A. 認可交易  
**適用於：** SQL Server、 Azure SQL Database、 Azure SQL 資料倉儲和 Parallel Data Warehouse   

下列範例會刪除作業候選項。 它會使用 AdventureWorks。 
  
```   
BEGIN TRANSACTION;   
DELETE FROM HumanResources.JobCandidate  
    WHERE JobCandidateID = 13;   
COMMIT TRANSACTION;   
```  
  
### <a name="b-committing-a-nested-transaction"></a>B. 認可巢狀交易  
**適用於：** SQL Server 和 Azure SQL Database    

此範例會建立一份資料表，並產生三個層級的巢狀交易，再認可巢狀交易。 雖然每個`COMMIT TRANSACTION`陳述式有*transaction_name*參數時，沒有任何關聯性之間`COMMIT TRANSACTION`和`BEGIN TRANSACTION`陳述式。 *Transaction_name*參數是只負責協助程式設計人員確認已編寫適當的認可數目時，是以遞減`@@TRANCOUNT`到 0，以便認可外部交易。 
  
```   
IF OBJECT_ID(N'TestTran',N'U') IS NOT NULL  
    DROP TABLE TestTran;  
GO  
CREATE TABLE TestTran (Cola int PRIMARY KEY, Colb char(3));  
GO  
-- This statement sets @@TRANCOUNT to 1.  
BEGIN TRANSACTION OuterTran;  
  
PRINT N'Transaction count after BEGIN OuterTran = '  
    + CAST(@@TRANCOUNT AS nvarchar(10));  
 
INSERT INTO TestTran VALUES (1, 'aaa');  
 
-- This statement sets @@TRANCOUNT to 2.  
BEGIN TRANSACTION Inner1;  
 
PRINT N'Transaction count after BEGIN Inner1 = '  
    + CAST(@@TRANCOUNT AS nvarchar(10));  
  
INSERT INTO TestTran VALUES (2, 'bbb');  
  
-- This statement sets @@TRANCOUNT to 3.  
BEGIN TRANSACTION Inner2;  
  
PRINT N'Transaction count after BEGIN Inner2 = '  
    + CAST(@@TRANCOUNT AS nvarchar(10));  
  
INSERT INTO TestTran VALUES (3, 'ccc');  
  
-- This statement decrements @@TRANCOUNT to 2.  
-- Nothing is committed.  
COMMIT TRANSACTION Inner2;  
 
PRINT N'Transaction count after COMMIT Inner2 = '  
    + CAST(@@TRANCOUNT AS nvarchar(10));  
 
-- This statement decrements @@TRANCOUNT to 1.  
-- Nothing is committed.  
COMMIT TRANSACTION Inner1;  
 
PRINT N'Transaction count after COMMIT Inner1 = '  
    + CAST(@@TRANCOUNT AS nvarchar(10));  
  
-- This statement decrements @@TRANCOUNT to 0 and  
-- commits outer transaction OuterTran.  
COMMIT TRANSACTION OuterTran;  
  
PRINT N'Transaction count after COMMIT OuterTran = '  
    + CAST(@@TRANCOUNT AS nvarchar(10));  
```  
  
## <a name="see-also"></a>另請參閱  
 [BEGIN DISTRIBUTED TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-distributed-transaction-transact-sql.md)   
 [BEGIN TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-transaction-transact-sql.md)   
 [認可工作 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/commit-work-transact-sql.md)   
 [ROLLBACK TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/rollback-transaction-transact-sql.md)   
 [ROLLBACK WORK &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/rollback-work-transact-sql.md)   
 [SAVE TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/save-transaction-transact-sql.md)   
 [@@TRANCOUNT &#40;Transact-SQL&#41;](../../t-sql/functions/trancount-transact-sql.md)  
  
  

