---
title: "catalog.create_execution （SSISDB 資料庫） |Microsoft 文件"
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 45d0c2f6-1f38-445f-ac06-e2a01f6ac600
caps.latest.revision: 18
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: e20b96e38f798c19a74d5f3a32a25e429dc8ebeb
ms.openlocfilehash: 7e9d38935a91bba81359bee7fdbd64dba86d0d26
ms.contentlocale: zh-tw
ms.lasthandoff: 10/20/2017

---
# <a name="catalogcreateexecution-ssisdb-database"></a>catalog.create_execution (SSISDB 資料庫)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中建立執行執行個體。  
  
 此預存程序會使用預設伺服器記錄層級。  
  
## <a name="syntax"></a>語法  
  
```sql  
catalog.create_execution [@folder_name = folder_name  
     , [@project_name =] project_name  
     , [@package_name =] package_name  
  [  , [@reference_id =] reference_id ]  
  [  , [@use32bitruntime =] use32bitruntime ] 
  [  , [@runinscaleout =] runinscaleout ]
  [  , [@useanyworker =] useanyworker ] 
     , [@execution_id =] execution_id OUTPUT  
```  
  
## <a name="arguments"></a>引數  
 [@folder_name =] *folder_name*  
 包含所要執行之封裝的資料夾名稱。 *Folder_name*是**nvarchar （128)**。  
  
 [@project_name =] *project_name*  
 包含所要執行之封裝的專案名稱。 *Project_name*是**nvarchar （128)**。  
  
 [@package_name =] *package_name*  
 要執行之封裝的名稱。 *Package_name*是**nvarchar （260)**。  
  
 [@reference_id =] *e _ i d*  
 環境參考的唯一識別碼。 這個參數是選擇性的。 *E _ i d*是**bigint**。  
  
 [@use32bitruntime =] *use32bitruntime*  
 指出是否要使用 32 位元執行階段，在 64 位元作業系統上執行封裝。 若要在 64 位元作業系統上執行時執行 32 位元執行階段使用值為 1。 使用 0 值，即可在執行 64 位元作業系統時執行 64 位元執行階段。 這個參數是選擇性的。 *Use32bitruntime*是**元**。  
 
 [@runinscaleout =] *runinscaleout*  
 表示是否在向外執行。在向外執行封裝中使用值為 1。使用 0 的值來執行封裝而不向外。這個參數是選擇性的。 如果未指定，會將其值設 DEFAULT_EXECUTION_MODE [SSISDB] 中。[目錄]。[catalog_properties]。 *Runinscaleout*是**元**。 
 
 [@useanyworker =] *useanyworker*  
  指出是否允許任何標尺出背景工作執行時，不要。 您可以使用 1 的值來執行具有任何標尺出背景工作的封裝。 使用值為 0 表示並非所有標尺出背景工作可執行封裝。 這個參數是選擇性的。 如果未指定，會將其值設為 1。 *Useanyworker*是**元**。 
  
 [@execution_id =] *execution_id*  
 傳回執行執行個體的唯一識別碼。 *Execution_id*是**bigint**。  

  
## <a name="remarks"></a>備註  
 執行是用以指定在封裝執行的單一執行個體期間，該封裝所使用的變數值。  
  
 如果您指定了環境參考*e _ i d*參數，預存程序會填入專案和封裝參數與常值或參考來自對應環境變數的值。 如果指定了環境參考，封裝執行期間就會使用預設參數值。 若要判斷哪些值只用於執行的特定執行個體，請使用*execution_id*輸出參數值，這個預存程序和查詢從[execution_parameter_values](../../integration-services/system-views/catalog-execution-parameter-values-ssisdb-database.md)檢視。  
  
 執行中只能夠指定標示為進入點的封裝。 如果封裝不是已指定的進入點，執行就會失敗。  
  
## <a name="example"></a>範例  
 下列範例呼叫 catalog.create_execution 建立 Child1.dtsx 封裝，這不是在向外執行的執行個體。Integration Services Project1 包含此封裝。 本範例呼叫 catalog.set_execution_parameter_value 來設定 Parameter1、Parameter2 和 LOGGING_LEVEL 參數的值。 本範例將呼叫 catalog.start_execution 以啟動執行之執行個體。  
  
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
 無  
  
## <a name="permissions"></a>Permissions  
 這個預存程序需要下列其中一個權限：  
  
-   專案的 READ 與 EXECUTE 權限，以及 (如果適用的話) 參考環境的 READ 權限  
  
-   成員資格**ssis_admin**資料庫角色  
  
-   成員資格**sysadmin**伺服器角色  

 如果@runinscaleout為 1，預存程序需要下列權限之一：
 
-   成員資格**ssis_admin**資料庫角色

-   成員資格**ssis_cluster_executor**資料庫角色

-   成員資格**sysadmin**伺服器角色
  
## <a name="errors-and-warnings"></a>錯誤和警告  
 下列清單描述的是可能引發錯誤或警告的某些狀況：  
  
-   封裝不存在。  
  
-   使用者未具備適當的權限。  
  
-   環境參考*e _ i d*，不正確。  
  
-   指定的封裝不是進入點封裝。  
  
-   參考的環境變數其資料類型與專案或封裝參數的資料類型不同。  
  
-   專案或封裝包含需要值的參數，但未指派任何值。  
  
-   環境參考的環境中找不到參考的環境變數*e _ i d*，指定。  
  
## <a name="see-also"></a>另請參閱  
 [catalog.start_execution &#40;SSISDB 資料庫 &#41;](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md)   
 [catalog.set_execution_parameter_value &#40;SSISDB 資料庫&#41;](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md)  
 [catalog.add_execution_worker &#40;SSISDB 資料庫 &#41;](../../integration-services/system-stored-procedures/catalog-add-execution-worker-ssisdb-database.md)  
  

