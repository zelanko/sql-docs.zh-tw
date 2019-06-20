---
title: sys.service_message_types (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.service_message_types
- service_message_types
- sys.service_message_types_TSQL
- service_message_types_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.service_message_types catalog view
ms.assetid: 6a38709a-60fe-46f6-89da-718f74f15600
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 81a7a5cd518096582ba07e4400982308b9c1c2aa
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62856636"
---
# <a name="sysservicemessagetypes-transact-sql"></a>sys.service_message_types (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  這份目錄檢視針對在 Service Broker 中登錄的每一種訊息類型，各包含一個資料列。
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|訊息類型的名稱，它在資料庫中是唯一的。 不是 NULLABLE。|  
|**message_type_id**|**int**|訊息類型的識別碼，它在資料庫中是唯一的。 不是 NULLABLE。|  
|**principal_id**|**int**|擁有這個訊息類型的資料庫主體識別碼。 NULLABLE。|  
|**validation**|**char(2)**|在傳送這種類型的訊息之前，已由 Broker 完成的驗證。 不是 NULLABLE。 它是下列項目之一：<br /><br /> N = 無<br /><br /> X = XML<br /><br /> E = 空的|  
|**validation_desc**|**nvarchar(60)**|在傳送這種類型的訊息之前，已由 Broker 完成的驗證描述。 NULLABLE。 它是下列項目之一：<br /><br /> 無<br /><br /> XML<br /><br /> EMPTY|  
|**xml_collection_id**|**int**|如果是使用 XML 結構描述來進行驗證，則使用該結構描述集合的識別碼。<br /><br /> 否則為 NULL。|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
  
