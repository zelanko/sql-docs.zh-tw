---
description: catalog.create_execution (SSISDB 資料庫)
title: catalog.create_execution (SSISDB 資料庫) | Microsoft Docs
ms.custom: ''
ms.date: 12/16/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 45d0c2f6-1f38-445f-ac06-e2a01f6ac600
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d0170a6b6a3733b54c24be1f06e91a6a60135faf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456933"
---
# <a name="catalogcreate_execution-ssisdb-database"></a>catalog.create_execution (SSISDB 資料庫)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中建立執行執行個體。  
  
 此預存程序會使用預設伺服器記錄層級。  
  
## <a name="syntax"></a>語法  
  
```sql  
catalog.create_execution [ @folder_name = ] folder_name  
     , [ @project_name = ] project_name  
     , [ @package_name = ] package_name  
  [  , [ @reference_id = ] reference_id ]  
  [  , [ @use32bitruntime = ] use32bitruntime ] 
  [  , [ @runinscaleout = ] runinscaleout ]
  [  , [ @useanyworker = ] useanyworker ] 
     , [ @execution_id = ] execution_id OUTPUT  
```  
  
## <a name="arguments"></a>引數  
 [@folder_name =] *folder_name*  
 包含所要執行之封裝的資料夾名稱。 *folder_name* 是 **nvarchar(128)** 。  
  
 [@project_name =] *project_name*  
 包含所要執行之封裝的專案名稱。 *project_name* 是 **nvarchar(128)** 。  
  
 [@package_name =] *package_name*  
 要執行之封裝的名稱。 *package_name* 是 **nvarchar(260)**。  
  
 [@reference_id =] *reference_id*  
 環境參考的唯一識別碼。 這是選擇性參數。 *reference_id* 是 **bigint**。  
  
 [@use32bitruntime =] *use32bitruntime*  
 指出是否要使用 32 位元執行階段，在 64 位元作業系統上執行封裝。 使用 1 值，即可在執行 64 位元作業系統時執行含 32 位元執行階段的套件。 使用 0 值，即可在執行 64 位元作業系統時執行 64 位元執行階段。 這是選擇性參數。 *Use32bitruntime* 是 **bit**。  
 
 [@runinscaleout =] *runinscaleout*  
 指出是否以擴增執行。使用 1 值，即可使用擴增執行套件。使用 0 值，即可不使用擴增執行套件。這是選擇性參數。 如果未指定，會在 [SSISDB].[catalog].[catalog_properties] 中將其值設定為 DEFAULT_EXECUTION_MODE。 *runinscaleout* 是 **bit**。 
 
[@useanyworker =] *useanyworker*  
指出是否允許任何 Scale Out Worker 進行執行。

-   使用 1 值，即可執行含任何 Scale Out Worker 的套件。 當您將 `@useanyworker` 設為 true，尚未達到最大工作計數 (如背景工作設定檔中指定) 的任何背景工作，都可執行套件。 如需背景工作設定檔的資訊，請參閱 [Integration Services (SSIS) Scale Out 背景工作](../scale-out/integration-services-ssis-scale-out-worker.md)。

-   使用 0 值，即可指出不允許所有 Scale Out Worker 執行套件。 當您將 `@useanyworker` 設為 false，您必須使用 Scale Out Manager，或藉由呼叫預存程序 `[catalog].[add_execution_worker]`，指定允許執行套件的背景工作。 如果您指定的背景工作已執行另一個套件，背景工作在完成執行目前的套件之後會要求執行另一個套件。

這是選擇性參數。 如果未指定，會將其值設定為 1。 *useanyworker* 是 **bit**。 
  
 [@execution_id =] *execution_id*  
 傳回執行執行個體的唯一識別碼。 *execution_id* 是 **bigint**。  

  
## <a name="remarks"></a>備註  
 執行是用以指定在封裝執行的單一執行個體期間，該封裝所使用的變數值。  
  
 如果使用 *reference_id* 參數指定環境參考，則預存程序會將來自對應環境變數的常值或參考值填入專案和套件參數。 如果指定了環境參考，封裝執行期間就會使用預設參數值。 若要精確地判斷哪些值用於執行的特定執行個體，請使用來自此預存程序的 *execution_id* 輸出參數值，並查詢 [execution_parameter_values](../../integration-services/system-views/catalog-execution-parameter-values-ssisdb-database.md) 檢視。  
  
 執行中只能夠指定標示為進入點的封裝。 如果封裝不是已指定的進入點，執行就會失敗。  
  
## <a name="example"></a>範例  
 下列範例呼叫 catalog.create_execution 來建立 Child1.dtsx 套件 (不在 Scale Out 中) 之執行的執行個體。Integration Services Project1 包含此封裝。 本範例呼叫 catalog.set_execution_parameter_value 來設定 Parameter1、Parameter2 和 LOGGING_LEVEL 參數的值。 本範例將呼叫 catalog.start_execution 以啟動執行之執行個體。  
  
```sql  
Declare @execution_id bigint  
EXEC [SSISDB].[catalog].[create_execution] @package_name=N'Child1.dtsx', @execution_id=@execution_id OUTPUT, @folder_name=N'TestDeply4', @project_name=N'Integration Services Project1', @use32bitruntime=False, @reference_id=Null  
Select @execution_id  
DECLARE @var0 sql_variant = N'Child1.dtsx'  
EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id, @object_type=20, @parameter_name=N'Parameter1', @parameter_value=@var0  
DECLARE @var1 sql_variant = N'Child2.dtsx'  
EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id, @object_type=20, @parameter_name=N'Parameter2', @parameter_value=@var1  
DECLARE @var2 smallint = 1  
EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id, @object_type=50, @parameter_name=N'LOGGING_LEVEL', @parameter_value=@var2  
EXEC [SSISDB].[catalog].[start_execution] @execution_id  
GO  
```  
  
## <a name="return-code-value"></a>傳回碼值  
 0 (成功)  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="permissions"></a>權限  
 這個預存程序需要下列其中一個權限：  
  
-   專案的 READ 與 EXECUTE 權限，以及 (如果適用的話) 參考環境的 READ 權限  
  
-   **ssis_admin** 資料庫角色的成員資格  
  
-   **系統管理員**伺服器角色的成員資格  

 如果 @runinscaleout 是 1，則預存程序需要下列其中一個權限：
 
-   **ssis_admin** 資料庫角色的成員資格

-   **ssis_cluster_executor** 資料庫角色的成員資格

-   **系統管理員**伺服器角色的成員資格
  
## <a name="errors-and-warnings"></a>錯誤和警告  
 下列清單描述的是可能引發錯誤或警告的某些狀況：  
  
-   封裝不存在。  
  
-   使用者未具備適當的權限。  
  
-   環境參考 *reference_id* 無效。  
  
-   指定的封裝不是進入點封裝。  
  
-   參考的環境變數其資料類型與專案或封裝參數的資料類型不同。  
  
-   專案或封裝包含需要值的參數，但未指派任何值。  
  
-   在環境參考 *reference_id* 所指定的環境中找不到參考的環境變數。  
  
## <a name="see-also"></a>另請參閱  
 [catalog.start_execution &#40;SSISDB 資料庫&#41;](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md)   
 [catalog.set_execution_parameter_value &#40;SSISDB 資料庫&#41;](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md)  
 [catalog.add_execution_worker &#40;SSISDB 資料庫&#41;](../../integration-services/system-stored-procedures/catalog-add-execution-worker-ssisdb-database.md)  
  
