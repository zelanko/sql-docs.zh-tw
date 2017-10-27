---
title: "決定性與非決定性函式 | Microsoft Docs"
ms.custom: 
ms.date: 08/26/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-udf
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- built-in functions [SQL Server]
- nondeterministic functions
- extended stored procedures [SQL Server], functions that call
- deterministic functions
- user-defined functions [SQL Server], deterministic
ms.assetid: 2f3ce5f5-c81c-4470-8141-8144d4f218dd
caps.latest.revision: 43
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: 8cc1fcfdeae8742a93916dfb08c9db1215f88721
ms.openlocfilehash: 2a25a75485ecfb5bae812b01f142a9650ce2933c
ms.contentlocale: zh-tw
ms.lasthandoff: 10/17/2017

---
# <a name="deterministic-and-nondeterministic-functions"></a>決定性與非決定性函數
  假設資料庫狀態相同，任何時候以特定的輸入值集來呼叫決定性函數時，一律會傳回相同的結果。 即使所存取的資料庫維持在相同的狀態，每次以特定的輸入值集來呼叫非決定性函數時，都會傳回不同的結果。 例如，在上述限定情況下，AVG 函數一律傳回相同的結果，而傳回目前日期時間值的 GETDATE 函數則一律傳回不同的結果。  
  
 無論是透過呼叫函數之計算資料行上的索引，還是透過參考函數的索引檢視，使用者自訂函數都有幾項屬性可決定 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 為函數的結果編製索引的能力。 函數的決定性是這類屬性的一種。 例如，如果檢視參考任何不具決定性的函數，則無法在檢視上建立叢集索引。 如需函數屬性 (包括決定性) 的詳細資訊，請參閱 [使用者定義函數](../../relational-databases/user-defined-functions/user-defined-functions.md)。  
  
 此主題會識別內建系統函數的決定性，以及當使用者自訂函數的具決定性屬性包含擴充預存程序的呼叫時，所造成的影響。  
  
## <a name="built-in-function-determinism"></a>內建函數決定性  
 您無法影響任何內建函數的決定論。 每個內建函數屬於具決定性或不具決定性，主要取決於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]實作函數的方式。 例如，在查詢中指定 ORDER BY 子句不會變更該查詢所使用之函式的決定性。  
  
 所有的字串內建函數都具有決定性。 如需這些函數的清單，請參閱[字串函數 &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)。  
  
 在下列內建函數類別目錄中，不屬於字串函數的內建函數一律會視為具有決定性。  
  
||||  
|-|-|-|  
|ABS|DATEDIFF|POWER|  
|ACOS|DAY|RADIANS|  
|ASIN|DEGREES|ROUND|  
|ATAN|EXP|SIGN|  
|ATN2|FLOOR|SIN|  
|CEILING|ISNULL|SQUARE|  
|COALESCE|ISNUMERIC|SQRT|  
|COS|LOG|TAN|  
|COT|LOG10|YEAR|  
|DATALENGTH|MONTH||  
|DATEADD|NULLIF||  
  
 下列函數並非永遠是具決定性函數，但若是以決定性的方式來指定，則可用於索引檢視表或計算資料行的索引。  
  
|函數|註解|  
|--------------|--------------|  
|所有彙總函式|除非為 OVER 與 ORDER BY 子句所指定，否則所有彙總函式都具有決定性。 如需這些函數的清單，請參閱[彙總函數 &#40;Transact-SQL&#41;](../../t-sql/functions/aggregate-functions-transact-sql.md)。|  
|CAST|除非搭配使用 **datetime**、 **smalldatetime**或 **sql_variant**，否則為決定性函數。|  
|CONVERT|除非存在這些條件之一，否則為具決定性函數：<br /><br /> <br /><br /> 來源類型為 **sql_variant**。<br /><br /> 目標類型為 **sql_variant** ，且其來源類型為非決定性函數。<br /><br /> 來源或目標類型為 **datetime** 或 **smalldatetime**；其他來源或目標類型為字元字串，而且指定了非決定性的樣式。 若要具有決定性，樣式參數必須是常數。 此外，小於或等於 100 的樣式不具決定性，但樣式 20 和 21 除外。 大於 100 的樣式具決定性，但樣式 106、107、109 和 113 除外。|  
|CHECKSUM|具決定性，但 CHECKSUM(*) 除外。|  
|ISDATE|若與 CONVERT 函數一併使用，只有在指定 CONVERT 樣式參數，且樣式不等於 0、100、9 或 109 時，才是具決定性的。|  
|RAND|RAND 只有在指定 *seed* 參數時才是具決定性的。|  
  
 所有的組態、資料指標、中繼資料、安全性及系統統計函數都是不具決定性的。 如需這些函數的清單，請參閱[組態函數 &#40;Transact-SQL&#41;](../../t-sql/functions/configuration-functions-transact-sql.md)、[游標函數 &#40;Transact-SQL&#41;](../../t-sql/functions/cursor-functions-transact-sql.md)、[中繼資料函數 &#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)、[安全性函數 &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md) 和[系統統計函數 &#40;Transact-SQL&#41;](../../t-sql/functions/system-statistical-functions-transact-sql.md)。  
  
 下列屬於其他類別的內建函數，一律是不具決定性的。  
  
|||  
|-|-|  
|@@CONNECTIONS |GETDATE|  
|@@CPU_BUSY |GETUTCDATE|  
|@@DBTS |GET_TRANSMISSION_STATUS|  
|@@IDLE |LAG|  
|@@IO_BUSY |LAST_VALUE|  
|@@MAX_CONNECTIONS |LEAD|  
|@@PACK_RECEIVED |MIN_ACTIVE_ROWVERSION|  
|@@PACK_SENT |NEWID|  
|@@PACKET_ERRORS |NEWSEQUENTIALID|  
|@@TIMETICKS |NEXT VALUE FOR|  
|@@TOTAL_ERRORS |NTILE|  
|@@TOTAL_READ |PARSENAME|  
|@@TOTAL_WRITE |PERCENTILE_CONT|  
|AT TIME ZONE|PERCENTILE_DISC|
|CUME_DIST|PERCENT_RANK|  
|CURRENT_TIMESTAMP|RAND|  
|DENSE_RANK|RANK|  
|FIRST_VALUE|ROW_NUMBER|   
|FORMAT|TEXTPTR|  
  
## <a name="calling-extended-stored-procedures-from-functions"></a>從函數呼叫擴充預存程序  
 呼叫擴充預存程序的函數是不具決定性的，因為擴充預存程序可能對資料庫造成副作用。 副作用是變更資料庫的全域狀態 (例如更新資料表)，或變更檔案或網路這類外部資源 (例如修改檔案或傳送電子郵件訊息)。 從使用者定義函式執行擴充預存程序時，請不要仰賴傳回一致的結果集。 不建議您使用會對資料庫造成副作用的使用者自訂函數。  
  
 從函數內部呼叫時，擴充預存程序無法傳回結果集給用戶端。 將結果集傳回用戶端的任何開放式資料服務 API 都會有 FAIL 傳回碼。  
  
 擴充預存程序不得連回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 而且，程序都無法加入相同的交易成為呼叫擴充預存程序的原始函數。  
  
 類似從批次或預存程序的引動過程，擴充預存程序是在執行 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows 安全帳戶內容中執行。 擴充預存程序的擁有者在授與其他使用者執行該程序的權限時，應考慮此資訊安全內容的權限。  
  
  

