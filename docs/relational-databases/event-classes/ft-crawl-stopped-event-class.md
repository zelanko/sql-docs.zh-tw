---
description: FT:Crawl Stopped 事件類別
title: FT:Crawl Stopped 事件類別 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- Crawl Stopped event class
ms.assetid: dbc91bf7-687c-4083-9694-02f3e102c175
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d88987358baf3e22b509b9fc6bdbc8d74eda2007
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "88491054"
---
# <a name="ftcrawl-stopped-event-class"></a>FT:Crawl Stopped 事件類別
[!INCLUDE [SQL Server - ASDB](../../includes/applies-to-version/sql-asdb.md)]
  **:Crawl Stopped** 事件類別指出全文檢索搜耙 (母體擴展) 已停止。 停止的原因可能是已順利完成搜耙，或是發生嚴重錯誤。  
  
## <a name="ftcrawl-stopped-event-class-data-columns"></a>FT:Crawl Stopped 事件類別資料行  
  
|資料行名稱|資料類型|描述|資料行識別碼|可篩選|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**DatabaseID**|**int**|已停止全文檢索搜耙之資料庫的識別碼。 請使用 DB_ID 函數判斷資料庫的值。|3|是|  
|**EventClass**|**int**|事件類型 = 156。|27|否|  
|**EventSequence**|**int**|要求中的給定事件順序。|51|否|  
|**IsSystem**|**int**|指出事件是發生在系統處理序或使用者處理序。 1 = 系統，0 = 使用者。|60|是|  
|**Exchange Spill**|**int**|系統指派給物件的識別碼。 此物件上的全文檢索索引已停止全文檢索搜耙。|22|是|  
|**SessionLoginName**|**nvarchar**|引發工作階段之使用者的登入名稱。 例如，如果您使用 Login1 連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，並以 Login2 執行陳述式，則 **SessionLoginName** 將顯示 Login1 而 **LoginName** 則顯示 Login2。 這個資料行會同時顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 與 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 登入。|64|是|  
|**SPID**|**int**|事件發生所在之工作階段的識別碼。|12|是|  
|**StartTime**|**datetime**|事件啟動的時間 (如果有的話)。|14|是|  
|**TransactionID**|**bigint**|由系統指派給交易的識別碼。|4|是|  
  
## <a name="see-also"></a>另請參閱  
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)  
  
  
