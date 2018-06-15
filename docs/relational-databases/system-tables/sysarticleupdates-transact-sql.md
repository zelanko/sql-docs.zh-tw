---
title: sysarticleupdates (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
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
- sysarticleupdates_TSQL
- sysarticleupdates
dev_langs:
- TSQL
helpviewer_keywords:
- sysarticleupdates system table
ms.assetid: 11a53bcd-a215-4d0b-9db8-233981d3ef5d
caps.latest.revision: 28
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 384e6abd93369bd1913bddf31b8dec6f8541e0d7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "33005575"
---
# <a name="sysarticleupdates-transact-sql"></a>sysarticleupdates (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  針對每個支援立即更新訂閱的發行項，各包含一個資料列。 這份資料表儲存在複寫的資料庫中。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**artid**|**int**|提供發行項唯一識別碼的識別欄位。|  
|**pubid**|**int**|發行項所屬發行集的識別碼。|  
|**sync_ins_proc**|**int**|處理「插入同步交易」之預存程序的識別碼。|  
|**sync_upd_proc**|**int**|處理「更新同步交易」之預存程序的識別碼。|  
|**sync_del_proc**|**int**|處理「刪除同步交易」之預存程序的識別碼。|  
|**autogen**|**bit**|指出自動產生預存程序：<br /><br /> **0** = false，不自動。<br /><br /> **1** = true，自動。|  
|**sync_upd_trig**|**int**|發行項資料表之自動版本控制觸發程序的識別碼。|  
|**conflict_tableid**|**int**|衝突資料表的識別碼。|  
|**ins_conflict_proc**|**int**|用來將衝突寫入程序的識別碼**conflict_table**。|  
|**identity_support**|**bit**|指定在使用佇列更新時，是否啟用自動識別範圍處理。 **0**表示沒有識別範圍支援。|  
  
## <a name="see-also"></a>另請參閱  
 [複寫資料表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
