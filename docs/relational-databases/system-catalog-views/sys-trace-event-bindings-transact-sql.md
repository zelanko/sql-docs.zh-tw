---
description: sys.trace_event_bindings (Transact-SQL)
title: sys. trace_event_bindings (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.trace_event_bindings_TSQL
- trace_event_bindings
- sys.trace_event_bindings
- trace_event_bindings_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.trace_event_bindings catalog view
ms.assetid: 22f534e1-4ed6-4b3e-9ead-1d1001a1b0f5
author: markingmyname
ms.author: maghan
ms.openlocfilehash: a1e9410664022a19b731d0d06e082dc8d15187a4
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89544952"
---
# <a name="systrace_event_bindings-transact-sql"></a>sys.trace_event_bindings (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **Sys. trace_event_bindings**目錄檢視包含事件和資料行的所有可能使用組合的清單。 針對 **trace_event_id** 資料行中所列的每個事件，所有可用的資料行都會列在 [ **trace_column_id** ] 資料行中。 不是每次發生給定的事件，都會擴展所有可用的資料行。 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 給定版本的這些值不會改變。  
  
 如需支援的追蹤事件的完整清單，請參閱 [SQL Server 事件類別參考](../../relational-databases/event-classes/sql-server-event-class-reference.md)。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]請改用擴充事件目錄檢視。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**trace_event_id**|**smallint**|追蹤事件的識別碼。 這個資料行也在 **sys. trace_events** 目錄檢視中。|  
|**trace_column_id**|**smallint**|追蹤資料行的識別碼。 這個資料行也在 **sys. trace_columns** 目錄檢視中。|  
  
## <a name="permissions"></a>權限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [物件目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [sys. 追蹤 &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-traces-transact-sql.md)   
 [sys. trace_categories &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-trace-categories-transact-sql.md)   
 [sys. trace_columns &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-trace-columns-transact-sql.md)   
 [sys. trace_events &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-trace-events-transact-sql.md)   
 [sys. trace_subclass_values &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-trace-subclass-values-transact-sql.md)  
  
  
