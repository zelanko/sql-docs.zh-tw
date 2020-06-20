---
title: FT:Crawl Aborted 事件類別 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Crawl Aborted event class
ms.assetid: eead8ea6-5051-4689-ab30-4dfbfda01fb9
author: stevestein
ms.author: sstein
ms.openlocfilehash: 843e15f6f4cc0e683bb24a9a4709d66707111737
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85052963"
---
# <a name="ftcrawl-aborted-event-class"></a>FT:Crawl Aborted 事件類別
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
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)  
  
  
