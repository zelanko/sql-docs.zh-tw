---
title: sys.databases sp_cdc_generate_wrapper_function （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 3c65ee865a5c4e4bccd11c12846de1a1ca8b5035
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85626029"
---
# <a name="syssp_cdc_generate_wrapper_function-transact-sql"></a>sys.sp_cdc_generate_wrapper_function (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

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
 [ @capture_instance =] '*capture_instance*'  
 這是即將產生指令碼的擷取執行個體。 *capture_instance*為**sysname** ，且預設值為 Null。 如果您省略了此值或將它明確設定為 NULL，系統就會針對所有擷取執行個體產生包裝函數指令碼。  
  
 [ @closed_high_end_point =] *high_end_pt_flag*  
 這是旗標位元，它會指出認可時間等於高端點的變更是否要由產生的程序包含在擷取間隔中。 *high_end_pt_flag*是**bit** ，預設值是1，表示應該包含端點。 值為 0 表示所有認可時間都將確實小於高端點。  
  
 [ @column_list =] '*column_list*'  
 這是即將包含在包裝函數所傳回之結果集中的已擷取資料行清單。 *column_list*是**Nvarchar （max）** ，且預設值為 Null。 當您指定了 NULL 時，就會包含所有已擷取的資料行。  
  
 [ @update_flag_list =] '*update_flag_list*'  
 這是更新旗標包含在包裝函數所傳回之結果集中的已包含資料行清單。 *update_flag_list*是**Nvarchar （max）** ，且預設值為 Null。 當您指定了 NULL 時，就不會包含任何更新旗標。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料行類型|描述|  
|-----------------|-----------------|-----------------|  
|**function_name**|**Nvarchar （145）**|產生之函數的名稱。|  
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
 [變更資料捕獲預存程式 &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/change-data-capture-stored-procedures-transact-sql.md)   
 [變更 Data Capture &#40;SSIS&#41;](../../integration-services/change-data-capture/change-data-capture-ssis.md)  
  
  
