---
title: M (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- MSpeer_conflictdetectionconfigrequest_TSQL
- MSpeer_conflictdetectionconfigrequest
dev_langs:
- TSQL
helpviewer_keywords:
- MSpeer_conflictdetectionconfigurerequest
ms.assetid: 83afa0ca-707e-4468-a888-228268ed4e10
caps.latest.revision: 11
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b1cecf9be5221cc8bbe3428c6cf2caabb4249438
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="mspeerconflictdetectionconfigrequest-transact-sql"></a>MSpeer_conflictdetectionconfigrequest (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  用於點對點複寫中，以追蹤發行集的全拓撲組態要求。 這份資料表儲存在發行集資料庫中。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|id|**int**|識別衝突組態要求。 中的 request_id 資料行會[MSpeer_conflictdetectionconfigresponse](../../relational-databases/system-tables/mspeer-conflictdetectionconfigresponse-transact-sql.md)會使用此值。|  
|publication|**sysname**|起始衝突組態要求的發行集名稱。|  
|sent_date|**datetime**|起始衝突組態要求的日期和時間。|  
|timeout|**int**|程序應該等候所有對等項目傳回衝突資訊的時間量。|  
|modified_date|**datetime**|完成階段的日期和時間。|  
|progress_phase|**nvarchar(32)**|使用下列其中一個值，識別處理的目前階段：<br /><br /> 시작됨<br /><br /> 瀏覽拓撲<br /><br /> 正在收集狀態<br /><br /> 已收集狀態|  
|phase_timed_out|**bit**|指出目前階段是否已逾時。|  
  
## <a name="see-also"></a>另請參閱  
 [複寫資料表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
