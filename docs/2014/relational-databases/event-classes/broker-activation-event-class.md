---
title: Broker:Activation 事件類別 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Broker:Activation event class
ms.assetid: 481d5b13-657e-4b51-8783-ccac3595bd45
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f2562f3931f98c040bb3dc475e3863bb6396dbbf
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52752870"
---
# <a name="brokeractivation-event-class"></a>Broker:Activation 事件類別
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 當佇列監視器啟動一個啟用預存程序、傳送 QUEUE_ACTIVATION 通知或佇列監視器所啟動的一個啟用預存程序結束時，會產生 **Broker:Activation** 事件。  
  
## <a name="brokeractivation-event-class-data-columns"></a>Broker:Activation 事件類別資料行  
  
|資料行|類型|描述|資料行編號|可篩選|  
|-----------------|----------|-----------------|-------------------|----------------|  
|**ClientProcessID**|`int`|主機電腦指派給用戶端應用程式執行中處理序的識別碼。 如果用戶端提供處理序識別碼，這個資料行就會擴展。|9|是|  
|**DatabaseID**|`int`|由 USE *database* 陳述式所指定的資料庫識別碼，或者如果沒有針對指定執行個體發出 USE *database*陳述式，則是預設資料庫的識別碼。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 資料行，則 **ServerName** 會顯示資料庫的名稱。 請使用 DB_ID 函數判斷資料庫的值。|3|是|  
|**EventClass**|`int`|擷取的事件類別類型。 對於 **Broker:Activation** ，一律為 **163**。|27|否|  
|**EventSequence**|`int`|此事件的序號。|51|否|  
|**EventSubClass**|`nvarchar`|此事件報告的特定動作。 為下列其中一個值：<br /><br /> **啟動**: <br />                [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 已開始啟用預存程序。<br /><br /> **結束**:啟用預存程序已正常結束。<br /><br /> **中止**:啟用預存程序已結束並發生錯誤。|21|否|  
|**HostName**|`nvarchar`|執行用戶端的電腦名稱。 這個資料行會在用戶端提供主機名稱時填入。 若要判斷主機名稱，請使用 HOST_NAME 函數。|8|是|  
|**IntegerData**|`int`|此佇列上作用中的工作數。|25|否|  
|**IsSystem**|`int`|指出事件是發生在系統處理序或使用者處理序。 1 = 系統，0 = 使用者。|60|否|  
|**LoginSid**|`image`|已登入之使用者的安全性識別碼 (SID)。 伺服器上的每一個登入之 SID 是唯一的。|41|是|  
|**NTDomainName**|`nvarchar`|使用者所隸屬的 Windows 網域。|7|是|  
|**NTUserName**|`nvarchar`|擁有產生此事件之連接的使用者名稱。|6|是|  
|**Exchange Spill**|`int`|與此事件相關聯的佇列。|22|否|  
|**ServerName**|`nvarchar`|正在追蹤之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的名稱。|26|否|  
|**SPID**|`int`|由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 指派給用戶端關聯之處理序的伺服器處理序識別碼。|12|是|  
|**StartTime**|`datetime`|事件啟動的時間 (如果有的話)。|14|是|  
|**TransactionID**|`bigint`|系統指派的交易識別碼。|4|否|  
  
  
