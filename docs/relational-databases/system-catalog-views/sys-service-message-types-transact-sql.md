---
title: "sys.service_message_types (TRANSACT-SQL) |Microsoft 文件"
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
- sys.service_message_types
- service_message_types
- sys.service_message_types_TSQL
- service_message_types_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.service_message_types catalog view
ms.assetid: 6a38709a-60fe-46f6-89da-718f74f15600
caps.latest.revision: "32"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 866424b72b284479e2f9e1771ff62c5099cb7f71
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="sysservicemessagetypes-transact-sql"></a>sys.service_message_types (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  這份目錄檢視針對在 Service Broker 中登錄的每一種訊息類型，各包含一個資料列。
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|訊息類型的名稱，它在資料庫中是唯一的。 不是 NULLABLE。|  
|**message_type_id**|**int**|訊息類型的識別碼，它在資料庫中是唯一的。 不是 NULLABLE。|  
|**principal_id**|**int**|擁有這個訊息類型的資料庫主體識別碼。 NULLABLE。|  
|**驗證**|**char(2)**|在傳送這種類型的訊息之前，已由 Broker 完成的驗證。 不是 NULLABLE。 它是下列項目之一：<br /><br /> N = 無<br /><br /> X = XML<br /><br /> E = 空的|  
|**validation_desc**|**nvarchar （60)**|在傳送這種類型的訊息之前，已由 Broker 完成的驗證描述。 NULLABLE。 它是下列項目之一：<br /><br /> 無<br /><br /> XML<br /><br /> EMPTY|  
|**xml_collection_id**|**int**|如果是使用 XML 結構描述來進行驗證，則使用該結構描述集合的識別碼。<br /><br /> 否則為 NULL。|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
  
