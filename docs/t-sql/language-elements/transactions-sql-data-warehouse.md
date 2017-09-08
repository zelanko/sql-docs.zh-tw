---
title: "交易 （SQL 資料倉儲） |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 87e5e593-a121-4428-9d3c-3af876224e35
caps.latest.revision: 8
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8202a0de588bce3a36fc048e68c283b52db7e89d
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="transactions-sql-data-warehouse"></a>交易 （SQL 資料倉儲）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  交易是一組一個或多個資料庫陳述式完整地被認可或全部回復。 每一筆交易是不可部分完成、 一致、 隔離且持久 (ACID)。 如果交易成功，就無法認可中的所有陳述式。 如果交易失敗，這至少其中一個群組中的陳述式失敗，則會回復整個群組。  
  
 開頭和結尾的交易取決於自動認可設定和 BEGIN TRANSACTION、 COMMIT 和 ROLLBACK 陳述式。 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]支援下列類型的交易：  
  
-   *外顯交易*開頭和結尾的 COMMIT 或 ROLLBACK 陳述式的 BEGIN TRANSACTION 陳述式。  
  
-   *自動認可交易*自動起始工作階段中，並不會啟動 BEGIN TRANSACTION 陳述式。 當自動認可設定為 ON 時，每個陳述式會在交易中執行，而且沒有明確 COMMIT 或 ROLLBACK 不需要。 當自動認可設定為 OFF 時，COMMIT 或 ROLLBACK 陳述式，才能決定交易的結果。 在[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]，COMMIT 或 ROLLBACK 陳述式，後面緊接著或 SET 自動認可 OFF 陳述式之後，開始自動認可交易。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [TRANSACT-SQL 語法慣例 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
BEGIN TRANSACTION [;]  
COMMIT [ TRAN | TRANSACTION | WORK ] [;]  
ROLLBACK [ TRAN | TRANSACTION | WORK ] [;]  
SET AUTOCOMMIT { ON | OFF } [;]  
SET IMPLICIT_TRANSACTIONS { ON | OFF } [;]  
```  
  
## <a name="arguments"></a>引數  
 BEGIN TRANSACTION  
 標示外顯交易的起點。  
  
 認可 [工作]  
 標示明確或自動認可交易的結尾。 這個陳述式會變更為永久向資料庫認可交易中。 陳述式認可等同於 COMMIT WORK，COMMIT TRAN、 COMMIT TRANSACTION。  
  
 復原 [工作]  
 交易回復到交易的開頭。 不向資料庫認可交易的變更。 陳述式回復等同於 ROLLBACK WORK、 ROLLBACK TRAN 與 ROLLBACK TRANSACTION。  
  
 設定自動認可 { **ON** |OFF}  
 決定如何開始和結束交易。  
  
 ON  
 每個陳述式執行自己的交易，而且沒有明確 COMMIT 或 ROLLBACK 陳述式不需要。 當自動認可是 ON 時，不允許明確的交易。  
  
 OFF  
 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]交易已不在進行中時，會自動起始交易。 任何後續陳述式會執行交易的一部分，並認可或回復，才能決定交易的結果。 一旦交易認可或復原在這種作業模式下，模式仍為 OFF，和[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]初始新交易。 當自動認可是 OFF 時，不允許明確的交易。  
  
 如果您變更使用中交易內的自動認可設定，並會影響在目前交易的設定，以及在交易完成之前不會影響。  
  
 如果自動認可為 ON 時，執行另一個設為自動認可 ON 陳述式沒有任何作用。 同樣地，如果自動認可是 OFF，另一個設定自動認可關閉執行沒有任何作用。  
  
 SET IMPLICIT_TRANSACTIONS {ON |**OFF** }  
 切換以設定自動認可的相同模式。 當設為 ON 時，SET IMPLICIT_TRANSACTIONS 會將連接設為隱含的交易模式。 當設為 OFF，則會將連接返回自動認可模式。  如需詳細資訊，請參閱[SET IMPLICIT_TRANSACTIONS &#40;TRANSACT-SQL &#41;](../../t-sql/statements/set-implicit-transactions-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 沒有特定的權限才能執行的交易相關的陳述式。 執行交易內的陳述式所需的權限。  
  
## <a name="error-handling"></a>錯誤處理  
 如果認可或復原執行而且沒有任何使用中交易，會引發錯誤。  
  
 如果交易已正在進行時執行 BEGIN TRANSACTION，則會引發錯誤。 如果成功的 BEGIN TRANSACTION 陳述式之後，或在自動認可設定關閉工作階段時，就會發生的 BEGIN TRANSACTION，也可能會發生。  
  
 如果執行階段陳述式錯誤以外的錯誤會阻止外顯交易，在成功完成[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]會自動回復交易並釋放交易所持有的所有資源。 例如，如果執行個體的用戶端的網路連線[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]已中斷或用戶端登出應用程式，在網路通知已中斷的執行個體時，會回復任何未認可的交易的連線。  
  
 如果在批次，就會發生執行階段陳述式錯誤[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]與一致的行為[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **XACT_ABORT**設**ON**和回復整個交易。 如需有關**XACT_ABORT**設定，請參閱[SET XACT_ABORT (TRANSACT-SQL)](http://msdn.microsoft.com/library/ms188792.aspx)。  
  
## <a name="general-remarks"></a>一般備註  
 工作階段只能執行一個交易在指定的時間。不支援儲存點和巢狀的交易。  
  
 它負責[!INCLUDE[DWsql](../../includes/dwsql-md.md)]程式設計人員發出認可點只在交易所參考的所有資料都邏輯正確。  
  
 當工作階段已終止交易完成之前時，會回復交易。  
  
 在工作階段層級管理交易模式。 例如，如果一個工作階段開始明確交易或自動認可設定為 OFF，或將 IMPLICIT_TRANSACTIONS 設為 ON，其不會影響任何其他工作階段的交易模式。  
  
## <a name="limitations-and-restrictions"></a>限制事項  
 您無法回復的交易資料修改已成為資料庫永久的一部分，因為發出 COMMIT 陳述式之後。  
  
 [CREATE DATABASE &#40;Azure SQL 資料倉儲 &#41;](../../t-sql/statements/create-database-azure-sql-data-warehouse.md)和[卸除資料庫 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-database-transact-sql.md)命令不能在明確交易。  
  
 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]沒有共用機制的交易。 這表示，在任何給定的時間點，只有一個工作階段工作的任何交易在系統中。  
  
## <a name="locking-behavior"></a>鎖定行為  
 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]使用鎖定來確保交易完整性，並維護資料庫一致性，當多位使用者同時存取資料，在相同的時間。 鎖定會使用隱含和明確交易。 每一個交易會要求資源，例如資料表或資料庫所需的交易上的不同類型的鎖定。 所有[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]鎖定是層級或更高版本的資料表。 鎖定會阻擋其他交易修改資源，以免造成要求鎖定的交易發生問題。 每一筆交易在它不再具有相依性被鎖定的資源; 時，會釋出它的鎖定外顯交易保留鎖定，直到交易完成時，它會認可或回復。  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-using-an-explicit-transaction"></a>A. 使用明確交易  
  
```  
BEGIN TRANSACTION;  
DELETE FROM HumanResources.JobCandidate  
    WHERE JobCandidateID = 13;  
COMMIT;  
```  
  
### <a name="b-rolling-back-a-transaction"></a>B. 回復交易  
 下列範例顯示回復交易的效果。  在此範例中，ROLLBACK 陳述式將會回復 INSERT 陳述式，但仍會存在建立的資料表。  
  
```  
CREATE TABLE ValueTable (id int);  
BEGIN TRANSACTION;  
       INSERT INTO ValueTable VALUES(1);  
       INSERT INTO ValueTable VALUES(2);  
ROLLBACK;  
```  
  
### <a name="c-setting-autocommit"></a>C. 設定自動認可  
 下列範例會設定自動認可設定`ON`。  
  
```  
SET AUTOCOMMIT ON;  
```  
  
 下列範例會設定自動認可設定`OFF`。  
  
```  
SET AUTOCOMMIT OFF;  
```  
  
### <a name="d-using-an-implicit-multi-statement-transaction"></a>D. 使用多重陳述式，隱含交易  
  
```  
SET AUTOCOMMIT OFF;  
CREATE TABLE ValueTable (id int);  
INSERT INTO ValueTable VALUES(1);  
INSERT INTO ValueTable VALUES(2);  
COMMIT;  
```  
  
## <a name="see-also"></a>另請參閱  
 [SET IMPLICIT_TRANSACTIONS &#40;TRANSACT-SQL &#41;](../../t-sql/statements/set-implicit-transactions-transact-sql.md)   
 [SET TRANSACTION ISOLATION LEVEL &#40;TRANSACT-SQL &#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)   
 [@@TRANCOUNT &#40;Transact-SQL&#41;](../../t-sql/functions/trancount-transact-sql.md)  
  
  
