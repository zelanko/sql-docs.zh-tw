---
title: "catalog.create_customized_logging_level |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 20b3ba0a-126f-49bf-b70f-61b2a0fcb750
caps.latest.revision: 9
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 126fa0af811033bb0be035b1f4c550620c696bb3
ms.contentlocale: zh-tw
ms.lasthandoff: 09/26/2017

---
# <a name="catalogcreatecustomizedlogginglevel"></a>catalog.create_customized_logging_level
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  建立新的自訂的記錄層級。 如需自訂的記錄層級的詳細資訊，請參閱[Integration Services &#40;SSIS &#41;記錄](../../integration-services/performance/integration-services-ssis-logging.md)。  
  
## <a name="syntax"></a>語法  
  
```sql  
catalog.create_customized_logging_level [ @level_name = ] level_name  
    , [ @level_description = ] level_description  
    , [ @profile_value = ] profile_value  
    , [ @event_value = ] event_value  
    , [ @level_id = ] level_id OUT   
```  
  
## <a name="arguments"></a>引數  
 [ @level_name =] *l*  
 針對新的現有名稱的自訂記錄層次。  
  
 *l*是**nvarchar （128)**。  
  
 [ @level_description =] *level_description*  
 描述新現有的自訂記錄層級。  
  
 *Level_description*是**nvarchar （1024)**。  
  
 [ @profile_value =] *profile_value*  
 您想要新的統計資料的自訂記錄層次記錄。  
  
 統計資料的有效值包括以下項目。 這些值對應至值上**統計資料** 索引標籤**自訂記錄層級管理** 對話方塊。  
  
-   執行 = 0  
  
-   磁碟區 = 1  
  
-   效能 = 2  
  
 *Profile_value*是**bigint**。  
  
 [ @event_value =] *event_value*  
 您想要新的事件可自訂記錄層級，記錄。  
  
 事件的有效值包括以下項目。 這些值對應至值上**事件** 索引標籤**自訂記錄層級管理** 對話方塊。  
  
|沒有事件內容的事件|事件的事件內容|  
|----------------------------------|-------------------------------|  
|OnVariableValueChanged = 0<br /><br /> OnExecutionStatusChanged = 1<br /><br /> OnPreExecute = 2<br /><br /> OnPostExecute = 3<br /><br /> OnPreValidate = 4<br /><br /> OnPostValidate = 5<br /><br /> OnWarning = 6<br /><br /> OnInformation = 7<br /><br /> OnError = 8<br /><br /> OnTaskFailed = 9<br /><br /> OnProgress = 10<br /><br /> OnQueryCancel = 11<br /><br /> OnBreakpointHit = 12<br /><br /> OnCustomEvent = 13<br /><br /> 診斷 = 14<br /><br /> DiagnosticEx = 15<br /><br /> NonDiagnostic = 16|OnVariableValueChanged_IncludeContext = 32<br /><br /> OnExecutionStatusChanged_IncludeContext = 33<br /><br /> OnPreExecute_IncludeContext = 34<br /><br /> OnPostExecute_IncludeContext = 35<br /><br /> OnPreValidate_IncludeContext = 36<br /><br /> OnPostValidate_IncludeContext = 37<br /><br /> OnWarning_IncludeContext = 38<br /><br /> OnInformation_IncludeContext = 39<br /><br /> OnError_IncludeContext = 40<br /><br /> OnTaskFailed_IncludeContext = 41<br /><br /> OnProgress_IncludeContext = 42<br /><br /> OnQueryCancel_IncludeContext = 43<br /><br /> OnBreakpointHit_IncludeContext = 44<br /><br /> OnCustomEvent_IncludeContext = 45<br /><br /> Diagnostic_IncludeContext = 46<br /><br /> DiagnosticEx_IncludeContext = 47<br /><br /> NonDiagnostic_IncludeContext = 48|  
  
 *Event_value*是**bigint**。  
  
 [ @level_id =] *level_id*出  
 新識別碼的自訂記錄層次。  
  
 *Level_id*是**bigint**。  
  
## <a name="remarks"></a>備註  
 若要結合多個值的 TRANSACT-SQL 中*profile_value*或*event_value*引數，請依照這個範例。 若要擷取 OnError (8) 和 (15) DiagnosticEx 事件，來計算公式*event_value*是`2^8 + 2^15 = 33024`。  
  
## <a name="return-codes"></a>傳回碼  
 0 (成功)  
  
 當預存程序失敗時，會擲回錯誤。  
  
## <a name="result-set"></a>結果集  
 無  
  
## <a name="permissions"></a>Permissions  
 這個預存程序需要下列其中一個權限：  
  
-   **ssis_admin** 資料庫角色中的成員資格  
  
-   **sysadmin** 伺服器角色中的成員資格  
  
## <a name="errors-and-warnings"></a>錯誤和警告  
 下列清單描述會導致預存程序失敗的情況。  
  
-   使用者沒有必要的權限。  
  
  

