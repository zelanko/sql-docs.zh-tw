---
title: catalog.add_data_tap | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: a25ebcc7-535e-4619-adf6-4e2b5a62ba37
author: chugugrace
ms.author: chugu
ms.openlocfilehash: cb4ede46fbff3d647ef57214a779335b256819c4
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/22/2020
ms.locfileid: "86915045"
---
# <a name="catalogadd_data_tap"></a>catalog.add_data_tap 

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  針對執行的執行個體，在封裝資料流程中的元件輸出上，加入資料點選。  
  
## <a name="syntax"></a>語法  
  
```sql  
catalog.add_data_tap [ @execution_id = ] execution_id  
, [ @task_package_path = ] task_package_path  
, [ @dataflow_path_id_string = ] dataflow_path_id_string  
, [ @data_filename = ] data_filename  
, [ @max_rows = ] max_rows  
, [ @data_tap_id = ] data_tap_id OUTPUT  
```  
  
## <a name="arguments"></a>引數  
 [ @execution_id = ] *execution_id*  
 含有封裝之執行的執行識別碼。 *execution_id* 是 **bigint**。  
  
 [ @task_package_path = ] *task_package_path*  
 資料流程工作的封裝路徑。 資料流程工作的 **PackagePath** 屬性會指定路徑。 路徑會區分大小寫。 若要尋找套件路徑，請在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 中以滑鼠右鍵按一下 [資料流程] 工作，然後按一下 [屬性]。 **PackagePath** 屬性會出現在 [屬性] 視窗中。  
  
 *task_package_path* 是 **nvarchar(max)** 。  
  
 [ @dataflow_path_id_string = ] *dataflow_path_id_string*  
 資料流程路徑的識別字串。 路徑會連接兩個資料流程元件。 路徑的 **IdentificationString** 屬性會指定字串。  
  
 若要尋找識別字串，在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 中以滑鼠右鍵按一下兩個資料流程元件之間的路徑，然後按一下 [屬性]。 **IdentificationString** 屬性會出現在 [屬性] 視窗中。  
  
 *dataflow_path_id_string* 是 **nvarchar(4000)** 。  
  
 [ @data_filename = ] *data_filename*  
 儲存點選資料的檔案名稱。 如果資料流程工作是在 Foreach 迴圈或 For 迴圈容器中執行，個別檔案會針對迴圈的每次反覆運算，來儲存點選資料。 每個檔案都會以對應於反覆運算的號碼為字首。  
  
 根據預設，檔案會儲存至 \<*drive*>:\Program Files\Microsoft SQL Server\130\DTS\DataDumps 資料夾。  
  
 *data_filename* 是 **nvarchar(4000)** 。  
  
 [ @max_rows = ] *max_rows*  
 在資料點選期間擷取的資料列數目。 如果沒有指定此值，則會擷取所有資料列。 *max_rows* 是 **int**。  
  
 [ @data_tap_id = ] *data_tap_id*  
 傳回資料點選的識別碼。 *data_tap_id* 是 **bigint**。  
  
## <a name="example"></a>範例  
 下列範例會在資料流程工作 `'Paths[OLE DB Source.OLE DB Source Output]` 中的資料流程路徑 `\Package\Data Flow Task` 上建立資料點選。 點選的資料會儲存在 DataDumps 資料夾 (\<*drive*>:\Program Files\Microsoft SQL Server\130\DTS\DataDumps) 的 `output0.txt` 檔案中。  
  
```sql
Declare @execution_id bigint  
Exec SSISDB.Catalog.create_execution @folder_name='Packages',@project_name='SSISPackages', @package_name='Package.dtsx',@reference_id=Null, @use32bitruntime=False, @execution_id=@execution_id OUTPUT  
  
Exec SSISDB.Catalog.set_execution_parameter_value @execution_id,50, 'LOGGING_LEVEL', 0  
  
Exec SSISDB.Catalog.add_data_tap @execution_id, @task_package_path='\Package\Data Flow Task', @dataflow_path_id_string = 'Paths[OLE DB Source.OLE DB Source Output]', @data_filename = 'output0.txt'  
  
Exec SSISDB.Catalog.start_execution @execution_id  
```  
  
## <a name="remarks"></a>備註  
 若要新增資料點選，執行的執行個體必須處於已建立狀態 ([catalog.operations &#40;SSISDB 資料庫&#41;](../../integration-services/system-views/catalog-operations-ssisdb-database.md) 檢視之**狀態**資料行中的值為 1)。 狀態值會在您進行執行時變更。 您可以呼叫 [catalog.create_execution &#40;SSISDB 資料庫&#41;](../../integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database.md) 來建立執行。  
  
 以下是 add_data_tap 預存程序的考量事項。  
  
-   如果執行包含一個父封裝和一個或多個子封裝，您需要針對要點選資料的每個封裝，各加入一個資料點選。  
  
-   如果封裝包含多個具有相同名稱的資料流程工作，則 task_package_path 會明確識別含有所點選之元件輸出的資料流程工作。  
  
-   當您加入資料點選時，在執行封裝之前不會進行驗證。  
  
-   建議您限制在資料點選期間擷取的資料列數目，以避免產生大型資料檔案。 如果執行預存程序的電腦將資料檔案的儲存空間用盡，封裝就會停止執行，並且會在記錄檔中寫入錯誤訊息。  
  
-   執行 add_data_tap 預存程序會影響封裝的效能。 建議您只在進行資料問題的疑難排解時，才執行預存程序。  
  
-   若要存取儲存點選資料的檔案，您必須是執行預存程序之電腦的管理員。 您也必須是啟動執行的使用者 (執行中包含具有資料點選的封裝)。  
  
## <a name="return-codes"></a>傳回碼  
 0 (成功)  
  
 當預存程序失敗時，會擲回錯誤。  
  
## <a name="result-set"></a>結果集  
 None  
  
## <a name="permissions"></a>權限  
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
  
## <a name="external-resources"></a>外部資源  
 rafael-salas.com 上的部落格文章：[SSIS 2012:資料點選一覽](https://go.microsoft.com/fwlink/?LinkId=239983)。  
  
## <a name="see-also"></a>另請參閱  
 [catalog.add_data_tap_by_guid](../../integration-services/system-stored-procedures/catalog-add-data-tap-by-guid.md)  
  
  
