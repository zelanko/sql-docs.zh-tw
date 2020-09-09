---
description: sys.trace_events (Transact-SQL)
title: sys. trace_events (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- trace_events_TSQL
- trace_events
- sys.trace_events
- sys.trace_events_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.trace_events catalog view
ms.assetid: e7d2c5df-0e17-4e94-9d41-d36c7ee60662
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 0b83821952fb9b7aa96a1c5c1da4033da1e750aa
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89544941"
---
# <a name="systrace_events-transact-sql"></a>sys.trace_events (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **Sys. trace_events**目錄檢視包含所有 SQL 追蹤事件的清單。 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 給定版本的這些追蹤事件不會改變。  
  
> **重要！** [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]請改用擴充事件目錄檢視。  
  
 如需有關這些追蹤事件的詳細資訊，請參閱 [SQL Server 事件類別參考](../../relational-databases/event-classes/sql-server-event-class-reference.md)。  
  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**trace_event_id**|**smallint**|事件的唯一識別碼。 這個資料行也在 **sys. trace_event_bindings** 和 **sys. trace_subclass_values** 目錄檢視中。|  
|**category_id**|**smallint**|事件的類別目錄識別碼。 這個資料行也在 **sys. trace_categories** 目錄檢視中。|  
|**name**|**nvarchar(128)**|這個事件的唯一名稱。 這個參數未翻譯成當地語系。|  
  
## <a name="permissions"></a>權限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [物件目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [sys. 追蹤 &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-traces-transact-sql.md)   
 [sys. trace_categories &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-trace-categories-transact-sql.md)   
 [sys. trace_columns &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-trace-columns-transact-sql.md)   
 [sys. trace_event_bindings &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-trace-event-bindings-transact-sql.md)   
 [sys. trace_subclass_values &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-trace-subclass-values-transact-sql.md)  
  
  
