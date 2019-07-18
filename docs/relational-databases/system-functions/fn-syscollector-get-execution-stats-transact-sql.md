---
title: fn_syscollector_get_execution_stats (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fn_syscollector_get_execution_stats
- fn_syscollector_get_execution_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- fn_syscollector_get_execution_stats function
ms.assetid: 793ad72c-a992-4a8d-8584-bcb6b3b476f1
author: rothja
ms.author: jroth
ms.openlocfilehash: 71a070de7c74d353be395628566c0bd3f63fd99a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68042737"
---
# <a name="fnsyscollectorgetexecutionstats-transact-sql"></a>fn_syscollector_get_execution_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  傳回有關收集組或封裝的詳細統計資料，其中包括封裝資料流程工作所記錄的錯誤資料列數目。 資料流程工作是處理資料的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 元件。 這些資料為關聯式格式，所以其輸入和輸出資料集會由資料列組成。  
  
 這些統計資料是從 syscollector_execution_stats 檢視中的項目計算而來。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
fn_syscollector_get_execution_stats ( log_id )  
```  
  
## <a name="arguments"></a>引數  
 *log_id*  
 執行記錄的本機唯一識別碼。 *g _ i d*已**int**。  
  
## <a name="table-returned"></a>傳回的資料表  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|avg_row_count_in|**int**|進入封裝之資料流程工作的平均資料列數目。<br /><br /> 注意:資料流程工作是處理資料的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 元件。 這些資料為關聯式格式，所以其輸入資料集是由資料列所組成。 這是進入此工作的資料列數目。 在轉換資料之後，這些資料會當做由資料列組成的結果集輸出。 資料流程工作會轉換資料，並輸出由資料列組成的結果集。 這個輸出是結束工作的資料列數目。|  
|min_row_count_in|**int**|進入封裝之資料流程工作的最小資料列數目。|  
|max_row_count_in|**int**|進入封裝之資料流程工作的最大資料列數目。|  
|avg_row_count_out|**int**|結束封裝之資料流程工作的平均資料列數目。|  
|min_row_count_out|**int**|結束封裝之資料流程工作的最小資料列數目。|  
|max_row_count_out|**int**|結束封裝之資料流程工作的最大資料列數目。|  
|avg_duration|**int**|在封裝之資料流程元件中花費的平均時間 (以毫秒為單位)。|  
|min_duration|**int**|在封裝之資料流程元件中花費的最少時間 (以毫秒為單位)。|  
|max_duration|**int**|在封裝之資料流程元件中花費的最多時間 (以毫秒為單位)。|  
  
## <a name="permissions"></a>Permissions  
 需要 SELECT **dc_operator**。  
  
## <a name="see-also"></a>另請參閱  
 [syscollector_execution_stats &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-catalog-views/syscollector-execution-stats-transact-sql.md)   
 [[資料收集]](../../relational-databases/data-collection/data-collection.md)  
  
  
