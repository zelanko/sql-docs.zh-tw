---
description: MSpeer_topologyrequest (Transact-SQL)
title: MSpeer_topologyrequest (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSpeer_topologyrequest_TSQL
- MSpeer_topologyrequest
dev_langs:
- TSQL
helpviewer_keywords:
- MSpeer_topologyrequest
ms.assetid: c644814b-4e40-44d7-b6b4-5954b0d4db7c
author: markingmyname
ms.author: maghan
ms.openlocfilehash: f3d04ce7291660b52b6273ee7afb562da4bd4fce
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89547045"
---
# <a name="mspeer_topologyrequest-transact-sql"></a>MSpeer_topologyrequest (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  用於點對點複寫中，以追蹤發行集的拓撲狀態要求。 這份資料表儲存在發行集資料庫中。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|id|**int**|識別拓撲狀態要求。 [MSpeer_topologyresponse](../../relational-databases/system-tables/mspeer-topologyresponse-transact-sql.md)中的 request_id 資料行使用此值。|  
|publication|**sysname**|起始拓撲狀態要求的發行集名稱。|  
|sent_date|**datetime**|起始拓撲狀態要求的日期和時間。|  
  
## <a name="see-also"></a>另請參閱  
 [複寫資料表 &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
