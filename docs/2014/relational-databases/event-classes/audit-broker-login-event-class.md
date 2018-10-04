---
title: Audit Broker Login 事件類別 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Audit Broker Login event class
ms.assetid: af9b1153-2791-40ef-a95c-50923cd0cc97
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c9ff2e1adad233d7bee51194858d1cca530bdfdd
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48155278"
---
# <a name="audit-broker-login-event-class"></a>Audit Broker 登入事件類別
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會建立 **Audit Broker Login** 事件，以報告與 Service Broker 傳輸安全性相關的稽核訊息。  
  
## <a name="audit-broker-login-event-class-data-columns"></a>Audit Broker 登入事件類別的資料行  
  
|資料行|類型|描述|資料行編號|可篩選|  
|-----------------|----------|-----------------|-------------------|----------------|  
|**ApplicationName**|**nvarchar**|在此事件類別中未使用。|10|是|  
|**ClientProcessID**|**int**|在此事件類別中未使用。|9|是|  
|**DatabaseID**|**int**|[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 資料行，則 **ServerName** 會顯示資料庫的名稱。 請使用 DB_ID 函數判斷資料庫的值。|3|是|  
|**EventClass**|**int**|擷取的事件類別類型。 **Audit Broker Login** 永遠是 **159**。|27|否|  
|**EventSequence**|**int**|此事件的序號。|51|否|  
|**EventSubClass**|**int**|事件子類別的類型，針對每個事件類別提供更詳細的相關資訊。 下表列出此事件的事件子類別值。|21|是|  
|**FileName**|**nvarchar**|遠端 Broker 驗證層級。 在遠端 Broker 結束點上設定的支援驗證方法。 可用的方法超過一種時，接受 (目標) 端點會判斷要先嘗試哪種方法。 可能的值為：<br /><br /> **None**： 未設定任何驗證方法。<br /><br /> **NTLM**。 需要 NTLM 驗證。<br /><br /> **KERBEROS**。 需要 Kerberos 驗證。<br /><br /> **NEGOTIATE**。 Windows 會交涉驗證方法。<br /><br /> **CERTIFICATE**。 需要為端點設定的憑證，它是儲存在 **master** 資料庫中。<br /><br /> **NTLM、CERTIFICATE**。 接受 NTLM 或 SSL 憑證驗證。<br /><br /> **KERBEROS、CERTIFICATE**。 接受 Kerberos 或結束點憑證驗證。<br /><br /> **NEGOTIATE、CERTIFICATE**。 由 Windows 交涉要使用的驗證方法，或可以使用端點憑證來進行驗證。<br /><br /> **CERTIFICATE、NTLM**。 接受使用端點憑證或 NTLM 來進行驗證。<br /><br /> **CERTIFICATE、KERBEROS**。 接受使用端點憑證或 Kerberos 來進行驗證。<br /><br /> **CERTIFICATE、NEGOTIATE**。 接受用以驗證的結束點憑證或由 Windows 交涉驗證方法。|36|否|  
|**HostName**|**nvarchar**|在此事件類別中未使用。|8|是|  
|**IsSystem**|**int**|指出事件是發生在系統處理序或使用者處理序。 1 = 系統，0 = 使用者。|60|否|  
|**LoginSid**|**image**|已登入之使用者的安全性識別碼 (SID)。 伺服器上的每一個登入之 SID 是唯一的。|41|是|  
|**NTDomainName**|**nvarchar**|使用者所隸屬的 Windows 網域。|7|是|  
|**NTUserName**|**nvarchar**|擁有產生此事件之連接的使用者名稱。|6|是|  
|**ObjectName**|**nvarchar**|用於此連接的連接字串。|34|否|  
|**OwnerName**|**nvarchar**|在本機 Broker 結束點上設定的支援驗證方法。 可用的方法超過一種時，接受 (目標) 端點會判斷要先嘗試哪種方法。 可能的值為：<br /><br /> **None**： 未設定任何驗證方法。<br /><br /> **NTLM**。 需要 NTLM 驗證。<br /><br /> **KERBEROS**。 需要 Kerberos 驗證。<br /><br /> **NEGOTIATE**。 Windows 會交涉驗證方法。<br /><br /> **CERTIFICATE**。 需要為端點設定的憑證，它是儲存在 **master** 資料庫中。<br /><br /> **NTLM、CERTIFICATE**。 接受 NTLM 或 SSL 憑證驗證。<br /><br /> **KERBEROS、CERTIFICATE**。 接受 Kerberos 或結束點憑證驗證。<br /><br /> **NEGOTIATE、CERTIFICATE**。 由 Windows 交涉要使用的驗證方法，或可以使用端點憑證來進行驗證。<br /><br /> **CERTIFICATE、NTLM**。 接受結束點憑證或供 NTLM 驗證之用。<br /><br /> **CERTIFICATE、KERBEROS**。 接受使用端點憑證或 Kerberos 來進行驗證。<br /><br /> **CERTIFICATE、NEGOTIATE**。 接受用以驗證的結束點憑證或由 Windows 交涉驗證方法。|37|否|  
|**ProviderName**|**nvarchar**|此連接所使用的驗證方法|46|否|  
|**RoleName**|**nvarchar**|連接的角色。 為 **initiator** 或 **target**其中一個角色。|38|否|  
|**ServerName**|**nvarchar**|被追蹤的 SQL Server 執行個體名稱。|26|否|  
|**SPID**|**int**|由 SQL Server 指派給用戶端關聯之處理序的伺服器處理序識別碼。|12|是|  
|**StartTime**|**datetime**|事件啟動的時間 (如果有的話)。|14|是|  
|**State**|**int**|指出產生事件的 SQL Server 原始程式碼內的位置。 每個可能產生此事件的位置都有不同的狀態碼。 Microsoft 支援工程師可以使用此狀態碼來尋找產生事件的位置。|30|否|  
|**TargetUserName**|**nvarchar**|登入狀態。 它是下列項目之一：<br /><br /> INITIAL<br /><br /> WAIT LOGIN NEGOTIATE<br /><br /> ONE ISC<br /><br /> ONE ASC<br /><br /> TWO ISC<br /><br /> TWO ASC<br /><br /> WAIT ISC Confirm<br /><br /> WAIT ASC Confirm<br /><br /> WAIT REJECT<br /><br /> WAIT PRE-MASTER SECRET<br /><br /> WAIT VALIDATION<br /><br /> WAIT ARBITRATION<br /><br /> ONLINE<br /><br /> error<br /><br /> **請注意**: ISC = 起始安全性內容。 ASC = Accept Security Context (接受安全性內容)|39|否|  
|**TransactionID**|**bigint**|系統指派的交易識別碼。|4|否|  
  
 下表列出此事件類別的子類別值。  
  
|ID|子類別|描述|  
|--------|--------------|-----------------|  
|1|Login Success|Login Success 事件是用以報告已成功完成相鄰的 Broker 登入處理序。|  
|2|Login Protocol Error|Login Protocol Error 事件是用以報告 Broker 所收到的訊息格式正確，但對於登入處理序目前的狀態無效。 此訊息可能已遺失或未按照順序送出。|  
|3|Message Format Error|Message Format Error 事件是用以報告 Broker 所收到訊息與預期的格式不符。 該訊息可能已損毀，或是 SQL Server 以外的程式可能有傳送訊息給 Service Broker 所使用的通訊埠。|  
|4|Negotiate Failure|Negotiate Failure 事件是用以報告本機 Broker 與遠端 Broker 支援驗證的互斥層級。|  
|5|Authentication Failure|Authentication Failure 事件是用以報告由於發生錯誤，而使 Service Broker 無法執行要連接的驗證。 對於 Windows 驗證而言，此事件是用以報告 Service Broker 無法使用 Windows 驗證。 對於以憑證為基礎的驗證，此事件是用以報告 Service Broker 無法存取憑證。|  
|6|Authorization Failure|Authorization Failure 事件是用以報告 Service Broker 拒絕連接的授權。 對於 Windows 驗證，此事件是用以報告連接的安全性識別碼與資料庫使用者不相符。 對於以憑證為基礎的驗證，此事件是用以報告訊息中所傳遞的公開金鑰與資料庫中的憑證不一致。|  
  
## <a name="see-also"></a>另請參閱  
 [CREATE ENDPOINT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-endpoint-transact-sql)   
 [ALTER ENDPOINT &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-endpoint-transact-sql)   
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)  
  
  
