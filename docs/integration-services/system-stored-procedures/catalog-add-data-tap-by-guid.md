---
title: "catalog.add_data_tap_by_guid |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
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
ms.assetid: ed9d7fa3-61a1-4e21-ba43-1ead7dfc74eb
caps.latest.revision: 15
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 9bd4ecb4a6a419f1965a349d46d16d764dd83708
ms.contentlocale: zh-tw
ms.lasthandoff: 09/26/2017

---
# <a name="catalogadddatatapbyguid"></a>catalog.add_data_tap_by_guid
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  針對執行的執行個體，在封裝資料流程中，將資料點選加入至特定的資料流程路徑。  
  
## <a name="syntax"></a>語法  
  
```sql  
catalog add_data_tap_by_guid [ @execution_id = ] execution_id  
, [ @dataflow_task_guid = ] dataflow_task_guid   
, [ @dataflow_path_id_string = ] dataflow_path_id_string  
, [ @data_filename = ] data_filename  
, [ @max_rows = ] max_rows  
, [ @data_tap_id = ] data_tap_id  
```  
  
## <a name="arguments"></a>引數  
 [ @execution_id =] *execution_id*  
 含有封裝之執行的執行識別碼。 *Execution_id*是**bigint**。  
  
 [ @dataflow_task_guid =] *dataflow_task_guid*  
 封裝中包含要點選之資料流程路徑的資料工作流程識別碼。 *Dataflow_task_guid*是**uniqueidentifier**。  
  
 [ @dataflow_path_id_string =] *dataflow_path_id_string*  
 資料流程路徑的識別字串。 路徑會連接兩個資料流程元件。 **IdentificationString**路徑屬性指定的字串。  
  
 若要尋找識別字串，在[!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]之間兩個資料流程元件，然後按一下路徑上按一下滑鼠右鍵**屬性**。 **IdentificationString**屬性會出現在**屬性**視窗。  
  
 *Dataflow_path_id_string*是**nvarchar （4000)**。  
  
 [ @data_filename =] *data_filename*  
 儲存點選資料的檔案名稱。 如果資料流程工作是在 Foreach 迴圈或 For 迴圈容器中執行，個別檔案會針對迴圈的每次反覆運算，來儲存點選資料。 每個檔案都會以對應於反覆運算的號碼為字首。 資料點選檔案會寫入至資料夾"*\<SQL Server 安裝資料夾 >*\130\DTS\\"。 *Data_filename*是**nvarchar （4000)**。  
  
 [ @max_rows =] max_rows  
 在資料點選期間擷取的資料列數目。 如果沒有指定此值，則會擷取所有資料列。 Max_rows 為**int**。  
  
 [ @data_tap_id =] *data_tap_id*  
 資料點選的識別碼。 *Data_tap_id*是**bigint**。  
  
## <a name="example"></a>範例  
 在下列範例中，資料流程路徑上建立資料點選`Paths[SRC DimDCVentor.OLE DB Source Output]`，請在資料流程工作`{D978A2E4-E05D-4374-9B05-50178A8817E8}`。 點選資料會儲存在 DCVendorOutput.csv 檔案中。  
  
```sql
exec catalog.add_data_tap_by_guid   @execution_id,   
'{D978A2E4-E05D-4374-9B05-50178A8817E8}',   
'Paths[SRC DimDCVentor.OLE DB Source Output]',   
'D:\demos\datafiles\DCVendorOutput.csv'  
```  
  
## <a name="remarks"></a>備註  
 若要加入資料點選，執行的執行個體必須是處於已建立狀態 (1 中的值**狀態**資料行[catalog.operations &#40;SSISDB 資料庫 &#41;](../../integration-services/system-views/catalog-operations-ssisdb-database.md)檢視)。 狀態值會在您進行執行時變更。 您可以建立執行時藉由呼叫[catalog.create_execution &#40;SSISDB 資料庫 &#41;](../../integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database.md).  
  
 以下是 add_data_tap_by_guid 預存程序的考量事項。  
  
-   當您加入資料點選時，在執行封裝之前不會進行驗證。  
  
-   建議您限制在資料點選期間擷取的資料列數目，以避免產生大型資料檔案。 如果執行預存程序的電腦將資料檔案的儲存空間用盡，預存程序就會停止執行。  
  
-   執行 add_data_tap_by_guid 預存程序會影響封裝的效能。 建議您只在進行資料問題的疑難排解時，才執行預存程序。  
  
-   若要存取儲存點選資料的檔案，您必須在執行預存程序所在電腦上擁有管理員權限，或者您必須是開始執行包含擁有資料點選之封裝的使用者。  
  
## <a name="return-codes"></a>傳回碼  
 0 (成功)  
  
 當預存程序失敗時，會擲回錯誤。  
  
## <a name="result-set"></a>結果集  
 無  
  
## <a name="permissions"></a>Permissions  
 這個預存程序需要下列其中一個權限：  
  
-   執行的執行個體之 MODIFY 權限  
  
-   成員資格**ssis_admin**資料庫角色  
  
-   成員資格**sysadmin**伺服器角色  
  
## <a name="errors-and-warnings"></a>錯誤和警告  
 下列清單描述會導致預存程序失敗的情況。  
  
-   使用者沒有 MODIFY 權限。  
  
-   指定封裝中已加入指定元件的資料點選。  
  
-   對於所要擷取的資料列數目，所指定的值無效。  
  
## <a name="requirements"></a>需求  
  
## <a name="see-also"></a>另請參閱  
 [catalog.add_data_tap](../../integration-services/system-stored-procedures/catalog-add-data-tap.md)  
  
  

