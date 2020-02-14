---
title: SQL Server 的 SQL Statistics 物件 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:SQL Statistics
- SQL Statistics object
ms.assetid: da7dbb4b-f632-45a0-b1ab-c35cc2695c86
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 7841fef89ae4eb0600dcc62c1561bff769500a47
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "67995658"
---
# <a name="sql-server-sql-statistics-object"></a>SQL Server 的 SQL Statistics 物件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **的** SQLServer:SQL Statistics [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物件會提供計數器，可用來監視編譯以及傳送給 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的要求類型。 監視查詢編譯和重新編譯的次數，以及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體所收到的批次數目，可讓您了解 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 處理使用者查詢的速度，以及查詢最佳化工具處理查詢的效率。  
  
 編譯是查詢回覆速度的重要部份。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 為了節省編譯成本，會將編譯過的查詢計畫儲存在查詢快取中。 快取的目標是減少編譯，透過儲存編譯過的查詢以供日後重複使用，以後執行時便可以省去重新編譯查詢的步驟。 不過，每個不同的查詢至少都需要編譯一次。 下列因素均可能導致查詢重新編譯：  
  
-   結構描述變更，包括基底結構描述變更，例如將資料行或索引加入資料表，或統計資料結構描述變更，例如在資料表內插入或刪除大量的資料列。  
  
-   環境 (SET 陳述式) 變更。 工作階段設定的變更，例如 ANSI_PADDING 或 ANSI_NULLS 可能導致查詢重新編譯。  
  
 如需簡單參數化與強制參數化的詳細資訊，請參閱 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)。  
  
 以下是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **SQL Statistics** 計數器。  
  
|SQL Server SQL Statistics 計數器|描述|  
|----------------------------------------|-----------------|  
|**Auto-Param Attempts/sec**|每秒的自動參數化嘗試次數。 此總數應該是所有失敗的、安全的與不安全的自動參數化之總和。 當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體嘗試以參數來取代部份常值，以將 [!INCLUDE[tsql](../../includes/tsql-md.md)] 要求參數化時，就會發生自動參數化；如此將可以在多個相似的要求中，重複使用所產生的快取執行計畫。 請注意，自動參數化在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]更新版本中也稱為簡單參數化。 此計數器不包含強制參數化。|  
|**Batch Requests/sec**|每秒接收的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 命令批次數目。 此統計資料受到所有條件約束的影響 (例如 I/O、使用者數目、快取大小、要求複雜性等)， 批次要求數目大，表示輸送量高。|  
|**Failed Auto-Params/sec**|每秒失敗的自動參數化嘗試。 這應該很小。 請注意，自動參數化在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]更新版本中也稱為簡單參數化。|  
|**Forced Parameterizations/sec**|每秒成功的強制參數化次數。|  
|**Guided Plan Executions/sec**|每秒計畫執行的次數 (已經使用計畫指南產生查詢計畫)。|  
|**Misguided Plan Executions/sec**|每秒計畫執行的次數 (在計畫產生期間無法接受計畫指南)。 計畫指南已被忽略而且使用一般編譯來產生執行的計畫。|  
|**Safe Auto-Params/sec**|每秒的安全自動參數化嘗試。 「安全」是一項判斷，認定可在不同但相似的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式之間共用快取執行計畫。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可進行多項自動參數化嘗試，當中有些是安全的，有些是失敗的。 請注意，自動參數化在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]更新版本中也稱為簡單參數化。 此項目不包含強制參數化。|  
|**SQL Attention rate**|每秒的注意事項數目。 注意事項是用戶端的要求，用來結束目前執行中的要求。|  
|**SQL Compilations/sec**|每秒的 SQL 編譯次數， 表示輸入編譯程式碼路徑的次數。 包括 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中由陳述式層級的重新編譯所造成的編譯。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用者活動穩定之後，此值會達到一個穩定的狀態。|  
|**SQL Re-Compilations/sec**|每秒的陳述式重新編譯次數， 此值計算觸發陳述式重新編譯的次數。 通常，您會希望重新編譯的次數降低。|  
|**Unsafe Auto-Params/sec**|每秒不安全的自動參數化嘗試次數。 例如，查詢具有一些特性，會阻止共用快取計畫。 這些特性就稱為不安全的。 強制參數化的次數不算在內。|  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 的 Plan Cache 物件](../../relational-databases/performance-monitor/sql-server-plan-cache-object.md)   
 [監視資源使用狀況 &#40;System Monitor&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
