---
title: sys.sp_cdc_generate_wrapper_function (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_cdc_generate_wrapper_function_TSQL
- sp_cdc_generate_wrapper_function
- sys.sp_cdc_generate_wrapper_function_TSQL
- sys.sp_cdc_generate_wrapper_function
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_cdc_generate_wrapper_function
- sp_cdc_generate_wrapper_function
ms.assetid: 85bc086d-8a4e-4949-a23b-bf53044b925c
caps.latest.revision: 11
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 0f8f81b97ad6b1c1bf09ee33bd460aab01872327
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="sysspcdcgeneratewrapperfunction-transact-sql"></a>sys.sp_cdc_generate_wrapper_function (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  針對可在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中使用的異動資料擷取查詢函數產生可建立包裝函數的指令碼。 產生之包裝函數所支援的 API 可讓您將查詢間隔指定為日期時間間隔。 這樣可讓此函數方便用於許多倉儲應用程式中，包括由使用異動資料擷取技術來判斷累加式載入之 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝設計師所開發的應用程式。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sys.sp_cdc_generate_wrapper_function  
    [ [ @capture_instance sysname = ] 'capture_instance'  
    [ , [ @closed_high_end_point = ] closed_high_end_pt  
    [ , [ @column_list = ] 'column_list'  
```  
  
```  
  
[ , [ @update_flag_list = ] 'update_flag_list'  
```  
  
## <a name="arguments"></a>引數  
 [ @capture_instance=] '*capture_instance*'  
 這是即將產生指令碼的擷取執行個體。 *capture_instance*是**sysname**且具有預設值是 NULL。 如果您省略了此值或將它明確設定為 NULL，系統就會針對所有擷取執行個體產生包裝函數指令碼。  
  
 [ @closed_high_end_point=] *high_end_pt_flag*  
 這是旗標位元，它會指出認可時間等於高端點的變更是否要由產生的程序包含在擷取間隔中。 *high_end_pt_flag*是**元**且具有預設值是 1，表示應該包含端點。 值為 0 表示所有認可時間都將確實小於高端點。  
  
 [ @column_list=] '*column_list*'  
 這是即將包含在包裝函數所傳回之結果集中的已擷取資料行清單。 *column_list*是**nvarchar （max)** 且具有預設值是 NULL。 當您指定了 NULL 時，就會包含所有已擷取的資料行。  
  
 [ @update_flag_list=] '*update_flag_list*'  
 這是更新旗標包含在包裝函數所傳回之結果集中的已包含資料行清單。 *update_flag_list*是**nvarchar （max)** 且具有預設值是 NULL。 當您指定了 NULL 時，就不會包含任何更新旗標。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料行類型|Description|  
|-----------------|-----------------|-----------------|  
|**function_name**|**nvarchar(145)**|產生之函數的名稱。|  
|**create_script**|**nvarchar(max)**|這是建立擷取執行個體包裝函數的指令碼。|  
  
## <a name="remarks"></a>備註  
 系統一定會產生建立函數來包裝擷取執行個體之所有變更查詢的指令碼。 如果擷取執行個體支援淨變更查詢，就會一併產生針對此查詢產生包裝函數的指令碼。  
  
## <a name="examples"></a>範例  
 下列範例將示範如何使用 `sys.sp_cdc_generate_wrapper_function`，針對所有異動資料擷取函數建立包裝函數。  
  
```  
DECLARE @wrapper_functions TABLE (  
    function_name sysname,  
    create_script nvarchar(max));  
  
INSERT INTO @wrapper_functions  
EXEC sys.sp_cdc_generate_wrapper_function;  
  
DECLARE @create_script nvarchar(max);  
DECLARE #hfunctions CURSOR LOCAL fast_forward  
FOR   
    SELECT create_script FROM @wrapper_functions;  
  
OPEN #hfunctions;  
FETCH #hfunctions INTO @create_script;  
WHILE (@@fetch_status <> -1)  
BEGIN  
    EXEC sp_executesql @create_script  
    FETCH #hfunctions INTO @create_script  
END;  
  
CLOSE #hfunctions;  
DEALLOCATE #hfunctions;  
```  
  
## <a name="see-also"></a>另請參閱  
 [異動資料擷取預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/change-data-capture-stored-procedures-transact-sql.md)   
 [異動資料擷取&#40;SSIS&#41;](../../integration-services/change-data-capture/change-data-capture-ssis.md)  
  
  
