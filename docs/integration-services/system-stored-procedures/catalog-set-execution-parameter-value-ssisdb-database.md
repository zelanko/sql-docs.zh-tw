---
title: "catalog.set_execution_parameter_value （SSISDB 資料庫） |Microsoft 文件"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 055d86c9-befd-4e63-acb1-6dfe833549d2
caps.latest.revision: 20
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: c3e47e4a5ae297202ba43679fba393421880a7ea
ms.openlocfilehash: 7b13e7b1c28bad6e573e829183372da4bb62f92d
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="catalogsetexecutionparametervalue-ssisdb-database"></a>catalog.set_execution_parameter_value (SSISDB 資料庫)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

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
 [ @execution_id =] *execution_id*  
 執行之執行個體的唯一識別碼。 *Execution_id*是**bigint**。  
  
 [ @object_type =] *object_type*  
 參數類型。  
  
 下列的參數，設定*object_type*為 50  
  
-   LOGGING_LEVEL  
  
-   CUSTOMIZED_LOGGING_LEVEL  
  
-   DUMP_ON_ERROR  
  
-   DUMP_ON_EVENT  
  
-   DUMP_EVENT_CODE  
  
-   CALLER_INFO  
  
-   SYNCHRONIZED  
  
 使用 `20` 值表示專案參數，或使用 `30` 值表示封裝參數。  
  
 *Object_type*是**smallint**。  
  
 [ @parameter_name =] *parameter_name*  
 參數的名稱。 *Parameter_name*是**nvarchar （128)**。  
  
 [ @parameter_value =] *parameter_value*  
 參數的值。 *Parameter_value*是**sql_variant**。  
  
## <a name="remarks"></a>備註  
 若要找出用於給定執行的參數值，請查詢 catalog.execution_parameter_values 檢視。  
  
 指定的範圍會在封裝執行期間所記錄的資訊，請設定*parameter_name* LOGGING_LEVEL，並將以*parameter_value*至下列值之一。  
  
 設定*object_type*參數設為 50。  
  
|Value|설명|  
|-----------|-----------------|  
|0|無<br /><br /> 關閉記錄功能。 只記錄封裝執行狀態。|  
|1|Basic<br /><br /> 記錄所有事件，自訂和診斷事件除外。 這是預設值。|  
|2|效能<br /><br /> 只記錄效能統計資料，以及 OnError 和 OnWarning 事件。|  
|3|Verbose<br /><br /> 記錄所有事件，包括自訂和診斷事件。 <br />自訂事件，包括 Integration Services 工作所記錄的那些事件。 如需詳細資訊，請參閱[自訂訊息以進行記錄](../../integration-services/performance/integration-services-ssis-logging.md#custom_messages)|  
|4|執行階段歷程<br /><br /> 收集追蹤資料流程中的歷程所需的資料。|  
|100|自訂記錄層級<br /><br /> CUSTOMIZED_LOGGING_LEVEL 參數中指定的設定。 如需您可以指定值的詳細資訊，請參閱[catalog.create_customized_logging_level](../../integration-services/system-stored-procedures/catalog-create-customized-logging-level.md)。<br /><br /> 如需自訂的記錄層級的詳細資訊，請參閱[Enable Logging for Package Execution on the SSIS Server](../../integration-services/performance/integration-services-ssis-logging.md#server_logging)。|  
  
 若要指定 Integration Services 伺服器在封裝執行期間發生任何錯誤時產生傾印檔案，請針對尚未執行之執行的執行個體，設定下列參數值。  
  
|매개 변수|Value|  
|---------------|-----------|  
|*execution_id*|執行的執行個體之唯一識別碼|  
|*object_type*|50|  
|*parameter_name*|'DUMP_ON_ERROR|  
|*parameter_value*|1|  
  
 若要指定 Integration Services 伺服器在封裝執行期間發生事件時產生傾印檔案，請針對尚未執行的執行執行個體，設定下列參數值。  
  
|매개 변수|Value|  
|---------------|-----------|  
|*execution_id*|執行的執行個體之唯一識別碼|  
|*object_type*|50|  
|*parameter_name*|'DUMP_ON_EVENT|  
|*parameter_value*|1|  
  
 若要指定封裝執行期間會導致 Integration Services 伺服器產生傾印檔案的事件，請針對尚未執行之執行的執行個體，設定下列參數值。 使用分號來分隔多個事件代碼。  
  
|매개 변수|Value|  
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
  
-   成員資格**ssis_admin**資料庫角色  
  
-   成員資格**sysadmin**伺服器角色  
  
## <a name="errors-and-warnings"></a>錯誤和警告  
 下列清單將描述可能會引發錯誤或警告的某些條件：  
  
-   使用者未具備適當的權限  
  
-   執行識別碼無效  
  
-   參數名稱無效  
  
-   參數值的資料類型與參數的資料類型不相符  
  
## <a name="see-also"></a>另請參閱  
 [catalog.execution_parameter_values &#40;SSISDB 資料庫 &#41;](../../integration-services/system-views/catalog-execution-parameter-values-ssisdb-database.md)   
 [產生封裝執行的傾印檔案](../../integration-services/troubleshooting/generating-dump-files-for-package-execution.md)  
  
  

