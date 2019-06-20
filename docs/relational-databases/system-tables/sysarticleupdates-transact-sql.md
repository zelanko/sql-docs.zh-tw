---
title: sysarticleupdates (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysarticleupdates_TSQL
- sysarticleupdates
dev_langs:
- TSQL
helpviewer_keywords:
- sysarticleupdates system table
ms.assetid: 11a53bcd-a215-4d0b-9db8-233981d3ef5d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 70827c6dcf420c4e4aa21aa8085e33b20fa72760
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62714161"
---
# <a name="sysarticleupdates-transact-sql"></a>sysarticleupdates (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  針對每個支援立即更新訂閱的發行項，各包含一個資料列。 這份資料表儲存在複寫的資料庫中。  
  
|資料行名稱|資料類型|描述|  
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
|**identity_support**|**bit**|指定在使用佇列更新時，是否啟用自動識別範圍處理。 **0**表示沒有任何身分識別支援範圍。|  
  
## <a name="see-also"></a>另請參閱  
 [複寫資料表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
