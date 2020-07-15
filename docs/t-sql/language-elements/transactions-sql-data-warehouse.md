---
title: 交易 (SQL 資料倉儲) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 87e5e593-a121-4428-9d3c-3af876224e35
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: ac7b9a500bb87dca74082c9d16874131eb82402d
ms.sourcegitcommit: 01297f2487fe017760adcc6db5d1df2c1234abb4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/09/2020
ms.locfileid: "86197404"
---
# <a name="transactions-sql-data-warehouse"></a>交易 (SQL 資料倉儲)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  交易是一組一或多個全部認可或全部復原的資料庫陳述式。 每個交易都是不可部分完成、一致、隔離和耐用 (ACID)。 如果交易成功，表示認可交易中的所有陳述式。 如果交易失敗，表示群組中至少有一個陳述式失敗，然後整個群組都會復原。  
  
 交易的開始和結束取決於 AUTOCOMMIT 設定，和 BEGIN TRANSACTION、COMMIT 和 ROLLBACK 陳述式。 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 支援下列交易類型：  
  
-   *明確交易*會以 BEGIN TRANSACTION 陳述式開始，並以 COMMIT 或 ROLLBACK 陳述式結束。  
  
-   *自動認可交易*會在工作階段中自動起始，而不會以 BEGIN TRANSACTION 陳述式開始。 當 AUTOCOMMIT 設定為 ON 時，交易中會執行每個陳述式，而且不需要明確的 COMMIT 或 ROLLBACK。 當 AUTOCOMMIT 設定為 OFF 時，就需要 COMMIT 或 ROLLBACK 陳述式，才能決定交易的結果。 在 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 中，自動認可交易會在 COMMIT 或 ROLLBACK 陳述式之後，或在 SET AUTOCOMMIT OFF 陳述式之後立即開始。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例 &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```syntaxsql
BEGIN TRANSACTION [;]  
COMMIT [ TRAN | TRANSACTION | WORK ] [;]  
ROLLBACK [ TRAN | TRANSACTION | WORK ] [;]  
SET AUTOCOMMIT { ON | OFF } [;]  
SET IMPLICIT_TRANSACTIONS { ON | OFF } [;]  
```  
  
## <a name="arguments"></a>引數  
 BEGIN TRANSACTION  
 標示明確交易的起點。  
  
 COMMIT [ WORK ]  
 標示明確或自動認可交易的結束。 此陳述式會導致交易中的變更永久認可到資料庫。 陳述式 COMMIT 等同於 COMMIT WORK、COMMIT TRAN 和 COMMIT TRANSACTION。  
  
 ROLLBACK [ WORK ]  
 將交易復原到交易的開頭。 交易的變更不會認可到資料庫。 陳述式 ROLLBACK 等同於 ROLLBACK WORK、ROLLBACK TRAN 和 ROLLBACK TRANSACTION。  
  
 SET AUTOCOMMIT { **ON** | OFF }  
 決定如何開始和結束交易。  
  
 開啟  
 每個陳述式都在自己的交易下執行，而且不需要明確的 COMMIT 或 ROLLBACK 陳述式。 當 AUTOCOMMIT 是 ON 時，允許明確的交易。  
  
 OFF  
 當交易不在進行中時，[!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 會自動起始交易。 交易會執行任何後續的陳述式，而且需要 COMMIT 或 ROLLBACK，才能決定交易的結果。 一旦交易在此作業模式下認可或復原，模式仍為 OFF，但是 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 會起始新交易。 當 AUTOCOMMIT 是 OFF 時，不允許明確的交易。  
  
 如果您在作用中的交易內變更 AUTOCOMMIT 設定，設定會影響目前的交易，但是要在交易完成之後才會生效。  
  
 如果 AUTOCOMMIT 為 ON，執行另一個 SET AUTOCOMMIT ON 陳述式沒有任何作用。 同樣地，如果 AUTOCOMMIT 為 OFF，執行另一個 SET AUTOCOMMIT OFF 沒有任何作用。  
  
 SET IMPLICIT_TRANSACTIONS { ON | **OFF** }  
 這會切換為與 SET AUTOCOMMIT 相同的模式。 當設為 ON 時，SET IMPLICIT_TRANSACTIONS 會將連接設為隱含的交易模式。 當設為 OFF 時，會讓連線返回自動認可模式。  如需詳細資訊，請參閱 [SET IMPLICIT_TRANSACTIONS &#40;Transact-SQL&#41;](../../t-sql/statements/set-implicit-transactions-transact-sql.md)。  
  
## <a name="permissions"></a>權限  
 執行與交易相關的陳述式，不需要任何特定的權限。 在交易內執行陳述式則需要權限。  
  
## <a name="error-handling"></a>錯誤處理  
 如果執行 COMMIT 或 ROLLBACK，但沒有任何作用中交易，會引發錯誤。  
  
 如果交易正在進行時執行 BEGIN TRANSACTION，會引發錯誤。 如果在 BEGIN TRANSACTION 陳述式成功之後，或當工作階段處於 SET AUTOCOMMIT OFF 時執行 BEGIN TRANSACTION，就會發生這個錯誤。  
  
 如果因為執行階段陳述式錯誤以外的錯誤而讓明確交易無法順利完成，[!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 會自動復原交易，並釋放交易所佔用的一切資源。 例如，如果用戶端與 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 執行個體之間的網路連線已中斷，或用戶端登出應用程式，該連線任何尚未認可的交易會在網路通知該執行個體發生中斷時全部復原。  
  
 如果在批次中發生執行階段陳述式錯誤，[!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 的行為會與將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**XACT_ABORT** 設定為 **ON** 一致，整個交易也會復原。 如需 **XACT_ABORT** 設定的詳細資訊，請參閱 [SET XACT_ABORT (Transact-SQL)](https://msdn.microsoft.com/library/ms188792.aspx)。  
  
## <a name="general-remarks"></a>一般備註  
 工作階段在指定的時間只能執行一個交易。不支援儲存點和巢狀交易。  
  
 [!INCLUDE[DWsql](../../includes/dwsql-md.md)] 程式設計人員的責任是，只有當交易所參考的所有資料都邏輯正確時，才發出 COMMIT。  
  
 當工作階段在交易完成之前終止時，交易會復原。  
  
 交易模式是在工作階段的層級進行管理。 例如，如果一個工作階段開始明確交易、將 AUTOCOMMIT 設為 OFF，或將 IMPLICIT_TRANSACTIONS 設為 ON，都不會影響任何其他工作階段的交易模式。  
  
## <a name="limitations-and-restrictions"></a>限制事項  
 您不能在發出 COMMIT 陳述式之後復原交易，因為資料修改已成為資料庫的永久部份。  
  
 在明確交易中不能使用 [CREATE DATABASE &#40;Azure SQL 資料倉儲&#41;](../../t-sql/statements/create-database-azure-sql-data-warehouse.md) 和 [DROP DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-transact-sql.md) 命令。  
  
 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 沒有交易共用機制。 這表示在任何給定的時間點，只有一個工作階段可以在系統中進行任何交易。  
  
## <a name="locking-behavior"></a>鎖定行為  
 當多個使用者同時存取資料時，[!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 會使用鎖定來確保交易的完整性，並維護資料庫的一致性。 隱含交易和明確交易都使用鎖定。 每個交易會對資源要求不同類型的鎖定，例如交易相依的資料表或資料庫。 所有 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 鎖定都是資料表層級或更高層級。 鎖定會阻擋其他交易修改資源，以免造成要求鎖定的交易發生問題。 每個交易會在對鎖定的資源不再具有相依性時釋出鎖定。明確交易則會在交易完成 (無論是認可或復原) 之前維持鎖定。  
  
## <a name="examples-sssdwfull-and-sspdw"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-using-an-explicit-transaction"></a>A. 使用明確交易  
  
```  
BEGIN TRANSACTION;  
DELETE FROM HumanResources.JobCandidate  
    WHERE JobCandidateID = 13;  
COMMIT;  
```  
  
### <a name="b-rolling-back-a-transaction"></a>B. 復原交易  
 下列範例示範復原交易的效果。  在此範例中，ROLLBACK 陳述式將復原 INSERT 陳述式，但所建立的資料表仍會存在。  
  
```  
CREATE TABLE ValueTable (id int);  
BEGIN TRANSACTION;  
       INSERT INTO ValueTable VALUES(1);  
       INSERT INTO ValueTable VALUES(2);  
ROLLBACK;  
```  
  
### <a name="c-setting-autocommit"></a>C. 設定 AUTOCOMMIT  
 下列範例將 AUTOCOMMIT 設定設為 `ON`。  
  
```  
SET AUTOCOMMIT ON;  
```  
  
 下列範例將 AUTOCOMMIT 設定設為 `OFF`。  
  
```  
SET AUTOCOMMIT OFF;  
```  
  
### <a name="d-using-an-implicit-multi-statement-transaction"></a>D. 使用隱含的多重陳述式交易  
  
```  
SET AUTOCOMMIT OFF;  
CREATE TABLE ValueTable (id int);  
INSERT INTO ValueTable VALUES(1);  
INSERT INTO ValueTable VALUES(2);  
COMMIT;  
```  
  
## <a name="see-also"></a>另請參閱  
 [SET IMPLICIT_TRANSACTIONS &#40;Transact-SQL&#41;](../../t-sql/statements/set-implicit-transactions-transact-sql.md)   
 [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)   
 [@@TRANCOUNT &#40;Transact-SQL&#41;](../../t-sql/functions/trancount-transact-sql.md)  
  
  
