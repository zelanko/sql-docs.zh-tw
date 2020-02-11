---
title: sys.databases trace_categories （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- trace_categories
- trace_categories_TSQL
- sys.trace_categories
- sys.trace_categories_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.trace_categories catalog view
ms.assetid: f6a86766-e2a9-4d9f-a073-1b59e888ba7d
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: c9685b9733c1d13b79ef2a19ee2f19bbe3130426
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68106667"
---
# <a name="systrace_categories-transact-sql"></a>sys.trace_categories (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  依類別目錄來分組類似的事件類別。 **Trace_categories**目錄檢視中的每個資料列都會識別在伺服器上唯一的類別。 
  [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 給定版本的這些類別目錄不會改變。  
  
 如需所支援追蹤事件的完整清單，請參閱[SQL Server 事件類別參考](../../relational-databases/event-classes/sql-server-event-class-reference.md)。  
  
> **重大!** 
  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]請改用擴充事件目錄檢視。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**category_id**|**smallint**|這個類別目錄的唯一識別碼。 此資料行也在**trace_events**目錄檢視中。|  
|**name**|**nvarchar(128)**|這個類別目錄的唯一名稱。 這個參數未翻譯成當地語系。|  
|**type**|**tinyint**|類別目錄類型：<br /><br /> 0 = 正常<br /><br /> 1 = 連接<br /><br /> 2 = 錯誤|  
  
## <a name="permissions"></a>權限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的物件目錄檢視](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [&#40;Transact-sql&#41;的追蹤](../../relational-databases/system-catalog-views/sys-traces-transact-sql.md)   
 [trace_columns &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-trace-columns-transact-sql.md)   
 [trace_events &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-trace-events-transact-sql.md)   
 [trace_event_bindings &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-trace-event-bindings-transact-sql.md)   
 [trace_subclass_values &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-trace-subclass-values-transact-sql.md)  
  
  
