---
title: "catalog.set_execution_parameter_value (SSISDB 資料庫) | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 055d86c9-befd-4e63-acb1-6dfe833549d2
caps.latest.revision: "20"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 233eed5038eb8a2f63e89cbadc5ea738398b8d8b
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="catalogsetexecutionparametervalue-ssisdb-database"></a>catalog.set_execution_parameter_value (SSISDB 資料庫)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  為 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中執行的執行個體設定參數值。  
  
 執行的執行個體啟動之後，參數值就無法變更。  
  
## <a name="syntax"></a>語法  
  
```sql  
catalog.set_execution_parameter_value [ @execution_id = execution_id  
    , [ @object_type = ] object_type  
    , [ @parameter_name = ] parameter_name  
    , [ @parameter_value = ] parameter_value  
```  
  
## <a name="arguments"></a>引數  
 [ @execution_id = ] *execution_id*  
 執行之執行個體的唯一識別碼。 *execution_id* 是 **bigint**。  
  
 [ @object_type = ] *object_type*  
 參數類型。  
  
 將下列參數的 *object_type* 設為 50  
  
-   LOGGING_LEVEL  
  
-   CUSTOMIZED_LOGGING_LEVEL  
  
-   DUMP_ON_ERROR  
  
-   DUMP_ON_EVENT  
  
-   DUMP_EVENT_CODE  
  
-   CALLER_INFO  
  
-   SYNCHRONIZED  
  
 使用 `20` 值表示專案參數，或使用 `30` 值表示封裝參數。  
  
 *object_type* 是 **smallint**。  
  
 [ @parameter_name = ] *parameter_name*  
 參數的名稱。 *parameter_name* 是 **nvarchar(128)**。  
  
 [ @parameter_value = ] *parameter_value*  
 參數的值。 *parameter_value* 是 **sql_variant**。  
  
## <a name="remarks"></a>備註  
 若要找出用於給定執行的參數值，請查詢 catalog.execution_parameter_values 檢視。  
  
 若要指定套件執行期間所記錄的資訊範圍，請將 *parameter_name* 設為 LOGGING_LEVEL，並將 *parameter_value* 設為下列其中一個值。  
  
 將 *object_type*參數設為 50。  
  
|值|描述|  
|-----------|-----------------|  
|0|無<br /><br /> 關閉記錄功能。 只記錄封裝執行狀態。|  
|1|Basic<br /><br /> 記錄所有事件，自訂和診斷事件除外。 這是預設值。|  
|2|效能<br /><br /> 只記錄效能統計資料，以及 OnError 和 OnWarning 事件。|  
|3|[詳細資訊]<br /><br /> 記錄所有事件，包括自訂和診斷事件。 <br />自訂事件，包括 Integration Services 工作所記錄的那些事件。 如需詳細資訊，請參閱[自訂訊息以進行記錄](../../integration-services/performance/integration-services-ssis-logging.md#custom_messages)|  
|4|執行階段歷程<br /><br /> 收集追蹤資料流程中歷程所需的資料。|  
|100|自訂記錄層次<br /><br /> 指定 CUSTOMIZED_LOGGING_LEVEL 參數中的設定。 如需可指定值的詳細資訊，請參閱 [catalog.create_customized_logging_level](../../integration-services/system-stored-procedures/catalog-create-customized-logging-level.md)。<br /><br /> 如需自訂記錄層次的詳細資訊，請參閱[在 SSIS 伺服器上啟用套件執行的記錄功能](../../integration-services/performance/integration-services-ssis-logging.md#server_logging)。|  
  
 若要指定 Integration Services 伺服器在封裝執行期間發生任何錯誤時產生傾印檔案，請針對尚未執行之執行的執行個體，設定下列參數值。  
  
|參數|值|  
|---------------|-----------|  
|*execution_id*|執行的執行個體之唯一識別碼|  
|*object_type*|50|  
|*parameter_name*|'DUMP_ON_ERROR|  
|*parameter_value*|1|  
  
 若要指定 Integration Services 伺服器在封裝執行期間發生事件時產生傾印檔案，請針對尚未執行的執行執行個體，設定下列參數值。  
  
|參數|值|  
|---------------|-----------|  
|*execution_id*|執行的執行個體之唯一識別碼|  
|*object_type*|50|  
|*parameter_name*|'DUMP_ON_EVENT|  
|*parameter_value*|1|  
  
 若要指定封裝執行期間會導致 Integration Services 伺服器產生傾印檔案的事件，請針對尚未執行之執行的執行個體，設定下列參數值。 使用分號來分隔多個事件代碼。  
  
|參數|值|  
|---------------|-----------|  
|*execution_id*|執行的執行個體之唯一識別碼|  
|*object_type*|50|  
|*parameter_name*|DUMP_EVENT_CODE|  
|*parameter_value*|一個或多個事件代碼|  
  
## <a name="example"></a>範例  
 下列範例指定 Integration Services 伺服器在封裝執行期間發生任何錯誤時產生傾印檔案。  
  
```sql
exec catalog.create_execution  'TR2','Recurring ETL', 'Dim_DCVendor.dtsx',NULL, 0,@execution_id out  
exec catalog.set_execution_parameter_value  @execution_id, 50, 'DUMP_ON_ERROR',1  
```  
  
## <a name="example"></a>範例  
 下列範例指定 Integration Services 伺服器在封裝執行期間發生事件時產生傾印檔案，以及指定會導致伺服器產生檔案的事件。  
  
```sql
exec catalog.create_execution  'TR2','Recurring ETL', 'Dim_DCVendor.dtsx',NULL, 0,@execution_id out  
exec catalog.set_execution_parameter_value  @execution_id, 50, 'DUMP_ON_EVENT',1  
  
declare @event_code nvarchar(50)  
set @event_code = '0xC020801C'  
exec catalog.set_execution_parameter_value  @execution_id, 50, 'DUMP_EVENT_CODE', @event_code  
```  
  
## <a name="return-code-value"></a>傳回碼值  
 0 (成功)  
  
## <a name="result-sets"></a>結果集  
 無  
  
## <a name="permissions"></a>Permissions  
 這個預存程序需要下列其中一個權限：  
  
-   執行的執行個體之 READ 和 MODIFY 權限  
  
-   **ssis_admin** 資料庫角色的成員資格  
  
-   **sysadmin** 伺服器角色的成員資格  
  
## <a name="errors-and-warnings"></a>錯誤和警告  
 下列清單將描述可能會引發錯誤或警告的某些條件：  
  
-   使用者未具備適當的權限  
  
-   執行識別碼無效  
  
-   參數名稱無效  
  
-   參數值的資料類型與參數的資料類型不相符  
  
## <a name="see-also"></a>另請參閱  
 [catalog.execution_parameter_values &#40;SSISDB 資料庫&#41;](../../integration-services/system-views/catalog-execution-parameter-values-ssisdb-database.md)   
 [產生套件執行的傾印檔案](../../integration-services/troubleshooting/generating-dump-files-for-package-execution.md)  
  
  
