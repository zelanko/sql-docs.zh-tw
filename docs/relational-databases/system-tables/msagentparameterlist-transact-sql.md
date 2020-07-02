---
title: Msdb.dbo.msagentparameterlist （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSagentparameterlist_TSQL
- MSagentparameterlist
dev_langs:
- TSQL
helpviewer_keywords:
- Msagentparameterlist system table
ms.assetid: 4ea571a0-078d-4e13-95ee-f3d4bbd4dfb2
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 3e240ab373316f72d41f472542907e3feb83cbbd
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85725491"
---
# <a name="msagentparameterlist-transact-sql"></a>MSagentparameterlist (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  **Msdb.dbo.msagentparameterlist**資料表包含複寫代理程式參數資訊，可用來指定可針對指定的代理程式類型設定的參數。 此資料表會儲存在**msdb**資料庫中。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**agent_type**|**tinyint**|代理程式的類型：<br /><br /> **1** = 快照集代理程式。<br /><br /> **2** = 記錄讀取器代理程式。<br /><br /> **3** = 散發代理程式。<br /><br /> **4** = 合併代理程式。<br /><br /> **9** = 佇列讀取器代理程式。|  
|**parameter_name**|**sysname**|有效代理程式參數的名稱。|  
|**default_value**|**nvarchar(4000)**|代理程式參數的預設值，其中 NULL 表示沒有這樣的值存在。|  
|**min_value**|**int**|為代理程式參數設定下限，其中 NULL 表示沒有下限。|  
|**max_value**|**int**|為代理程式參數設定上限，其中 NULL 表示沒有上限。|  
  
## <a name="see-also"></a>另請參閱  
 [複寫資料表 &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
