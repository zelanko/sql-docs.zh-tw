---
title: catalog.add_data_tap_by_guid | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: language-reference
ms.assetid: ed9d7fa3-61a1-4e21-ba43-1ead7dfc74eb
caps.latest.revision: 15
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c69317a8739a5547042a035c0c2b2fc13cc7d434
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
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
 [ @execution_id = ] *execution_id*  
 含有封裝之執行的執行識別碼。 *execution_id* 是 **bigint**。  
  
 [ @dataflow_task_guid = ] *dataflow_task_guid*  
 封裝中包含要點選之資料流程路徑的資料工作流程識別碼。 *dataflow_task_guid* 是 **uniqueidentifier**。  
  
 [ @dataflow_path_id_string = ] *dataflow_path_id_string*  
 資料流程路徑的識別字串。 路徑會連接兩個資料流程元件。 路徑的 **IdentificationString** 屬性會指定字串。  
  
 若要尋找識別字串，在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 中以滑鼠右鍵按一下兩個資料流程元件之間的路徑，然後按一下 [屬性]。 **IdentificationString** 屬性會出現在 [屬性] 視窗中。  
  
 *dataflow_path_id_string* 是 **nvarchar(4000)**。  
  
 [ @data_filename = ] *data_filename*  
 儲存點選資料的檔案名稱。 如果資料流程工作是在 Foreach 迴圈或 For 迴圈容器中執行，個別檔案會針對迴圈的每次反覆運算，來儲存點選資料。 每個檔案都會以對應於反覆運算的號碼為字首。 資料點選檔案會寫入至資料夾 "\<SQL Server 安裝資料夾>\130\DTS\\"。 *data_filename* 是 **nvarchar(4000)**。  
  
 [ @max_rows = ] max_rows  
 在資料點選期間擷取的資料列數目。 如果沒有指定此值，則會擷取所有資料列。 max_rows 是 **int**。  
  
 [ @data_tap_id = ] *data_tap_id*  
 資料點選的識別碼。 *data_tap_id* 是 **bigint**。  
  
## <a name="example"></a>範例  
 下列範例會在資料流程工作 `{D978A2E4-E05D-4374-9B05-50178A8817E8}` 中的資料流程路徑 `Paths[SRC DimDCVentor.OLE DB Source Output]` 上建立資料點選。 點選資料會儲存在 DCVendorOutput.csv 檔案中。  
  
```sql
exec catalog.add_data_tap_by_guid   @execution_id,   
'{D978A2E4-E05D-4374-9B05-50178A8817E8}',   
'Paths[SRC DimDCVentor.OLE DB Source Output]',   
'D:\demos\datafiles\DCVendorOutput.csv'  
```  
  
## <a name="remarks"></a>Remarks  
 若要新增資料點選，執行的執行個體必須處於已建立狀態 ([catalog.operations &#40;SSISDB 資料庫&#41;](../../integration-services/system-views/catalog-operations-ssisdb-database.md) 檢視之**狀態**資料行中的值為 1)。 狀態值會在您進行執行時變更。 您可以呼叫 [catalog.create_execution &#40;SSISDB 資料庫&#41;](../../integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database.md) 來建立執行。  
  
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
  
-   **ssis_admin** 資料庫角色的成員資格  
  
-   **系統管理員**伺服器角色的成員資格  
  
## <a name="errors-and-warnings"></a>錯誤和警告  
 下列清單描述會導致預存程序失敗的情況。  
  
-   使用者沒有 MODIFY 權限。  
  
-   指定封裝中已加入指定元件的資料點選。  
  
-   對於所要擷取的資料列數目，所指定的值無效。  
  
## <a name="requirements"></a>需求  
  
## <a name="see-also"></a>另請參閱  
 [catalog.add_data_tap](../../integration-services/system-stored-procedures/catalog-add-data-tap.md)  
  
  
