---
description: sys.service_contract_message_usages (Transact-SQL)
title: sys. service_contract_message_usages (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- service_contract_message_usages_TSQL
- sys.service_contract_message_usages
- sys.service_contract_message_usages_TSQL
- service_contract_message_usages
dev_langs:
- TSQL
helpviewer_keywords:
- sys.service_contract_message_usages catalog view
ms.assetid: f783e662-126c-4595-8e22-f9d05191f5d0
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 43767305ac23b5ae4074e36fe2c3256d2fe12fd7
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89539546"
---
# <a name="sysservice_contract_message_usages-transact-sql"></a>sys.service_contract_message_usages (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  這份目錄檢視針對每個 (合約、訊息類型) 配對，各包含一個資料列。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**service_contract_id**|**int**|使用訊息類型的合約識別碼。 不是 NULLABLE。|  
|**message_type_id**|**int**|合約所用的訊息類型識別碼。 不是 NULLABLE。|  
|**is_sent_by_initiator**|**bit**|可由交談起始端傳送的訊息類型。 不是 NULLABLE。|  
|**is_sent_by_target**|**bit**|可由交談目標傳送的訊息類型。 不是 NULLABLE。|  
  
## <a name="permissions"></a>權限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
  
