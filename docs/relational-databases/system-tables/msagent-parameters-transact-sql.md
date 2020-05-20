---
title: MSagent_parameters （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSagent_parameters_TSQL
- MSagent_parameters
dev_langs:
- TSQL
helpviewer_keywords:
- MSagent_parameters system table
ms.assetid: be30abc9-c00d-446f-b1b4-1269772f37e6
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 92957ae8cb47f181d230d16b96c9d6e40b1ea107
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82805532"
---
# <a name="msagent_parameters-transact-sql"></a>MSagent_parameters (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSagent_parameters**資料表包含與代理程式設定檔相關聯的參數。 這些參數名稱與該代理程式所支援的參數同名。 此資料表會儲存在**msdb**資料庫中。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**profile_id**|**int**|**MSagent_profiles**資料表中的設定檔識別碼。|  
|**parameter_name**|**sysname**|參數名稱。|  
|**值**|**nvarchar(255)**|參數的值。|  
  
## <a name="see-also"></a>另請參閱  
 [複寫資料表 &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
