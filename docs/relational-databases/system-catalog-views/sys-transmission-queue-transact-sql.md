---
description: sys.transmission_queue (Transact-SQL)
title: sys. transmission_queue (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- transmission_queue
- sys.transmission_queue_TSQL
- sys.transmission_queue
- transmission_queue_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.transmission_queue catalog view
ms.assetid: f3515d1a-be8f-4a27-8058-8865f0919838
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 9e3fbd63f399b54af919fd791f33e5d6f7b75a93
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88400294"
---
# <a name="systransmission_queue-transact-sql"></a>sys.transmission_queue (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  這份目錄檢視會針對傳輸佇列中的每一則訊息，各包含一個資料列，如下表所示：  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**conversation_handle**|**uniqueidentifier**|這則訊息所屬之交談的識別碼。 不是 NULLABLE。|  
|**to_service_name**|**nvarchar(256)**|這則訊息所送往之服務的名稱。 NULLABLE。|  
|**to_broker_instance**|**nvarchar(128)**|主控這則訊息所送往之服務的 Broker 識別碼。 NULLABLE。|  
|**from_service_name**|**nvarchar(256)**|這則訊息的來源服務名稱。 NULLABLE。|  
|**service_contract_name**|**nvarchar(256)**|這則訊息之交談所遵照的合約名稱。 NULLABLE。|  
|**enqueue_time**|**datetime**|訊息進入佇列的時間。 無論執行個體的當地時區為何，這個值一律使用 UTC。 不是 NULLABLE。|  
|**message_sequence_number**|**bigint**|訊息的序號。 不是 NULLABLE。|  
|**message_type_name**|**nvarchar(256)**|訊息的訊息類型名稱。 NULLABLE。|  
|**is_conversation_error**|**bit**|這則訊息是否為錯誤訊息。<br /><br /> 0 = 不是錯誤訊息。<br /><br /> 1 = 錯誤訊息。<br /><br /> 不是 NULLABLE。|  
|**is_end_of_dialog**|**bit**|這則訊息是否代表交談訊息結束。 不是 NULLABLE。<br /><br /> 0 = 不代表交談訊息結束。<br /><br /> 1 = 代表交談訊息結束。<br /><br /> 不是 NULLABLE。|  
|**message_body**|**varbinary(max)**|這則訊息的主體。 NULLABLE。|  
|**transmission_status**|**nvarchar(4000)**|這則訊息進入佇列的理由。 它通常是錯誤訊息，說明傳送訊息為何失敗。 如果是空白，表示尚未傳送訊息。 NULLABLE。|  
|**priority**|**tinyint**|指派給這個訊息的優先權等級。 不是 NULLABLE。|  
  
## <a name="permissions"></a>權限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
  
