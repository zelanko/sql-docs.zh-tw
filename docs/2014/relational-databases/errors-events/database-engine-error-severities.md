---
title: Database Engine 錯誤嚴重性 | Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- user-defined error messages [SQL Server]
- severity levels [SQL Server]
- retrieving error severity
- errors [SQL Server], severity
- TRY...CATCH [SQL Server]
ms.assetid: 3e7f5925-6edd-42e1-bf17-f7deb03993a7
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9de758c6a54ca1993efc8873a02293331a129b33
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52529702"
---
# <a name="database-engine-error-severities"></a>Database Engine 錯誤嚴重性
  當 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]產生錯誤時，錯誤的嚴重性會指出 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]所發生的問題類型。  
  
## <a name="levels-of-severity"></a>嚴重性層級  
 下表列出和描述 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]所產生之錯誤的嚴重性層級。  
  
|嚴重性層級|描述|  
|--------------------|-----------------|  
|0-9|傳回狀態資訊或報告不嚴重之錯誤的參考訊息。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 不會產生嚴重性 0-9 的系統錯誤。|  
|10|傳回狀態資訊或報告不嚴重之錯誤的參考訊息。 基於相容性考量， [!INCLUDE[ssDE](../../includes/ssde-md.md)] 會先將嚴重性 10 轉換成嚴重性 0，再將錯誤資訊傳回給發出呼叫的應用程式。|  
|11-16|指出使用者能夠更正的錯誤。|  
|11|指出給定的物件或實體不存在。|  
|12|因特殊查詢提示而不使用鎖定之查詢的特殊嚴重性。 在某些情況下，這些陳述式所執行的讀取作業可能會產生不一致的資料，因為並沒有採取鎖定來保證一致性。|  
|13|指出交易死結錯誤。|  
|14|指出與安全性相關的錯誤，例如，沒有權限。|  
|15|指出 [!INCLUDE[tsql](../../includes/tsql-md.md)] 命令的語法錯誤。|  
|16|指出使用者能夠更正的一般錯誤。|  
|17-19|指出使用者無法更正的軟體錯誤。 請通知系統管理員這個問題。|  
|17|指出陳述式使 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 將資源 (如記憶體、鎖定，或資料庫的磁碟空間) 用完，或超出系統管理員所設定的某項限制。|  
|18|指出 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 軟體發生問題，但陳述式執行完成，且 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體的連接也得到維護。 每當出現嚴重性層級 18 的訊息時，都應該通知系統管理員。|  
|19|指出超出不可設定的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 限制，已終止目前的批次處理序。 嚴重性層級 19 或以上的錯誤訊息，會停止執行目前的批次。 嚴重性層級 19 的錯誤很少，必須由系統管理員或主要支援提供者來更正。 當出現嚴重性層級 19 的訊息時，請連絡您的系統管理員。 嚴重性層級 19-25 的錯誤訊息會寫入錯誤記錄中。|  
|20-24|指出系統問題，這些都是嚴重錯誤，表示執行陳述式或批次的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 工作已不在執行中。 工作會將發生情況的相關資訊記錄下來，再終止作業。 在大部份的情況下，通往 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體的應用程式連接也會終止。 如果發生這個情況，隨著問題而不同，應用程式可能會無法重新連接。<br /><br /> 這個範圍的錯誤訊息可能會影響所有存取相同資料庫之資料的處理序，且可能表示資料庫或物件已經損毀。 嚴重性層級 19-24 的錯誤訊息會寫入錯誤記錄中。|  
|20|指出陳述式發生問題。 由於問題只影響到目前的工作，因此，資料庫本身可能並沒有損毀。|  
|21|指出發生影響目前資料庫中所有工作的問題，但資料庫本身可能並沒有損毀。|  
|22|指出軟體或硬體問題已損毀訊息所指定的資料表或索引。<br /><br /> 嚴重性層級 22 的錯誤很少發生。 如果發生，請執行 DBCC CHECKDB 來判斷資料庫中的其他物件是否也已損毀。 可能只有緩衝快取發生問題，磁碟本身並沒有問題。 若是如此，重新啟動 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體便可以更正這個問題。 若要繼續作業，您必須重新連接 [!INCLUDE[ssDE](../../includes/ssde-md.md)]執行個體；否則，請利用 DBCC 來修復問題。 在某些情況下，您可能需要還原資料庫。<br /><br /> 如果重新啟動 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體仍未更正這個問題，就表示磁碟發生問題。 有時終結錯誤訊息所指定的物件可以解決這個問題。 例如，如果訊息報告 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體在非叢集索引中找到長度是 0 的資料列，請刪除這個索引，再重建它。|  
|23|指出由於硬體或軟體發生問題，因此，整個資料庫的完整性有問題。<br /><br /> 嚴重性層級 23 的錯誤很少發生。 如果發生，請執行 DBCC CHECKDB 來判斷損毀的範圍。 可能只有快取發生問題，磁碟本身並沒有問題。 若是如此，重新啟動 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體便可以更正這個問題。 若要繼續作業，您必須重新連接 [!INCLUDE[ssDE](../../includes/ssde-md.md)]執行個體；否則，請利用 DBCC 來修復問題。 在某些情況下，您可能需要還原資料庫。|  
|24|指出媒體失敗。 系統管理員可能需要還原資料庫。 您也可能需要電洽您的硬體廠商。|  
  
## <a name="user-defined-error-message-severity"></a>使用者自訂的錯誤訊息嚴重性  
 您可以利用**sp_addmessage** ，將嚴重性 1-25 的使用者自訂錯誤訊息加入 **sys.messages** 目錄檢視中。 RAISERROR 可以使用這些使用者自訂的錯誤訊息。 如需詳細資訊，請參閱 [sp_addmessage &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmessage-transact-sql)。  
  
 RAISERROR 可以用來產生使用者定義的錯誤訊息，其嚴重性為 1 到 25。 RAISERROR 可以參考儲存在 **sys.messages** 目錄檢視的使用者定義錯誤訊息，或是動態建立訊息。 當在產生錯誤時使用 **sys.messages** 中的使用者自訂錯誤訊息，RAISERROR 指定的嚴重性會覆寫 **sys.messages** 所指定的嚴重性。 如需詳細資訊，請參閱 [RAISERROR &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/raiserror-transact-sql)。  
  
## <a name="error-severity-and-trycatch"></a>錯誤嚴重性和 TRY...CATCH  
 TRY...CATCH 建構會捕捉嚴重性大於 10 而並未終止資料庫連接的所有執行錯誤。  
  
 嚴重性 0-10 的錯誤是資訊訊息，不會使執行動作跳出 TRY...CATCH 建構的 CATCH 區塊。  
  
 CATCH 區塊不會處理嚴重性通常是 20-25 的終止資料庫連接的錯誤，因為在連接終止時，會中止執行動作。  
  
 如需詳細資訊，請參閱 [TRY...CATCH &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/try-catch-transact-sql)所發生的問題類型。  
  
## <a name="retrieving-error-severity"></a>擷取錯誤嚴重性  
 您可以利用 ERROR_SEVERITY 系統函式來擷取造成執行 TRY...CATCH 建構的 CATCH 區塊之錯誤的嚴重性。 如果是在 CATCH 區塊範圍之外呼叫，ERROR_SEVERITY 會傳回 NULL。 如需詳細資訊，請參閱 [ERROR_SEVERITY &#40;Transact-SQL&#41;](/sql/t-sql/functions/error-severity-transact-sql)。  
  
## <a name="see-also"></a>另請參閱  
 [了解 Database Engine 錯誤](../native-client-ole-db-errors/errors.md)   
 [sys.messages &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages)   
 [系統函數 &#40;Transact-SQL&#41;](/sql/t-sql/functions/system-functions-transact-sql)   
 [TRY...CATCH &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/try-catch-transact-sql)  
  
  
