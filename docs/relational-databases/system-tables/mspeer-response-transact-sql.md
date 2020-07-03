---
title: MSpeer_response （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSpeer_response
- MSpeer_response_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSpeer_response system table
ms.assetid: 510e24cf-0292-47a9-b1d9-71a30fef030f
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 371ee711cbae4c97dc95e9d31d51739c29e85d14
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85889633"
---
# <a name="mspeer_response-transact-sql"></a>MSpeer_response (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  在點對點複寫中，會使用**MSpeer_response**資料表來儲存每個節點對發行集狀態要求的回應。 這份資料表儲存在發行集資料庫中。  
  
## <a name="definition"></a>定義  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**request_id**|**int**|識別[MSpeer_request](../../relational-databases/system-tables/mspeer-request-transact-sql.md)資料表中的狀態要求專案。|  
|**級**|**sysname**|產生回應的對等。|  
|**peer_db**|**sysname**|在產生回應之對等的訂閱資料庫。|  
|**received_date**|**datetime**|收到對等要求的日期和時間。|  
  
## <a name="see-also"></a>另請參閱  
 [複寫資料表 &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
