---
title: sp_helpdistributor_properties (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_helpdistributor_properties_TSQL
- sp_helpdistributor_properties
helpviewer_keywords:
- sp_helpdistributor_properties
ms.assetid: ee267724-3244-49eb-84c9-f38dbefdd639
caps.latest.revision: 14
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a738c9c7e8791295848799c50ccf2a6340f7595a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="sphelpdistributorproperties-transact-sql"></a>sp_helpdistributor_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回散發者屬性。 這個預存程序執行於散發資料庫的散發者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_helpdistributor_properties   
```  
  
## <a name="result-set"></a>結果集  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**heartbeat_interval**|**int**|在未記錄進度訊息的情況下，代理程式所能執行的最大分鐘數。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_helpdistributor_properties**用於所有複寫類型。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色、 成員的**db_owner**或**replmonitor**固定的資料庫角色中的使用者與散發資料庫使用此散發者的發行集的發行集存取清單 (PAL) 能夠執行**sp_helpdistributor_properties**。  
  
## <a name="see-also"></a>另請參閱  
 [sp_changedistributor_property &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedistributor-property-transact-sql.md)  
  
  
