---
title: sp_check_join_filter (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
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
- filter_TSQL
- sp_check_TSQL
- sp_check_join_filter
- sp_check_join_filter_TSQL
- join
- join_TSQL
- filter
- sp_check
helpviewer_keywords:
- sp_check_join_filter
ms.assetid: e9699d59-c8c9-45f6-a561-f7f95084a540
caps.latest.revision: 14
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 83e25f05600cb1a9319b865c4f7e0340e139dec5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32991105"
---
# <a name="spcheckjoinfilter-transact-sql"></a>sp_check_join_filter (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  用來驗證兩個資料表之間的聯結篩選，以判斷聯結篩選子句是否有效。 這個預存程序也會傳回有關所提供之聯結篩選的資訊，包括它是否能夠搭配使用給定資料表之預先計算的資料分割。 這個預存程序執行於發行集的發行者端。 如需詳細資訊，請參閱[使用預先計算的資料分割最佳化參數化篩選效能](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_check_join_filter [ @filtered_table = ] 'filtered_table'  
        , [@join_table = ] 'join_table'  
        , [ @join_filterclause = ] 'join_filterclause'  
```  
  
## <a name="arguments"></a>引數  
 [ **@filtered_table**=] **'***filtered_table***'**  
 這是篩選的資料表名稱。 *filtered_table*是**nvarchar （400)**，沒有預設值。  
  
 [ **@join_table**=] **'***join_table***'**  
 針對聯結的資料表名稱*filtered_table*。 *join_table*是**nvarchar （400)**，沒有預設值。  
  
 [ **@join_filterclause** =] **'***join_filterclause***'**  
 這是正在測試的聯結篩選子句。 *join_filterclause*是**nvarchar （1000)**，沒有預設值。  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**can_use_partition_groups**|**bit**|是發行集是否為預先計算的資料分割;其中**1**表示可以使用指出資料分割，以及**0**表示，無法使用。|  
|**has_dynamic_filters**|**bit**|提供的篩選子句包含至少一個參數化篩選函數。其中**1**表示會使用參數化篩選函數，以及**0**表示，不會使用這類函式。|  
|**dynamic_filters_function_list**|**nvarchar(500)**|篩選子句中定義發行項參數化篩選的函數清單，其中每個函數皆以分號加以分隔。|  
|**uses_host_name**|**bit**|如果[host_name （)](../../t-sql/functions/host-name-transact-sql.md)函數是否用於篩選子句中，其中**1**表示存在於此函式。|  
|**uses_suser_sname**|**bit**|如果[suser_sname （)](../../t-sql/functions/suser-sname-transact-sql.md)函數是否用於篩選子句中，其中**1**表示存在於此函式。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_check_join_filter**用於合併式複寫中。  
  
 **sp_check_join_filter**可以執行對任何相關資料表中，即使它們尚未發行。 在定義兩個發行項之間的聯結篩選之前，您可以使用這個預存程序，先驗證聯結篩選子句。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_check_join_filter**。  
  
## <a name="see-also"></a>另請參閱  
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
