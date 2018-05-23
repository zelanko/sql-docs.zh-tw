---
title: Hash Warning 事件類別 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Hash Warning event class
ms.assetid: cb93c620-4be9-4362-8bf0-af3f2048bdaf
caps.latest.revision: 39
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: add64ff3832d95c4a16a097a22f420423c1dc09c
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2018
---
# <a name="hash-warning-event-class"></a>Hash Warning 事件類別
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Hash Warning 事件類別可用來監視在雜湊作業期間發生雜湊遞迴或雜湊停止 (Hash Bailout) 的時間。  
  
 當建立輸入不符合可用記憶體時，會發生雜湊遞迴，因而將輸入分割為多個需要個別處理的資料分割。 如果這些資料分割中仍有任何資料分割不符合可用記憶體，則這些資料分割會再分為子資料分割，仍是需要個別處理。 這個分割處理會繼續進行，直到每個資料分割都符合可用記憶體或達到最大遞迴等級為止 (顯示於 IntegerData 資料行)。  
  
 當雜湊作業達到最大遞迴等級時會發生 Hash Bailout，且切換到其他計畫以處理其他的分割資料。 發生 Hash Bailout 是因為資料的誤用。  
  
 雜湊遞迴和 Hash Bailout 會導致伺服器的效能降低。 若要刪除或降低雜湊遞迴和釋出的頻率，請執行下列其中之一：  
  
-   確定在已聯結或已分組的資料行上存在統計資料。  
  
-   如果資料行上存在統計資料，請加以更新。  
  
-   使用不同的聯結類型。 例如，如果適用，請改用 MERGE 或 LOOP 聯結。  
  
-   在電腦上增加可用記憶體。 如果沒有足夠的記憶體可以直接處理詢問，且需要溢出至磁碟時，就會發生雜湊釋出或遞迴。  
  
 建立或更新資料行 (包含在聯結中) 上的統計資料，是降低發生雜湊遞迴或釋出次數最有效的方法。  
  
> [!NOTE]  
>  詞彙「寬限雜湊聯結」和「遞迴雜湊聯結」也可用來說明 Hash Bailout。  
  
> [!IMPORTANT]  
>  若要決定查詢最佳化工具產生執行計畫時發生 Hash Warning 事件的位置，您也應在追蹤中收集顯示計畫事件類別。 您可選擇任何 Showplan 事件類別，但是不包含不會傳回節點識別碼的 Showplan Text 及 Showplan Text (未編碼) 事件類別。 Showplan 中的節點識別碼會識別查詢最佳化工具在產生查詢執行計畫時所執行的每項作業。 這些作業稱為「運算子」，而 Showplan 中的每個運算子都會有節點識別碼。 Hash Warning 事件的 ObjectID 資料行都會對應到 Showplan 中的節點識別碼，因此您可以判斷造成錯誤的運算子或運算。  
  
## <a name="hash-warning-event-class-data-columns"></a>Hash Warning Event 事件類別資料行  
  
|資料行名稱|資料類型|描述|資料行識別碼|可篩選|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|**nvarchar**|建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體之連接的用戶端應用程式名稱。 這個資料行會填入應用程式所傳送的值，而非程式的顯示名稱。|10|是|  
|ClientProcessID|**int**|由主機電腦指派給處理序 (用戶端應用程式執行所在) 的識別碼。 若用戶端有提供用戶端處理序識別碼，就會填入此資料行。|9|是|  
|DatabaseID|**int**|由 USE *database* 陳述式所指定的資料庫識別碼，或者如果沒有針對指定執行個體發出 USE *database* 陳述式，則是預設的資料庫。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 如果在追蹤中擷取 ServerName 資料行，則會顯示資料庫的名稱。 請使用 DB_ID 函數判斷資料庫的值。|3|是|  
|DatabaseName|**nvarchar**|正在執行使用者陳述式的資料庫名稱。|35|是|  
|EventClass|**int**|事件類型 = 55。|27|否|  
|EventSequence|**int**|要求中的給定事件順序。|51|否|  
|EventSubClass|**int**|事件子類別的類型。<br /><br /> 0=遞迴<br /><br /> 1=釋出|21|是|  
|GroupID|**int**|SQL 追蹤事件引發所在之工作負載群組的識別碼。|66|是|  
|HostName|**nvarchar**|執行用戶端的電腦名稱。 如果用戶端提供主機名稱，這個資料行就會擴展。 若要判斷主機名稱，請使用 HOST_NAME 函數。|8|是|  
|IntegerData|**int**|遞迴等級 (僅限雜湊遞迴)。|25|是|  
|IsSystem|**int**|指出事件是發生在系統處理序或使用者處理序。 1 = 系統，0 = 使用者。|60|是|  
|LoginName|**nvarchar**|使用者登入的名稱 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全性登入或 *\<網域>\\<使用者名稱\>* 格式的 Windows 登入認證)。|11|是|  
|LoginSid|**image**|已登入之使用者的安全性識別碼 (SID)。 您可以在 sys.server_principals 目錄檢視中找到這項資訊。 伺服器上的每一個登入之 SID 是唯一的。|41|是|  
|NTDomainName|**nvarchar**|使用者所隸屬的 Windows 網域。|7|是|  
|NTUserName|**nvarchar**|Windows 使用者名稱。|6|是|  
|ObjectID|**int**|在重新分割中，雜湊群根節點的節點識別碼。 與顯示計畫中的節點識別碼相對應。|22|是|  
|RequestID|**int**|包含陳述式之要求的識別碼。|49|是|  
|ServerName|**nvarchar**|所追蹤之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的名稱。|26||  
|SessionLoginName|**nvarchar**|引發工作階段之使用者的登入名稱。 例如，如果您使用 Login1 連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，並以 Login2 身分執行陳述式，則 SessionLoginName 將顯示 Login1 而 LoginName 則顯示 Login2。 此資料行將同時顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 Windows 登入。|64|是|  
|SPID|**int**|事件發生所在之工作階段的識別碼。|12|是|  
|StartTime|**datetime**|事件啟動的時間 (如果有的話)。|14|是|  
|TransactionID|**bigint**|由系統指派給交易的識別碼。|4|是|  
|XactSequence|**bigint**|描述目前交易的 Token。|50|是|  
  
## <a name="see-also"></a>另請參閱  
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)    
 [聯結](../../relational-databases/performance/joins.md)    
  
  
