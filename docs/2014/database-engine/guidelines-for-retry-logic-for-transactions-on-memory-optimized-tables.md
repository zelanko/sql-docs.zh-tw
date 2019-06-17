---
title: 記憶體最佳化資料表交易的重試邏輯的指導方針 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: f2a35c37-4449-49ee-8bba-928028f1de66
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 01f719470419940b130967b7c1360c4ae0c281eb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62779212"
---
# <a name="guidelines-for-retry-logic-for-transactions-on-memory-optimized-tables"></a>記憶體最佳化資料表交易的重試邏輯方針
  存取記憶體最佳化資料表的交易會產生一些錯誤狀況。  
  
-   41302. 目前交易嘗試更新自從此交易啟動以來已經更新的記錄。  
  
-   41305. 目前的交易無法認可，因為可重複的讀取驗證失敗。  
  
-   41325. 目前的交易無法認可，因為可序列化驗證失敗。  
  
-   41301. 目前交易具有相依性的先前交易已經中止，而且目前交易無法再認可。  
  
 這些錯誤的常見原因是同時執行中交易之間的干擾。 常見的更正動作是重試交易。  
  
 如需有關這些錯誤狀況的詳細資訊，請參閱衝突偵測、 驗證和認可相依性檢查在[Transactions in Memory-Optimized Tables](../relational-databases/in-memory-oltp/memory-optimized-tables.md)。  
  
 記憶體最佳化的資料表不能發生死結 (錯誤碼 1205)。 鎖定未用於記憶體最佳化的資料表。 不過，如果應用程式已經包含死結的重試邏輯，現有邏輯可擴充成包含新的錯誤碼。  
  
## <a name="considerations-for-retrying"></a>重試考量  
 應用程式通常會發生交易之間的衝突，而需要實作重試邏輯以解決這些衝突。 遇到的衝突數目取決於一些因素：  
  
-   個別資料列的競爭。 隨著嘗試更新相同資料列的交易數目增加，發生衝突的可能性也會增加。  
  
-   REPEATABLE READ 交易讀取的資料列數目。 讀取的資料列愈多，並行交易更新其中一些資料列的可能性愈大。 這會造成可重複的讀取驗證失敗。  
  
-   SERIALIZABLE 交易使用的掃描範圍大小。 掃描範圍愈大，並行交易導入虛設項目列，造成可序列化驗證失敗的機率愈高。  
  
     應用程式難以避免這些衝突，因此需要重試邏輯。  
  
> [!IMPORTANT]  
>  存取記憶體最佳化資料表的讀取/寫入交易需要重試邏輯。  
  
### <a name="considerations-for-read-only-transactions-and-natively-compiled-stored-procedures"></a>唯讀交易和原生編譯預存程序的考量  
 跨越原生編譯預存程序單次執行的唯讀交易不需要 REPEATABLE READ 和 SERIALIZABLE 交易驗證。 因為交易是唯讀，寫入衝突不會發生。  
  
 不過，相依性失敗可能仍然發生。 相依性失敗比因衝突所導致的錯誤更少見。 因此，在大部分情況下，跨越原生編譯預存程序單次執行的唯讀交易不需要特定重試邏輯。  
  
### <a name="considerations-for-read-only-transactions-and-cross-container-transactions"></a>唯讀交易和跨容器交易的考量  
 唯讀跨容器交易是在原生編譯預存程序的內容之外開始，如果記憶體最佳化的資料表都是在 SNAPSHOT 隔離下存取，這類交易不會執行驗證。 不過，當記憶體最佳化的資料表是在 REPEATABLE READ 或 SERIALIZABLE 隔離下存取時，在認可時會執行驗證。 在此情況下，可能需要重試邏輯。  
  
 如需詳細資訊，請參閱一節上中的跨容器交易[交易隔離等級](../../2014/database-engine/transaction-isolation-levels.md)。  
  
## <a name="implementing-retry-logic"></a>實作重試邏輯  
 如同存取記憶體最佳化資料表的所有交易，您必須考慮重試邏輯以處理潛在的失敗，例如寫入衝突 (錯誤碼 41302) 或相依性失敗 (錯誤碼 41301)。 在多數應用程式中的失敗率都很低，不過仍然必須透過重試交易處理失敗。 兩個實作重試邏輯的建議方式如下：  
  
-   用戶端重試。 在一般情況中，用戶端重試是較適合實作重試邏輯的方式。 用戶端應用程式會擷取交易擲出的錯誤，然後重試交易。 若現有的用戶端應用程式有處理死結的重試邏輯，您可以擴充應用程式以處理新的錯誤碼。  
  
-   使用包裝函式預存程序。 用戶端會呼叫解譯的 [!INCLUDE[tsql](../includes/tsql-md.md)] 預存程序，其會呼叫原生編譯的預存程序或執行交易。 包裝函式程序會隨後視需要使用 try/catch 邏輯，擷取錯誤及重試程序呼叫。 這可能會在失敗前將該結果傳回用戶端，而且用戶端不會知道要將其捨棄。 因此，為了安全起見，最好只搭配不傳回任何結果集至用戶端的原生編譯預存程序來使用此方法。  
  
 重試邏輯可在 [!INCLUDE[tsql](../includes/tsql-md.md)] 中或在中間層的應用程式程式碼中實作。  
  
 考慮重試邏輯的兩個可能原因如下：  
  
-   用戶端應用程式有其他錯誤碼 (例如 1205) 的重試邏輯，這些錯誤碼是可擴充的。  
  
-   衝突很少，而使用備妥的執行，減少端對端延遲很重要。 如需有關原生執行直接編譯預存程序，請參閱 < [Natively Compiled Stored Procedures](../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)。  
  
 下列範例示範解譯的 [!INCLUDE[tsql](../includes/tsql-md.md)] 預存程序中的重試邏輯，該預存程序包含原生編譯預存程序或跨容器交易的呼叫。  
  
```sql  
CREATE PROCEDURE usp_my_procedure @param1 type1, @param2 type2, ...  
AS  
BEGIN  
  -- number of retries - tune based on the workload  
  DECLARE @retry INT = 10  
  
  WHILE (@retry > 0)  
  BEGIN  
    BEGIN TRY  
  
      -- exec usp_my_native_proc @param1, @param2, ...  
  
      --       or  
  
      -- BEGIN TRANSACTION  
      --   ...  
      -- COMMIT TRANSACTION  
  
      SET @retry = 0  
    END TRY  
    BEGIN CATCH  
      SET @retry -= 1  
  
      -- the error number for deadlocks (1205) does not need to be included for   
      -- transactions that do not access disk-based tables  
      IF (@retry > 0 AND error_number() in (41302, 41305, 41325, 41301, 1205))  
      BEGIN  
        -- these error conditions are transaction dooming - rollback the transaction  
        -- this is not needed if the transaction spans a single native proc execution  
        --   as the native proc will simply rollback when an error is thrown   
        IF XACT_STATE() = -1  
          ROLLBACK TRANSACTION  
  
        -- use a delay if there is a high rate of write conflicts (41302)  
        --   length of delay should depend on the typical duration of conflicting transactions  
        -- WAITFOR DELAY '00:00:00.001'  
      END  
      ELSE  
      BEGIN  
        -- insert custom error handling for other error conditions here  
  
        -- throw if this is not a qualifying error condition  
        ;THROW  
      END  
    END CATCH  
  END  
END  
```  
  
## <a name="see-also"></a>另請參閱  
 [了解記憶體最佳化資料表上的交易](../../2014/database-engine/understanding-transactions-on-memory-optimized-tables.md)   
 [記憶體最佳化資料表中的交易](../relational-databases/in-memory-oltp/memory-optimized-tables.md)   
 [搭配經記憶體最佳化的資料表使用交易隔離等級的方針](../../2014/database-engine/guidelines-for-transaction-isolation-levels-with-memory-optimized-tables.md)  
  
  
