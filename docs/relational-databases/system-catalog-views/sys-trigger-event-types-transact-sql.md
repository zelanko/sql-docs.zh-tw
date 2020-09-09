---
description: sys.trigger_event_types (Transact-SQL)
title: sys. trigger_event_types (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- trigger_event_types_TSQL
- sys.trigger_event_types_TSQL
- sys.trigger_event_types
- trigger_event_types
dev_langs:
- TSQL
helpviewer_keywords:
- sys.trigger_event_types catalog view
ms.assetid: 054aed54-7151-4760-934a-149fa434f1ae
author: markingmyname
ms.author: maghan
ms.openlocfilehash: aaa944c06fc90a5a7b1a1c421b1c77963aa5d40e
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89544902"
---
# <a name="systrigger_event_types-transact-sql"></a>sys.trigger_event_types (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  針對可以引發觸發程序的每個事件或事件群組，各傳回一個資料列。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**type**|**int**|造成觸發程序引發的事件或事件群組的類型。|  
|**type_name**|**Nvarchar (64) **|事件或事件群組的名稱。 這可以在 [CREATE TRIGGER](../../t-sql/statements/create-trigger-transact-sql.md) 語句的 FOR 子句中指定。|  
|**parent_type**|**int**|事件或事件群組之父項的事件群組類型。|  
  
## <a name="permissions"></a>權限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [物件目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
