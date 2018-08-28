---
title: Audit Database Mirroring Login 事件類別 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- event notifications [SQL Server], database mirroring
- Audit Database Mirroring Login event class
- database mirroring [SQL Server], event notifications
ms.assetid: d0bd436d-aade-4208-a7e5-75cf3b5d0ce9
caps.latest.revision: 16
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 48caa4b54fbf2a7045533bfdc793a1ef1aec9a2e
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43082758"
---
# <a name="audit-database-mirroring-login-event-class"></a>Audit Database Mirroring Login 事件類別
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 建立 **Audit Database Mirroring Login** 事件來報告與資料庫鏡像傳輸安全性有關的稽核訊息。  
  
## <a name="audit-database-mirroring-login-event-class-data-columns"></a>Audit Database Mirroring Login 事件類別資料行  
  
|資料行|類型|Description|資料行編號|可篩選|  
|-----------------|----------|-----------------|-------------------|----------------|  
|**ApplicationName**|**nvarchar**|在此事件類別中未使用。|10|是|  
|**ClientProcessID**|**int**|在此事件類別中未使用。|9|是|  
|**DatabaseID**|**int**|[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 資料行，則 **ServerName** 會顯示資料庫的名稱。 請使用 DB_ID 函數判斷資料庫的值。|3|是|  
|**EventClass**|**int**|擷取的事件類別類型。 **Audit Database Mirroring Login** 永遠是 **154**。|27|否|  
|**EventSequence**|**int**|此事件的序號。|51|否|  
|**EventSubClass**|**int**|事件子類別的類型，針對每個事件類別提供更詳細的相關資訊。 下表列出此事件的事件子類別值。|21|是|  
|**FileName**|**nvarchar**|在遠端資料庫鏡像端點上設定的支援驗證方法。 可用的方法超過一種時，接受 (目標) 端點會判斷要先嘗試哪種方法。 可能的值為：<br /><br /> <br /><br /> **None**： 未設定任何驗證方法。<br /><br /> **NTLM**。 需要 NTLM 驗證。<br /><br /> **KERBEROS**。 需要 Kerberos 驗證。<br /><br /> **NEGOTIATE**。 Windows 會交涉驗證方法。<br /><br /> **CERTIFICATE**。 需要為端點設定的憑證，它是儲存在 **master** 資料庫中。<br /><br /> **NTLM、CERTIFICATE**。 接受使用 NTLM 或端點憑證來進行驗證。<br /><br /> **KERBEROS、CERTIFICATE**。 接受使用 Kerberos 或端點憑證來進行驗證。<br /><br /> **NEGOTIATE、CERTIFICATE**。 由 Windows 交涉要使用的驗證方法，或可以使用端點憑證來進行驗證。<br /><br /> **CERTIFICATE、NTLM**。 接受使用端點憑證或 NTLM 來進行驗證。<br /><br /> **CERTIFICATE、KERBEROS**。 接受使用端點憑證或 Kerberos 來進行驗證。<br /><br /> **CERTIFICATE、NEGOTIATE**。 接受使用端點憑證來進行驗證，或由 Windows 交涉要使用的驗證方法。|36|否|  
|**HostName**|**nvarchar**|在此事件類別中未使用。|8|是|  
|**IsSystem**|**int**|指出事件是發生在系統處理序或使用者處理序。 1 = 系統，0 = 使用者。|60|否|  
|**LoginSid**|**image**|已登入之使用者的安全性識別碼 (SID)。 伺服器上的每一個登入之 SID 是唯一的。|41|是|  
|**NTDomainName**|**nvarchar**|使用者所隸屬的 Windows 網域。|7|是|  
|**NTUserName**|**nvarchar**|擁有產生此事件之連接的使用者名稱。|6|是|  
|**ObjectName**|**nvarchar**|用於此連接的連接字串。|34|否|  
|**OwnerName**|**nvarchar**|在本機資料庫鏡像端點上設定的支援驗證方法。 可用的方法超過一種時，接受 (目標) 端點會判斷要先嘗試哪種方法。 可能的值為：<br /><br /> <br /><br /> **None**： 未設定任何驗證方法。<br /><br /> **NTLM**。 需要 NTLM 驗證。<br /><br /> **KERBEROS**。 需要 Kerberos 驗證。<br /><br /> **NEGOTIATE**。 Windows 會交涉驗證方法。<br /><br /> **CERTIFICATE**。 需要為端點設定的憑證，它是儲存在 **master** 資料庫中。<br /><br /> **NTLM、CERTIFICATE**。 接受使用 NTLM 或端點憑證來進行驗證。<br /><br /> **KERBEROS、CERTIFICATE**。 接受使用 Kerberos 或端點憑證來進行驗證。<br /><br /> **NEGOTIATE、CERTIFICATE**。 由 Windows 交涉要使用的驗證方法，或可以使用端點憑證來進行驗證。<br /><br /> **CERTIFICATE、NTLM**。 接受使用端點憑證或 NTLM 來進行驗證。<br /><br /> **CERTIFICATE、KERBEROS**。 接受使用端點憑證或 Kerberos 來進行驗證。<br /><br /> **CERTIFICATE、NEGOTIATE**。 接受使用端點憑證來進行驗證，或由 Windows 交涉要使用的驗證方法。|37|否|  
|**ProviderName**|**nvarchar**|用於此連接的連接字串。|46|否|  
|**RoleName**|**nvarchar**|連接的角色。 為 **initiator** 或 **target**其中一個角色。|38|否|  
|**ServerName**|**nvarchar**|正在追蹤之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的名稱。|26|否|  
|**SPID**|**int**|由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 指派給用戶端關聯之處理序的伺服器處理序識別碼。|12|是|  
|**StartTime**|**datetime**|事件啟動的時間 (如果有的話)。|14|是|  
|**State**|**int**|指出產生事件的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 原始程式碼內的位置。 每個可能產生此事件的位置都有不同的狀態碼。 Microsoft 支援工程師可以使用此狀態碼來尋找產生事件的位置。|30|否|  
|**TargetUserName**|**nvarchar**|登入狀態。 它是下列項目之一：<br /><br /> **INITIAL**<br /><br /> **WAIT LOGIN NEGOTIATE**<br /><br /> **ONE ISC**<br /><br /> **ONE ASC**<br /><br /> **TWO ISC**<br /><br /> **TWO ASC**<br /><br /> **WAIT ISC Confirm**<br /><br /> **WAIT ASC Confirm**<br /><br /> **WAIT REJECT**<br /><br /> **WAIT PRE-MASTER SECRET**<br /><br /> **WAIT VALIDATION**<br /><br /> **WAIT ARBITRATION**<br /><br /> **ONLINE**<br /><br /> **ERROR**<br /><br /> <br /><br /> 注意：ISC = 起始安全性內容。 ASC = 接受安全性內容。|39|否|  
|**TransactionID**|**bigint**|系統指派的交易識別碼。|4|否|  
  
 下表列出此事件類別的子類別值。  
  
|ID|子類別|Description|  
|--------|--------------|-----------------|  
|@shouldalert|Login Success|Login Success 事件會報告鄰近之資料庫鏡像登入程序已成功完成。|  
|2|Login Protocol Error|Login Protocol Error 事件會報告資料庫鏡像登入收到格式完整，但對於登入程序之目前狀態而言無效的訊息。 此訊息可能已遺失或未按照順序送出。|  
|3|Message Format Error|Message Format Error 事件會報告資料庫鏡像登入已收到不符合預期格式的訊息。 訊息可能已損壞，或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以外的程式正將訊息傳送到資料庫鏡像使用的通訊埠。|  
|4|Negotiate Failure|Negotiate Failure 事件會報告本機資料庫鏡像端點與遠端資料庫鏡像端點支援互斥層級的驗證。|  
|5|Authentication Failure|Authentication Failure 事件會報告資料庫鏡像端點由於錯誤而無法執行連線驗證。 對於 Windows 驗證，此事件會報告資料庫鏡像端點無法使用 Windows 驗證。 對於以憑證為基礎的驗證，此事件會報告資料庫鏡像端點無法存取憑證。|  
|6|Authorization Failure|Authorization Failure 事件會報告資料庫鏡像端點拒絕進行連線驗證。 對於 Windows 驗證，此事件是用以報告連接的安全性識別碼與資料庫使用者不相符。 對於以憑證為基礎的驗證，此事件會報告訊息中傳送的公開金鑰不符合 **master** 資料庫中的憑證。|  
  
## <a name="see-also"></a>另請參閱  
 [CREATE ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/create-endpoint-transact-sql.md)   
 [ALTER ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/alter-endpoint-transact-sql.md)   
 [資料庫鏡像 &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)  
  
  
