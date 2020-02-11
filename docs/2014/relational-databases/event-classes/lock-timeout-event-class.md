---
title: Lock:Timeout 事件類別 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Timeout event class
ms.assetid: 8492f4be-4ea9-4059-80e0-9e7b71597da9
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 67f9d89897ef36d297dbeabfffcc02906677cb29
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62663953"
---
# <a name="locktimeout-event-class"></a>Lock:Timeout 事件類別
  Lock:Timeout 事件類別指出資源 (例如分頁) 上的鎖定要求已逾時，因為其他交易在所需資源上已有封鎖的鎖定。 逾時由 @@LOCK_TIMEOUT 系統函式決定，且可使用 SET LOCK_TIMEOUT 陳述式來設定。  
  
 請使用 Lock:Timeout 事件類別來監視發生逾時狀況的時間。 此資訊有助於判斷逾時是否會明顯影響應用程式的效能及包含哪些物件。 您可以檢查修改這些物件的應用程式碼，以判斷是否可以變更來減少逾時。  
  
 持續時間為 0 的 Lock:Timeout 事件通常是內部鎖定探查的結果，並不一定表示有問題。 Lock:Timeout (timeout > 0) 事件可用來忽略持續時間為 0 的逾時。  
  
## <a name="locktimeout-event-class-data-columns"></a>Lock:Timeout 事件類別資料行  
  
|資料行名稱|資料類型|描述|資料行識別碼|可篩選|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|`nvarchar`|建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體之連接的用戶端應用程式名稱。 這個資料行會填入應用程式所傳送的值，而非程式的顯示名稱。|10|是|  
|BinaryData|`image`|鎖定資源識別碼。|2|是|  
|ClientProcessID|`int`|由主機電腦指派給處理序 (用戶端應用程式執行所在) 的識別碼。 如果用戶端提供用戶端處理序識別碼，這個資料行就會擴展。|9|是|  
|DatabaseID|`int`|發生鎖定逾時的資料庫識別碼。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]如果在追蹤中捕捉到 ServerName 資料行，而且伺服器可供使用，則會顯示資料庫的名稱。 請使用 DB_ID 函數判斷資料庫的值。|3|是|  
|DatabaseName|`nvarchar`|發生逾時之資料庫的名稱。|35|是|  
|Duration|`bigint`|在發出鎖定要求和鎖定逾時之間的時間量 (以百萬分之一秒為單位)。|13|是|  
|EndTime|`datetime`|事件結束的時間。|15|是|  
|EventClass|`int`|事件類型 = 27。|27|否|  
|EventSequence|`int`|要求中之給定事件的順序。|51|否|  
|GroupID|`int`|SQL 追蹤事件引發所在之工作負載群組的識別碼。|66|是|  
|HostName|`nvarchar`|執行用戶端的電腦名稱。 如果用戶端提供主機名稱，這個資料行就會擴展。 若要判斷主機名稱，請使用 HOST_NAME 函數。|8|是|  
|IntegerData2|`int`|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|55|是|  
|IsSystem|`int`|指出事件是發生在系統處理序或使用者處理序。 1 = 系統，0 = 使用者。|60|是|  
|LoginName|`nvarchar`|使用者登入的名稱 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全性登入或 DOMAIN\username 格式的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 登入認證)。|11|是|  
|LoginSid|`image`|已登入之使用者的安全性識別碼 (SID)。 您可以在 sys.server_principals 目錄檢視中找到這項資訊。 伺服器上的每一個登入之 SID 是唯一的。|41|是|  
|模式|`int`|逾時之後產生的模式。<br /><br /> 0=NULL - 與其他所有鎖定模式相容 (LCK_M_NL)<br /><br /> 1=結構描述穩定性鎖定 (LCK_M_SCH_S)<br /><br /> 2=結構描述修改鎖定 (LCK_M_SCH_M)<br /><br /> 3=共用鎖定 (LCK_M_S)<br /><br /> 4=更新鎖定 (LCK_M_U)<br /><br /> 5=獨佔鎖定 (LCK_M_X)<br /><br /> 6=意圖共用鎖定 (LCK_M_IS)<br /><br /> 7=意圖更新鎖定 (LCK_M_IU)<br /><br /> 8=意圖獨佔鎖定 (LCK_M_IX)<br /><br /> 9=與意圖更新共用 (LCK_M_SIU)<br /><br /> 10=與意圖獨佔共用 (LCK_M_SIX)<br /><br /> 11=以意圖獨佔更新 (LCK_M_UIX)<br /><br /> 12=大量更新鎖定 (LCK_M_BU)<br /><br /> 13=關鍵範圍共用/共用 (LCK_M_RS_S)<br /><br /> 14=關鍵範圍共用/更新 (LCK_M_RS_U)<br /><br /> 15=關鍵範圍插入 NULL (LCK_M_RI_NL)<br /><br /> 16=關鍵範圍插入共用 (LCK_M_RI_S)<br /><br /> 17=關鍵範圍插入更新 (LCK_M_RI_U)<br /><br /> 18=關鍵範圍插入獨佔 (LCK_M_RI_X)<br /><br /> 19=關鍵範圍獨佔共用 (LCK_M_RX_S)<br /><br /> 20=關鍵範圍獨佔更新 (LCK_M_RX_U)<br /><br /> 21=關鍵範圍獨佔獨佔 (LCK_M_RX_X)|32|是|  
|NTDomainName|`nvarchar`|使用者所隸屬的 Windows 網域。|7|是|  
|NTUserName|`nvarchar`|Windows 使用者名稱。|6|是|  
|ObjectID|`int`|已逾時之物件的識別碼 (如果有且適用的話)。|22|是|  
|ObjectID2|`bigint`|相關物件或實體的識別碼 (如果有且適用的話)。|56|是|  
|OwnerID|`int`|1=TRANSACTION<br /><br /> 2=CURSOR<br /><br /> 3=SESSION<br /><br /> 4=SHARED_TRANSACTION_WORKSPACE<br /><br /> 5=EXCLUSIVE_TRANSACTION_WORKSPACE|58|是|  
|RequestID|`int`|包含陳述式之要求的識別碼。|49|是|  
|ServerName|`nvarchar`|正在追蹤之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的名稱。|26|否|  
|SessionLoginName|`nvarchar`|引發工作階段之使用者的登入名稱。 例如，如果您使用 Login1 連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，並以 Login2 的身分執行陳述式，SessionLoginName 會顯示 Login1，而 LoginName 會顯示 Login2。 此資料行將同時顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 Windows 登入。|64|是|  
|SPID|`int`|事件發生所在之工作階段的識別碼。|12|是|  
|StartTime|`datetime`|事件啟動的時間 (如果有的話)。|14|是|  
|TextData|`ntext`|文字值，視逾時發生時所取得的鎖定類型而定。|1|是|  
|TransactionID|`bigint`|由系統指派給交易的識別碼。|4|是|  
|類型|`int`|1=NULL_RESOURCE<br /><br /> 2=DATABASE<br /><br /> 3=FILE<br /><br /> 5=OBJECT<br /><br /> 6=PAGE<br /><br /> 7=KEY<br /><br /> 8=EXTENT<br /><br /> 9=RID<br /><br /> 10=APPLICATION<br /><br /> 11=METADATA<br /><br /> 12=AUTONAMEDB<br /><br /> 13=HOBT<br /><br /> 14=ALLOCATION_UNIT|57|是|  
  
## <a name="see-also"></a>另請參閱  
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [Lock： Timeout &#40;timeout &#62; 0&#41; 事件類別](lock-timeout-timeout-0-event-class.md)   
 [sys.dm_tran_locks &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql)  
  
  
