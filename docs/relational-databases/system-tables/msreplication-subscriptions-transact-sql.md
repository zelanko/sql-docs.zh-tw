---
title: MSreplication_subscriptions （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSreplication_subscriptions
- MSreplication_subscriptions_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSreplication_subscriptions system table
ms.assetid: fd0c5843-4e9b-4448-8bfb-0a4067d1d8d1
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 37114a42cd7e9c64872ff42848bb916b21c1d941
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82812362"
---
# <a name="msreplication_subscriptions-transact-sql"></a>MSreplication_subscriptions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSreplication_subscriptions**資料表會針對服務本機訂閱者資料庫的每個散發代理程式，各包含一個複寫資訊資料列。 這份資料表儲存在訂閱資料庫中。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**publisher**|**sysname**|發行者的名稱。|  
|**publisher_db**|**sysname**|發行者資料庫的名稱。|  
|**發行集**|**sysname**|發行集的名稱。|  
|**independent_agent**|**bit**|指出這個發行集是否有獨立的散發代理程式。|  
|**subscription_type**|**int**|訂閱的類型：<br /><br /> 0 = 發送。<br /><br /> 1 = 提取。<br /><br /> 2 = 匿名。|  
|**distribution_agent**|**sysname**|散發代理程式的名稱。|  
|**Time**|**smalldatetime**|前次由散發代理程式更新的時間。|  
|**描述**|**nvarchar(255)**|訂閱的描述。|  
|**transaction_timestamp**|**varbinary(16)**|僅供內部使用。|  
|**update_mode**|**tinyint**|更新的類型。|  
|**agent_id**|**binary(16)**|代理程式的識別碼。|  
|**subscription_guid**|**binary(16)**|發行集訂閱版本的全域識別碼。|  
|**subid**|**binary(16)**|匿名訂閱的全域識別碼。|  
|**immediate_sync**|**bit**|指出每次執行快照集代理程式時，是否要建立或重新建立同步處理檔案。|  
  
## <a name="see-also"></a>另請參閱  
 [複寫資料表 &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [&#40;Transact-sql&#41;的複寫視圖](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_helpsubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)  
  
  
