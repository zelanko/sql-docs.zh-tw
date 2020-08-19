---
description: sp_check_dynamic_filters (Transact-SQL)
title: sp_check_dynamic_filters (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- dynamic_filters_TSQL
- sp_check_TSQL
- check
- sp_check_dynamic filter
- check_TSQL
- filters_TSQL
- check_dynamic_filters_TSQL
- dynamic filters
- filters
- check dynamic filters
- sp_check_dynamic filter_TSQL
- sp_check_for_sync_trigger_TSQL
- sp_check
helpviewer_keywords:
- sp_check_dynamic_filters
ms.assetid: dd7760db-a3a5-460f-bd97-b8d436015e19
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: a03c61bc663597f27e3305813528edaf3e395635
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88486221"
---
# <a name="sp_check_dynamic_filters-transact-sql"></a>sp_check_dynamic_filters (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  顯示發行集之參數化資料列篩選器屬性的相關資訊，尤其是用來產生發行集篩選資料分割的函數，以及發行集是否適合使用預先計算的資料分割。 這個預存程序執行於發行集資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_check_dynamic_filters [ @publication = ] 'publication'  
```  
  
## <a name="arguments"></a>引數  
`[ @publication = ] 'publication'` 這是發行集的名稱。 *發行* 集是 **sysname**，沒有預設值。  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**can_use_partition_groups**|**bit**|這是指發行集是否符合使用預先計算分割區的資格;其中 **1** 表示可以使用預先計算的資料分割，而 **0** 表示無法使用它們。|  
|**has_dynamic_filters**|**bit**|如果在發行集內至少定義了一個參數化資料列篩選器，則為。其中 **1** 表示有一或多個參數化資料列篩選存在，而 **0** 表示沒有任何動態篩選存在。|  
|**dynamic_filters_function_list**|**Nvarchar (500) **|用來篩選發行集中的發行項之函數清單，每個函數都用分號來分開。|  
|**validate_subscriber_info**|**Nvarchar (500) **|用來篩選發行集中的發行項之函數清單，每個函數都用加號 (+) 來分開。|  
|**uses_host_name**|**bit**|如果在參數化資料列篩選器中使用 [HOST_NAME ( # B1 ](../../t-sql/functions/host-name-transact-sql.md) 函數， **1** 表示此函式用於動態篩選。|  
|**uses_suser_sname**|**bit**|如果在參數化資料列篩選器中使用 [SUSER_SNAME ( # B1 ](../../t-sql/functions/suser-sname-transact-sql.md) 函數， **1** 表示此函式用於動態篩選。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="remarks"></a>備註  
 **sp_check_dynamic_filters** 用於合併式複寫中。  
  
 如果發行集已定義為使用預先計算的資料分割， **sp_check_dynamic_filters** 會檢查是否違反預先計算資料分割的限制。 如果找到任何違反限制的情況，便會傳回錯誤。 如需詳細資訊，請參閱[使用預先計算的資料分割最佳化參數化篩選效能](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md)。  
  
 如果已將發行集定義為有參數化資料列篩選器，但找不到參數化資料列篩選器，便會傳回錯誤。  
  
## <a name="permissions"></a>權限  
 只有 **系統管理員（sysadmin** ）固定伺服器角色或 **db_owner** 固定資料庫角色的成員，才能夠執行 **sp_check_dynamic_filters**。  
  
## <a name="see-also"></a>另請參閱  
 [使用參數化篩選來管理合併式發行集的資料分割](../../relational-databases/replication/publish/manage-partitions-for-a-merge-publication-with-parameterized-filters.md)   
 [sp_check_join_filter &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-check-join-filter-transact-sql.md)   
 [sp_check_subset_filter &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-check-subset-filter-transact-sql.md)  
  
  
