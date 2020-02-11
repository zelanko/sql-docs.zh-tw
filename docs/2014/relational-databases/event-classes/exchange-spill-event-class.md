---
title: Exchange Spill 事件類別 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Exchange Spill event class
ms.assetid: fb876cec-f88d-4975-b3fd-0fb85dc0a7ff
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0220e81325345e84524ec0218dbaff7d6143bdd8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62663654"
---
# <a name="exchange-spill-event-class"></a>Exchange Spill 事件類別
  **Exchange Spill** 事件類別指出平行查詢計劃中的通訊緩衝區，已暫時寫入 **tempdb** 資料庫。 這種情況並不常見，只有在查詢計畫有多重範圍掃描時才會發生。  
  
 通常，產生這類範圍掃描的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查詢，會有多個 BETWEEN 運算子，而每個運算子都會選取資料表中某個範圍的資料列，或選取某個索引。 或者，您可以使用像是（T. a > 10 和 T. \< 20）或（t. a > 100 和 t. \< 120）的運算式來取得多個範圍。 此外，查詢計畫一定需要依序掃描這些範圍，這是因為 T.a 上有 ORDER BY 子句，或是計畫中有 Iterator，因此必須以排序順序取用 Tuple 所致。  
  
 當這類查詢的查詢計劃有多個 **Parallelism** 運算子時，由 **Parallelism** 運算子所使用的記憶體通訊緩衝區將會變滿，因而發生查詢執行進度停止的情況。 這時候，其中一個 **Parallelism** 運算子會將它的輸出緩衝區寫入 **tempdb** (此作業稱為 *Exchange Spill*)，以便從它的部分輸入緩衝區取用資料列。 最後，等到取用者有餘力取用時，轉散出去的資料列就會傳回給取用者。  
  
 在極少數的情況下，同一個執行計畫內會發生多次交換轉散，因而導致查詢執行速度降低。 如果您發現同一個查詢計畫執行內發生超過五次的交換轉散，請連絡您的技術支援人員。  
  
 交換轉散有時候是暫時的，只要資料分佈情況一有變更就會消失。  
  
 您可以用以下方式來避免交換轉散事件：  
  
-   如果您不需要將結果集排序，請省略 ORDER BY 子句。  
  
-   如果必須使用 ORDER BY，請從 ORDER BY 子句中刪除參與多重範圍掃描 (例如上述範例中的 T.a) 的資料行。  
  
-   使用索引提示，強制最佳化工具在有問題的資料表上使用不同的存取路徑。  
  
-   重寫查詢，以產生不同的查詢執行計畫。  
  
-   將 MAXDOP = 1 選項加入查詢結尾或索引作業，以強制進行查詢的序列執行。 如需詳細資訊，請參閱 [設定 max degree of parallelism 伺服器組態選項](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md) 和 [設定平行索引作業](../indexes/configure-parallel-index-operations.md)。  
  
> [!IMPORTANT]  
>  若要判斷查詢最佳化工具產生執行計畫時發生 **Exchange Spill** 事件的位置，您也應在追蹤內收集 Showplan 事件類別。 您可以選擇任何 Showplan 事件類別，但是不包含不會傳回節點識別碼的 **Showplan Text** 及 **Showplan Text (Unencoded)** 事件類別。 Showplan 中的節點識別碼會識別查詢最佳化工具在產生查詢執行計畫時所執行的每項作業。 這些作業稱為「運算子」(Operator)，而 Showplan 中的每個運算子都會有節點識別碼。 **Exchange Spill** 事件類別的 **ObjectID** 資料行會對應到執行程序表中的節點識別碼，因此您可以判斷造成錯誤的運算子或運算。  
  
## <a name="exchange-spill-event-class-data-columns"></a>Exchange Spill 事件類別資料行  
  
|資料行名稱|資料類型|描述|資料行識別碼|可篩選|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**ApplicationName**|**nvarchar**|建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體之連接的用戶端應用程式名稱。 這個資料行會填入應用程式所傳送的值，而非程式的顯示名稱。|10|是|  
|**ClientProcessID**|**int**|由主機電腦指派給處理序 (用戶端應用程式執行所在) 的識別碼。 如果用戶端提供用戶端處理序識別碼，這個資料行就會擴展。|9|是|  
|**DatabaseID**|**int**|由 USE *database* 陳述式所指定的資料庫識別碼，或者如果沒有針對指定執行個體發出 USE *database* 陳述式，則是預設的資料庫。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 資料行，則 **ServerName** 會顯示資料庫的名稱。 請使用 DB_ID 函數判斷資料庫的值。|3|是|  
|**DatabaseName**|**nvarchar**|正在執行使用者陳述式的資料庫名稱。|35|是|  
|**EventClass**|**int**|事件類型 = 127。|27|否|  
|**EventSequence**|**int**|要求中的給定事件順序。|51|否|  
|**EventSubClass**|**int**|事件子類別的類型。<br /><br /> 1=開始轉散<br /><br /> 2=結束轉散|21|是|  
|**GroupID**|**int**|SQL 追蹤事件引發所在之工作負載群組的識別碼。|66|是|  
|**HostName**|**nvarchar**|執行用戶端的電腦名稱。 如果用戶端提供主機名稱，這個資料行就會擴展。 若要判斷主機名稱，請使用 HOST_NAME 函數。|8|是|  
|**IsSystem**|**int**|指出事件是發生在系統處理序或使用者處理序。 1 = 系統，0 = 使用者。|60|是|  
|**LoginName**|**nvarchar**|使用者登入的名稱 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全性登入或 *\<網域>\\<使用者名稱\>* 格式的 Windows 登入認證)。|11|是|  
|**LoginSid**|**image**|已登入之使用者的安全性識別碼 (SID)。 您可以在 **master** 資料庫的 **syslogins** 資料表中找到這項資訊。 伺服器上的每一個登入之 SID 是唯一的。|41|是|  
|**NTDomainName**|**nvarchar**|使用者所隸屬的 Windows 網域。|7|是|  
|**NTUserName**|**nvarchar**|Windows 使用者名稱。|6|是|  
|**Exchange Spill**|**int**|系統指派給物件的識別碼。 與顯示計畫中的節點識別碼相對應。|22|是|  
|**RequestID**|**int**|包含陳述式之要求的識別碼。|49|是|  
|**ServerName**|**nvarchar**|正在追蹤之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的名稱。|26|否|  
|**SessionLoginName**|**nvarchar**|引發工作階段之使用者的登入名稱。 例如，如果您使用 Login1 連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，並以 Login2 執行陳述式，則 **SessionLoginName** 將顯示 Login1 而 **LoginName** 則顯示 Login2。 此資料行將同時顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 Windows 登入。|64|是|  
|**SPID**|**int**|事件發生所在之工作階段的識別碼。|12|是|  
|**StartTime**|**datetime**|事件啟動的時間 (如果有的話)。|14|是|  
|**TransactionID**|**bigint**|由系統指派給交易的識別碼。|4|是|  
|**XactSequence**|**bigint**|描述目前交易的 Token。|50|是|  
  
## <a name="see-also"></a>另請參閱  
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [設定索引選項](../indexes/set-index-options.md)   
 [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql)  
  
  
