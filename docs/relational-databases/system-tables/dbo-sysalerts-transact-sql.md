---
title: dbo.sysalerts (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 10/24/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.sysalerts
- sysalerts_TSQL
- dbo.sysalerts_TSQL
- sysalerts
dev_langs:
- TSQL
helpviewer_keywords:
- sysalerts system table
ms.assetid: a2c2f50d-61f3-4951-996a-add5ad092cc2
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7bad6fbd9229547318a060f08eeb102b21cda9bb
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47855037"
---
# <a name="dbosysalerts-transact-sql"></a>dbo.sysalerts (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  針對每個警示各包含一個資料列。 警示是事件的回應所傳送的訊息。 警示可以將訊息轉送到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 環境之外，它可能是電子郵件訊息，也可能是呼叫器訊息。 另外，警示也可以產生工作。  這份資料表儲存在**msdb**資料庫。
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**id**|**int**|警示識別碼。|  
|**name**|**sysname**|警示名稱。|  
|**event_source**|**nvarchar(100)**|事件來源：[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。|  
|**event_category_id**|**int**|保留供日後使用。|  
|**event_id**|**int**|保留供日後使用。|  
|**message_id**|**int**|使用者定義訊息識別碼或參考**sysmessages**觸發此警示的訊息。|  
|**severity**|**int**|觸發這個警示的嚴重性。|  
|**enabled**|**tinyint**|警示的狀態：<br /><br /> **0** = 已停用。<br /><br /> **1** = 啟用。|  
|**delay_between_responses**|**int**|這個警示各次通知之間的等待期間 (以秒為單位)。|  
|**last_occurrence_date**|**int**|警示的前一次出現 (日期)。|  
|**last_occurrence_time**|**int**|警示的前一次出現 (日期時間)。|  
|**last_response_date**|**int**|警示的前一次通知 (日期)。|  
|**last_response_time**|**int**|警示的前一次通知 (日期時間)。|  
|**notification_message**|**nvarchar(512)**|隨著警示而傳送的其他資訊。|  
|**include_event_description**|**tinyint**|位元遮罩表示是否會傳送電子郵件、 呼叫器或 Net send 事件描述。 請參閱以下值的圖表。|  
|**database_name**|**nvarchar(512)**|這個警示必須出現在其中以便觸發這個警示的資料庫。|  
|**event_description_keyword**|**nvarchar(100)**|錯誤必須符合才能觸發警示的模式。|  
|**occurrence_count**|**int**|這個警示的出現次數。|  
|**count_reset_date**|**int**|天數 （日期） 計數將重設為**0**。|  
|**count_reset_time**|**int**|日期時間計數將重設為**0**。|  
|**job_id**|**uniqueidentifier**|發生這個警示時所執行的作業識別碼。|  
|**has_notification**|**int**|發生警示時收到電子郵件通知的操作員數目。|  
|**flags**|**int**|已保留。|  
|**performance_condition**|**nvarchar(512)**|已保留。|  
|**category_id**|**int**|已保留。|  
  
 ## <a name="remarks"></a>備註

下表顯示之 include_event_description 位元遮罩值。 Dbo.sysalerts 會傳回的十進位值。 

|Decimal | BINARY | 意義 |
|------|------|------|
|0 |0000 |沒有訊息 |
|1 |0001 |電子郵件 |
|2 |0010 |呼叫器 |
|3 |0011 |呼叫器和電子郵件 |
|4 |0100 |Net Send |
|5 |0101 |Net send 和電子郵件 |
|6 |0110 |Net send 和呼叫器 |
|7 |0111 |Net send、 呼叫器和電子郵件 |
  
