---
title: FT:Crawl Aborted 事件類別 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: event-classes
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Crawl Aborted event class
ms.assetid: eead8ea6-5051-4689-ab30-4dfbfda01fb9
caps.latest.revision: 28
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: da99912dcef9d9894933ba30fa6f276742e91bf8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="ftcrawl-aborted-event-class"></a>FT:Crawl Aborted 事件類別
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  **FT:Crawl Aborted** 事件類別指出全文檢索搜耙期間遇到了例外狀況。 這個錯誤通常會造成全文檢索搜耙停止。 請檢查 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 事件記錄檔或搜耙記錄檔，以取得更詳細的錯誤資訊。  
  
## <a name="ftcrawl-aborted-event-class-data-columns"></a>FT:Crawl Aborted 事件類別資料行  
  
|資料行名稱|資料類型|描述|資料行識別碼|可篩選|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**DatabaseID**|**int**|正在執行全文檢索搜耙的資料庫識別碼。 請使用 DB_ID 函數判斷資料庫的值。|3|是|  
|**錯誤**|**int**|給定事件的錯誤號碼。 通常這是存放在 **sysmessages** 資料表中的錯誤號碼。|31|是|  
|**EventClass**|**int**|事件類型 = 157。|27|否|  
|**EventSequence**|**int**|要求中的給定事件順序。|51|否|  
|**IsSystem**|**int**|指出事件是發生在系統處理序或使用者處理序。 1 = 系統，0 = 使用者。|60|是|  
|**Exchange Spill**|**int**|發生失敗時，正在執行全文檢索搜耙的物件識別碼 (由系統指派)。|22|是|  
|**SessionLoginName**|**nvarchar**|引發工作階段之使用者的登入名稱。 例如，如果您使用 Login1 連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，並以 Login2 執行陳述式，則 **SessionLoginName** 將顯示 Login1 而 **LoginName** 則顯示 Login2。 此資料行將同時顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 Windows 登入。|64|是|  
|**SPID**|**int**|事件發生所在之工作階段的識別碼。|12|是|  
|**StartTime**|**datetime**|事件啟動的時間 (如果有的話)。|14|是|  
|**State**|**int**|相當於錯誤狀態碼。|30|是|  
|**TransactionID**|**bigint**|由系統指派給交易的識別碼。|4|是|  
  
## <a name="see-also"></a>另請參閱  
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)  
  
  
