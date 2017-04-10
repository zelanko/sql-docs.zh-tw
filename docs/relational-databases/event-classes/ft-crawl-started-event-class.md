---
title: "FT:Crawl Started 事件類別 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Crawl Started 事件類別"
ms.assetid: 2535b856-97e8-4fb2-8ba0-5d5446355fa6
caps.latest.revision: 28
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 28
---
# FT:Crawl Started 事件類別
  **FT:Crawl Started** 事件類別指出全文檢索搜耙 (母體擴展) 已啟動。 使用此事件類別來檢查是否真由工作者工作來挑選搜耙要求。  
  
## FT: Crawl Started 事件類別資料行  
  
|資料行名稱|資料類型|描述|資料行識別碼|可篩選|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**DatabaseID**|**int**|已啟動全文檢索搜耙之資料庫的識別碼。 請使用 DB_ID 函數判斷資料庫的值。|3|是|  
|**EventClass**|**int**|事件類型 = 155。|27|否|  
|**EventSequence**|**int**|要求中的給定事件順序。|51|否|  
|**IsSystem**|**int**|指出事件是發生在系統處理序或使用者處理序。 1 = 系統，0 = 使用者。|60|是|  
|**ObjectID**|**int**|系統指派給物件的識別碼。 此物件的全文檢索索引上已啟動全文檢索搜耙。|22|是|  
|**SessionLoginName**|**nvarchar**|引發工作階段之使用者的登入名稱。 例如，如果您使用 Login1 連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，並以 Login2 執行陳述式，則 **SessionLoginName** 將顯示 Login1 而 **LoginName** 則顯示 Login2。 這個資料行會同時顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 與 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 登入。|64|是|  
|**SPID**|**int**|事件發生所在之工作階段的識別碼。|12|是|  
|**StartTime**|**datetime**|事件啟動的時間 (如果有的話)。|14|是|  
|**TextData**|**ntext**|全文檢索搜耙類型。 值可以是「完整」、「累加」、「手動」或「自動」。|1|是|  
|**TransactionID**|**bigint**|由系統指派給交易的識別碼。|4|是|  
  
## 另請參閱  
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)  
  
  