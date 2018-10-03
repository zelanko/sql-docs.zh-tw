---
title: MStracer_history (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- MStracer_history
- MStracer_history_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MStracer_history system table
ms.assetid: 97237a0c-d574-4b17-8a94-1a8730b31d98
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 439a40ad6362c0cb39e8559c267c7d62d1218f9c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47782076"
---
# <a name="mstracerhistory-transact-sql"></a>MStracer_history (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MStracer_history**資料表會維護所有已在訂閱者端接收的追蹤 token 記錄。 這份資料表儲存在散發資料庫中，並且由複寫用來監視效能之用。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**parent_tracer_id**|**int**|唯一識別追蹤 Token。|  
|**agent_id**|**int**|識別處理追蹤 Token 記錄的代理程式。|  
|**subscriber_commit**|**datetime**|在訂閱者端認可追蹤 Token 記錄的日期和時間。|  
  
## <a name="see-also"></a>另請參閱  
 [複寫資料表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
