---
title: sys.databases （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- messages_TSQL
- sys.messages_TSQL
- sys.messages
- messages
dev_langs:
- TSQL
helpviewer_keywords:
- error messages [SQL Server]
- sys.messages catalog view
- error numbers [SQL Server]
ms.assetid: 8c16ecdf-68f4-4a2a-b594-086e3344e58a
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 8ed45ac6fd511d2024cc11916fe70980a7a6a065
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82816058"
---
# <a name="messages-for-errors-catalog-views---sysmessages"></a>訊息 (適用於錯誤) 目錄檢視 - sys.messages
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  針對系統定義和使用者定義的訊息，包含系統中每個**message_id**或錯誤訊息**language_id**的資料列。 如需詳細資訊，請參閱 [sp_addmessage &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmessage-transact-sql.md)。  
   
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**message_id**|**int**|訊息的識別碼。 在伺服器中，這是唯一的。 小於 50000 的訊息識別碼，都是系統訊息。|  
|**language_id**|**smallint**|**文字**中使用文字的語言識別項，如**sys.syslanguages**中所定義。 這對指定的**message_id**而言是唯一的。|  
|**severity**|**tinyint**|訊息的嚴重性層級，介於 1 至 25 之間。 這對於**message_id**內的所有訊息語言都是一樣的。|  
|**is_event_logged**|**bit**|1 = 當引發錯誤時，會以記錄事件的方式記錄訊息。 這對於**message_id**內的所有訊息語言都是一樣的。|  
|**text**|**nvarchar(2048)**|當對應的**language_id**為作用中時，所使用之訊息的文字。|  
  
## <a name="permissions"></a>權限  
 需要 **public** 角色的成員資格。  如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [THROW &#40;Transact-SQL&#41;](../../t-sql/language-elements/throw-transact-sql.md)   
 [&#40;Transact-sql&#41;的目錄檢視](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [&#41; 目錄檢視 &#40;Transact-sql 的錯誤 &#40;訊息&#41;](https://msdn.microsoft.com/library/8ac78c53-7b97-41b3-9cbd-5f97c179f1f2)   
 [例外狀況訊息方塊程式設計](https://msdn.microsoft.com/library/0b1ba514-6959-4e69-bfd2-3cf3c1ac4b9c)   
 [錯誤訊息](../../relational-databases/native-client-odbc-error-messages/error-messages.md)   
 [資料庫引擎事件和錯誤](../../relational-databases/errors-events/database-engine-events-and-errors.md)  
  
  
