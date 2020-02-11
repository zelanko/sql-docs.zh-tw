---
title: Deadlock Graph 事件類別 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Deadlock Graph event class
ms.assetid: 20f92233-c912-4382-8993-8e2e23d03fbe
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 741fb8ac694568911c1b2b5def7bd07a8c86e8ec
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62662916"
---
# <a name="deadlock-graph-event-class"></a>Deadlock Graph 事件類別
  「**鎖死圖形**」事件類別提供了鎖死的 XML 描述。 此事件與 **Lock:Deadlock** 事件會同時發生。  
  
## <a name="deadlock-graph-event-class-data-columns"></a>Deadlock Graph 事件類別資料行  
  
|資料行名稱|資料類型|描述|資料行識別碼|可篩選|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**EventClass**|**int**|事件類別 = 148。|27|否|  
|**EventSequence**|**int**|要求中的給定事件順序。|51|否|  
|**IsSystem**|**int**|指出事件是發生在系統處理序或使用者處理序。 1 = 系統，0 = 使用者。 此事件的值永遠為 1。|60|是|  
|**LoginName**|**nvarchar**|使用者的登入名稱（ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安全性登入或「網域 \ 使用者[!INCLUDE[msCoName](../../includes/msconame-md.md)] 」格式的 Windows 登入認證）。 此事件的值永遠為系統使用者。|11|是|  
|**LoginSid**|**image**|已登入之使用者的安全性識別碼 (SID)。 您可以在 sys.server_principals 目錄檢視中找到這項資訊。 伺服器上的每一個登入之 SID 是唯一的。 此事件的值永遠為系統使用者的 SID。|41|是|  
|**ServerName**|**nvarchar**|正在追蹤之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的名稱。|26|否|  
|**SessionLoginName**|**nvarchar**|引發工作階段之使用者的登入名稱。 例如，如果您使用 Login1 連接[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]到，並以 Login2 的身分執行語句，**則 sessionloginname 將**會顯示 Login1，而**LoginName**會顯示 Login2。 此資料行將同時顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 Windows 登入。|64|是|  
|**SPID**|**int**|事件發生所在之工作階段的識別碼。|12|是|  
|**StartTime**|**datetime**|偵測到死結的時間。|14|是|  
|**TextData**|**ntext**|死結的 XML 描述。|1|是|  
|**TransactionID**|**Bigint**|未使用。|4|是|  
  
## <a name="see-also"></a>另請參閱  
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [Lock:Deadlock 事件類別](lock-deadlock-event-class.md)  
  
  
