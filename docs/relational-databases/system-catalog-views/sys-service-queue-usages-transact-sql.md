---
title: sys.service_queue_usages (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.service_queue_usages
- sys.service_queue_usages_TSQL
- service_queue_usages
- service_queue_usages_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.service_queue_usages catalog view
ms.assetid: d58dcdaf-f82d-43d9-941b-f520581442bf
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8ddeccbf7b70f399569083a05366bc803fd1b1c8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47596207"
---
# <a name="sysservicequeueusages-transact-sql"></a>sys.service_queue_usages (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  這份目錄檢視會針對服務和服務佇列之間的每一個參考，各傳回一個資料列。 服務只能與一個佇列相關聯。 但一個佇列可以與多個服務相關聯。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**service_id**|**int**|服務的識別碼。 在資料庫中，這是唯一的。 不是 NULLABLE。|  
|**service_queue_id**|**int**|服務所用的服務佇列識別碼。 不是 NULLABLE。|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [sys.services &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/sys-services-transact-sql.md)  
  
  
