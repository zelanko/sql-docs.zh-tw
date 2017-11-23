---
title: "sys.messages (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- messages_TSQL
- sys.messages_TSQL
- sys.messages
- messages
dev_langs: TSQL
helpviewer_keywords:
- error messages [SQL Server]
- sys.messages catalog view
- error numbers [SQL Server]
ms.assetid: 8c16ecdf-68f4-4a2a-b594-086e3344e58a
caps.latest.revision: "38"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: b8163fb44e72942422b044a23687c395a75bbfcd
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="messages-for-errors-catalog-views---sysmessages"></a>訊息 （錯誤） 目錄檢視-sys.messages
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  每個包含一個資料列**message_id**或**language_id**系統，同時系統定義和使用者定義訊息中的錯誤訊息。 如需詳細資訊，請參閱 [sp_addmessage &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmessage-transact-sql.md)。  
   
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**message_id**|**int**|訊息的識別碼。 在伺服器中，這是唯一的。 小於 50000 的訊息識別碼，都是系統訊息。|  
|**language_id**|**smallint**|語言識別碼中的文字**文字**使用，如下所述**syslanguages**。 這是唯一的指定**message_id**。|  
|**嚴重性**|**tinyint**|訊息的嚴重性層級，介於 1 至 25 之間。 這會是相同的所有內的訊息語言**message_id**。|  
|**is_event_logged**|**bit**|1 = 當引發錯誤時，會以記錄事件的方式記錄訊息。 這會是相同的所有內的訊息語言**message_id**。|  
|**text**|**nvarchar(2048)**|訊息的文字時使用對應**language_id**為作用中。|  
  
## <a name="permissions"></a>Permissions  
 需要 **public** 角色的成員資格。 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>請參閱＜  
 [THROW &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/throw-transact-sql.md)   
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [訊息 &#40; 錯誤 &#41;目錄檢視 &#40;TRANSACT-SQL &#41;](http://msdn.microsoft.com/library/8ac78c53-7b97-41b3-9cbd-5f97c179f1f2)   
 [例外狀況訊息方塊程式設計](http://msdn.microsoft.com/library/0b1ba514-6959-4e69-bfd2-3cf3c1ac4b9c)   
 [錯誤訊息](../../relational-databases/native-client-odbc-error-messages/error-messages.md)   
 [資料庫引擎事件和錯誤](../../relational-databases/errors-events/database-engine-events-and-errors.md)  
  
  
