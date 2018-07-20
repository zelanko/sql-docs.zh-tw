---
title: MSagentparameterlist & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
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
- MSagentparameterlist_TSQL
- MSagentparameterlist
dev_langs:
- TSQL
helpviewer_keywords:
- Msagentparameterlist system table
ms.assetid: 4ea571a0-078d-4e13-95ee-f3d4bbd4dfb2
caps.latest.revision: 13
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cf4ba519e2fef4a297e7406689aa33f489c01805
ms.sourcegitcommit: a431ca21eac82117492d7b84c398ddb3fced53cc
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/17/2018
ms.locfileid: "39101256"
---
# <a name="msagentparameterlist-transact-sql"></a>MSagentparameterlist (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSagentparameterlist**資料表包含複寫代理程式參數資訊，用來指定可以針對給定代理程式類型設定的參數。 這份資料表儲存在**msdb**資料庫。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**agent_type**|**tinyint**|代理程式的類型：<br /><br /> **1** = 快照集代理程式。<br /><br /> **2** = 記錄讀取器代理程式。<br /><br /> **3** = 散發代理程式。<br /><br /> **4** = 合併代理程式。<br /><br /> **9** = 佇列讀取器代理程式。|  
|**parameter_name**|**sysname**|有效代理程式參數的名稱。|  
|**default_value**|**nvarchar(4000)**|代理程式參數的預設值，其中 NULL 表示沒有這樣的值存在。|  
|**min_value**|**int**|為代理程式參數設定下限，其中 NULL 表示沒有下限。|  
|**max_value**|**int**|為代理程式參數設定上限，其中 NULL 表示沒有上限。|  
  
## <a name="see-also"></a>另請參閱  
 [複寫資料表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
