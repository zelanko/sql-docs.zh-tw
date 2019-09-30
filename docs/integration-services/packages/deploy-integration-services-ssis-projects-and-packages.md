---
title: 部署 Integration Services (SSIS) 專案和套件 | Microsoft Docs
ms.custom: ''
ms.date: 06/04/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.bids.converttolegacydeployment.f1
- sql13.ssis.deploymentwizard.f1
- sql13.ssis.ssms.isenvprop.permissions.f1
- sql13.ssis.ssms.isenvprop.general.f1
- sql13.ssis.ssms.iscreateenv.f1
- sql13.ssis.ssms.isenvprop.variables.f1
- sql13.ssis.migrationwizard.f1
ms.assetid: bea8ce8d-cf63-4257-840a-fc9adceade8c
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f35fb523d95b47b64e10feab8d4caa2370b79b5f
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/26/2019
ms.locfileid: "71282637"
---
# <a name="deploy-integration-services-ssis-projects-and-packages"></a>部署 Integration Services (SSIS) 專案和封裝

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 支援兩種部署模型：專案部署模型和舊版封裝部署模型。 專案部署模型可讓您將專案部署至 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器。  
  
如需舊版封裝部署模型的詳細資訊，請參閱[舊版封裝部署 &#40;SSIS&#41;](../../integration-services/packages/legacy-package-deployment-ssis.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssISversion11](../../includes/ssisversion11-md.md)]引進專案部署模型。 在此部署模型中，您無法在未部署整個專案的情況下部署一或多個套件。 [!INCLUDE[ssISversion13](../../includes/ssisversion13-md.md)] 引進累加套件部署功能，可讓您部署一或多個套件，而不需部署整個專案。  

> [!NOTE]
> 本文描述如何在一般情況下部署 SSIS 套件，以及如何在內部部署部署套件。 您也可以將 SSIS 套件部署到下列平台：
> - **Microsoft Azure 雲端**。 如需詳細資訊，請參閱[將 SQL Server Integration Services 工作負載隨即轉移至雲端](../lift-shift/ssis-azure-lift-shift-ssis-packages-overview.md)。
> - **Linux**。 如需詳細資訊，請參閱[使用 SSIS 在 Linux 上擷取、轉換和載入資料](../../linux/sql-server-linux-migrate-ssis.md)。

## <a name="compare-project-deployment-model-and-legacy-package-deployment-model"></a>專案部署模型與舊版封裝部署模型的比較  
 您為專案選擇的部署模型類型，會決定可用於該專案的開發及管理選項。 下表顯示使用專案部署模型與使用封裝部署模型之間的差異和相似性。  
  
|使用專案部署模型時|使用舊版封裝部署模型時|  
|---------------------------------------------|----------------------------------------------------|  
|專案是部署的單位。|封裝是部署的單位。|  
|參數可用來將值指派給封裝屬性。|組態可用來將值指派給封裝屬性。|  
|專案 (包含封裝和參數) 會建立至專案部署檔 (副檔名 .ispac)。|封裝 (副檔名 .dtsx) 和組態 (副檔名 .dtsconfig) 會個別儲存到檔案系統。|  
|專案 (包含封裝和參數) 部署到 SQL Server 執行個體上的 SSISDB 目錄。|封裝和組態會複製到另一台電腦上的檔案系統。 封裝也可以儲存至 SQL Server 執行個體上的 MSDB 資料庫。|  
|資料庫引擎上需要 CLR 整合。|資料庫引擎上不需要 CLR 整合。|  
|環境特定變數參數值會儲存在環境變數中。|環境特定組態值會儲存在組態檔中。|  
|在執行之前，可以先在伺服器上驗證目錄中的專案和封裝。 您可以使用 SQL Server Management Studio、預存程序或 Managed 程式碼來執行驗證。|臨執行前才驗證封裝。 您也可以用 dtExec 或 Managed 程式碼來驗證封裝。|  
|在資料庫引擎上啟動執行，藉以執行封裝。 在執行啟動之前，將專案識別碼、明確的參數值 (選擇性) 和環境參考 (選擇性) 指派給執行。<br /><br /> 您也可以使用 **dtExec**執行封裝。|以 **dtExec** 與 **DTExecUI** 執行公用程式來執行封裝。 以命令提示字元引數 (選擇性) 來識別適用的組態。|  
|在執行期間，會自動擷取封裝所產生的事件，並儲存至目錄。 您可以用 Transact-SQL 檢視來查詢這些事件。|在執行期間，不會自動擷取封裝所產生的事件。 必須將記錄提供者加入封裝，才能擷取事件。|  
|封裝是在單獨的 Windows 處理序中執行。|封裝是在單獨的 Windows 處理序中執行。|  
|使用 SQL Server Agent 來排定封裝執行的時程。|使用 SQL Server Agent 來排定封裝執行的時程。|  
  
 [!INCLUDE[ssISversion11](../../includes/ssisversion11-md.md)]引進專案部署模型。 如果您使用此模型，您就無法在未部署整個專案的情況下部署一或多個封裝。 [!INCLUDE[ssISversion13](../../includes/ssisversion13-md.md)] 引進累加封裝部署功能，可讓您部署一個或多個封裝，而不需部署整個專案。   
  
## <a name="features-of-project-deployment-model"></a>專案部署模型的功能  
 下表列出可用於專為專案部署模型開發之專案的功能。  
  
|功能|Description|  
|-------------|-----------------|  
|參數|參數指定要供封裝使用的資料。 您可以將參數範圍限定在分別具有封裝參數和專案參數的封裝層級或專案層級。 在運算式或工作中，都會用到參數。 將專案部署到目錄之後，您可以為每個參數各指定一個常值，或是使用在設計時所指派的預設值。 您也可以參考環境變數來替代常值。 環境變數會在封裝執行時解析。|  
|環境|環境是可供 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案參考之變數的容器。 每個專案都可以有多個環境參考，但是封裝執行的單一執行個體只能參考來自單一環境的變數。 環境可讓您組織指派給封裝的值。 例如，您可能會有命名為 "Dev"、"test" 和 "Production" 的環境。|  
|環境變數|環境變數定義在封裝執行期間，可指派給參數的常值。 若要使用環境變數，請建立環境參考 (在對應至具有參數之環境的專案中)、指派參數值給環境變數的名稱，並且在設定執行的執行個體時，指定相對應的環境參考。|  
|SSISDB 目錄|所有 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 物件都會在名為 SSISDB 目錄之資料庫中的 SQL Server 執行個體上儲存及管理。 該目錄可讓您使用資料夾專案和環境。 SQL Server 的每個執行個體都可以有一個目錄。 每個目錄中可以有零個或多個資料夾。 每個資料夾可以有零個以上的專案和零個以上的環境。 目錄中的資料夾也可以用作對 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 物件的權限界限。|  
|目錄預存程序和檢視|有大量的預存程序和檢視可用來管理目錄中的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 物件。 例如，您可以指定參數和環境變數的值、建立和啟動執行，以及監視目錄作業。 您甚至可以在執行啟動之前，查看封裝將要使用哪些確切的值。|  
  
## <a name="project-deployment"></a>專案部署  
 專案部署模型的中心是專案部署檔案 (副檔名 .ispac)。 專案部署檔案是獨立的 (self-contained) 部署單位，其中只包含專案中封裝和參數的相關基本資訊。 專案部署檔案不會擷取 Integration Services 專案檔 (副檔名 .dtproj) 中包含的所有資訊。 例如，您用來撰寫附註的其他文字檔不是儲存在專案部署檔案中，因此不會部署至目錄。  

## <a name="permissions-required-to-deploy-ssis-projects-and-packages"></a>部署 SSIS 專案和參數所需的權限

如果您變更預設 SSIS 服務帳戶，則可能需要先將其他權限授與非預設服務帳戶，才能成功部署套件。 如果非預設服務帳戶沒有必要權限，您可能會看到下列錯誤訊息。

*執行使用者自訂常式或彙總 "deploy_project_internal" 時，發生 .NET Framework 錯誤：System.ComponentModel.Win32Exception:用戶端沒有必要的權限。*

此錯誤通常是缺少 DCOM 權限的結果。 若要修正錯誤，請執行下列動作。

1.  開啟 [元件服務]  主控台 (或執行 Dcomcnfg.exe)。
2.  在 [元件服務]  主控台中，展開 [元件服務]   > [電腦]   > [我的電腦]   > [DCOM 設定]  。
3.  在清單中，找到 [Microsoft SQL Server Integration Services xx.0]  以表示您正在使用的 SQL Server 版本。 例如，SQL Server 2016 是第 13 版。
4.  按一下滑鼠右鍵，然後選取 [屬性]  。
5.  在 [Microsoft SQL Server Integration Services 13.0 內容]  對話方塊中，選取 [安全性]  索引標籤。
6.  針對啟動和啟用、存取以及設定這三組權限，選取 [自訂]  ，然後選取 [編輯]  開啟 [權限]  對話方塊。
7.  在 [權限]  對話方塊中，新增非預設服務帳戶，並視需要授與 [允許]  權限。 帳戶通常會有 [本機啟動]  和 [本機啟用]  權限。
8.  按兩次 [確定]  ，然後關閉 [元件服務]  主控台。

如需本節中所述錯誤的詳細資訊，以及 SSIS 服務帳戶所需權限的詳細資訊，請參閱下列部落格文章。  
[System.ComponentModel.Win32Exception:部署 SSIS 專案時，用戶端沒有這項特殊權限](https://blogs.msdn.microsoft.com/dataaccesstechnologies/2013/08/20/system-componentmodel-win32exception-a-required-privilege-is-not-held-by-the-client-while-deploying-ssis-project/)

## <a name="deploy-projects-to-integration-services-server"></a>將專案部署至 Integration Services 伺服器
  在目前版本的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]中，您可以將專案部署到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器可讓您管理封裝、執行封裝，以及利用環境設定封裝的執行值。  
  
> [!NOTE]  
>  與舊版 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]相同，在目前版本中，您也可以將封裝部署至 SQL Server 的執行個體，以及使用 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務來執行和管理封裝。 您會使用封裝部署模型。 如需詳細資訊，請參閱[舊版封裝部署 &#40;SSIS&#41;](../../integration-services/packages/legacy-package-deployment-ssis.md)。  
  
 如果要將專案部署至 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器，請完成下列工作：  
  
1.  建立 SSISDB 目錄 (如果尚未建立)。 如需詳細資訊，請參閱 [SSIS 目錄](../../integration-services/catalog/ssis-catalog.md)。  
  
2.  請執行 [Integration Services 專案轉換精靈]  將專案轉換為專案部署模型。 如需詳細資訊，請參閱以下指示：[將專案轉換為專案部署模型](#convert)  
  
    -   如果您在 [!INCLUDE[ssISversion12](../../includes/ssisversion12-md.md)] 或更新版本中建立專案，則專案會根據預設使用專案部署模型。  
  
    -   若是在舊版 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]中建立專案，在您於 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]中開啟專案檔案後，請將專案轉換為專案部署模型。  
  
        > [!NOTE]  
        >  如果專案包含一個或多個資料來源，則在完成專案轉換時，會移除資料來源。 若要建立專案中的封裝可以共用的資料來源連接，請在專案層級加入連接管理員。 如需詳細資訊，請參閱 [加入、刪除或共用封裝中的連線管理員](https://msdn.microsoft.com/library/6f2ba4ea-10be-4c40-9e80-7efcf6ee9655)。  
  
         根據您是從 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 還是從 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 執行 [Integration Services 專案轉換精靈]  ，此精靈會執行不同的轉換工作。  
  
        -   如果您是從 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 執行此精靈，則專案中包含的封裝會從 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 2005、2008 或 2008 R2 轉換為目前版本的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 使用的格式。 系統將會升級原始專案 (.dtproj) 和封裝 (.dtsx) 檔。  
  
        -   如果您是從 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]執行此精靈，此精靈將會從專案中包含的封裝和組態產生專案部署檔案 (.ispac)。 系統將不會升級原始封裝 (.dtsx) 檔。  
  
             您可以在精靈的 [選取目的地]  頁面中選取現有的檔案，或建立一個新檔案。  
  
             若要在轉換專案時升級封裝檔，請從 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 執行 [Integration Services 專案轉換精靈]  。 若要從專案轉換個別升級封裝檔案，請從 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 執行 [Integration Services 專案轉換精靈]  ，然後執行 [SSIS 封裝升級精靈]  。 若您個別升級封裝檔，請確認是否儲存變更。 否則，當您將專案轉換成專案部署模型時，所有未儲存的封裝變更將不予轉換。  
  
     如需封裝升級的詳細資訊，請參閱 [升級 Integration Services 封裝](../../integration-services/install-windows/upgrade-integration-services-packages.md) 和 [使用 SSIS 封裝升級精靈來升級 Integration Services 封裝](../../integration-services/install-windows/upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard.md)。  
  
3.  將專案部署至 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器。 如需詳細資訊，請參閱以下指示：[將專案部署至 Integration Services 伺服器](#deploy)。  
  
4.  (選擇性) 建立部署專案的環境。 
  
###  <a name="convert"></a> 將專案轉換為專案部署模型  
  
1.  開啟 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 中的專案，然後在方案總管中，以滑鼠右鍵按一下該專案，並按一下 [轉換為專案部署模型]  。  
  
     -或-  
  
     從 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 的 [物件總管] 中，以滑鼠右鍵按一下 [專案]  節點，然後選取 [匯入封裝]  。  
  
2.  完成精靈。
  
###  <a name="deploy"></a> 將專案部署至 Integration Services 伺服器  
  
1.  開啟 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 中的專案，然後從 [專案]  功能表中選取 [部署]  ，以啟動 [Integration Services 部署精靈]  。  
  
     -或-  
  
     在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，展開 [物件總管] 內的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] > SSISDB  節點，然後找出您要部署之專案的 [專案] 資料夾。 以滑鼠右鍵按一下 [專案]  資料夾，然後按一下 [部署專案]  。  
  
     -或-  
  
     在命令提示字元中，從 **%ProgramFiles%\Microsoft SQL Server\130\DTS\Binn** 執行 **isdeploymentwizard.exe**。 64 位元的電腦上的 **%ProgramFiles(x86)%\Microsoft SQL Server\130\DTS\Binn**也有提供 32 位元版本的工具。  
  
2.  在 [選取來源]  頁面上，按一下 [專案部署檔案]  以選取專案的部署檔案。  
  
     -或-  
  
     按一下 [Integration Services 目錄]  ，選取已經部署至 SSISDB 目錄的專案。  
  
3.  完成精靈。 

## <a name="deploy-packages-to-integration-services-server"></a>將封裝部署至 Integration Services 伺服器
  [!INCLUDE[ssISversion13](../../includes/ssisversion13-md.md)] 引進累加封裝部署功能，可讓您將一或多個封裝部署到現有或新的專案中，而不需部署整個專案。  
  
###  <a name="DeployWizard"></a> 使用 Integration Services 部署精靈部署封裝  
  
1.  在命令提示字元中，從 **%ProgramFiles%\Microsoft SQL Server\130\DTS\Binn** 執行 **isdeploymentwizard.exe**。 64 位元的電腦上的 **%ProgramFiles(x86)%\Microsoft SQL Server\130\DTS\Binn** 也有提供 32 位元版本的工具。  
  
2.  在 [選取來源]  頁面上，切換至 [封裝部署模型]  。 然後，選取含有來源封裝的資料夾並設定封裝。  
  
3.  完成精靈。 遵循 [Package Deployment Model](#PackageModel)(封裝部署模型) 中所述的其餘步驟。  
  
###  <a name="SSMS"></a> 使用 SQL Server Management Studio 部署封裝  
  
1.  在 SQL Server Management Studio 中，依序展開物件總管中的 [Integration Services 目錄]   > [SISDB]  節點。  
  
2.  以滑鼠右鍵按一下 [專案]  資料夾，然後按一下 [部署專案]  。  
  
3.  如果您看到 [簡介]  頁面，按一下 [下一步]  以繼續。  
  
4.  在 [選取來源]  頁面上，切換至 [封裝部署模型]  。 然後，選取含有來源封裝的資料夾並設定封裝。  
  
5.  完成精靈。 遵循 [Package Deployment Model](#PackageModel)(封裝部署模型) 中所述的其餘步驟。  
  
###  <a name="SSDT"></a> 使用 SQL Server Data Tools 部署封裝 (Visual Studio)  
  
1.  在 Visual Studio 中，開啟 Integration Services 專案，並選取您想要部署的封裝。  
  
2.  按一下滑鼠右鍵並選取 [部署封裝]  。 隨即開啟 [部署精靈]，其中包含設定為來源封裝的所選封裝。  
  
3.  完成精靈。 遵循 [Package Deployment Model](#PackageModel)(封裝部署模型) 中所述的其餘步驟。  
  
###  <a name="StoredProcedure"></a> 使用 deploy_packages 預存程序部署封裝  
 您可以使用 **[catalog].[deploy_packages]** 預存程序，將一或多個 SSIS 封裝部署至 SSIS 目錄。 下列程式碼範例示範如何使用此預存程序，將封裝部署至 SSIS 伺服器。 如需詳細資訊，請參閱 [catalog.deploy_packages](../../integration-services/system-stored-procedures/catalog-deploy-packages.md)。  
  
```cs
  
private static void Main(string[] args)  
{  
    // Connection string to SSISDB  
    var connectionString = "Data Source=.;Initial Catalog=SSISDB;Integrated Security=True;MultipleActiveResultSets=false";  
  
    using (var sqlConnection = new SqlConnection(connectionString))  
    {  
        sqlConnection.Open();  
  
        var sqlCommand = new SqlCommand  
        {  
            Connection = sqlConnection,  
            CommandType = CommandType.StoredProcedure,  
            CommandText = "[catalog].[deploy_packages]"  
        };  
  
        var packageData = Encoding.UTF8.GetBytes(File.ReadAllText(@"C:\Test\Package.dtsx"));  
  
        // DataTable: name is the package name without extension and package_data is byte array of package.  
        var packageTable = new DataTable();  
        packageTable.Columns.Add("name", typeof(string));  
        packageTable.Columns.Add("package_data", typeof(byte[]));  
        packageTable.Rows.Add("Package", packageData);  
  
        // Set the destination project and folder which is named Folder and Project.  
        sqlCommand.Parameters.Add(new SqlParameter("@folder_name", SqlDbType.NVarChar, ParameterDirection.Input, "Folder", -1));  
        sqlCommand.Parameters.Add(new SqlParameter("@project_name", SqlDbType.NVarChar, ParameterDirection.Input, "Project", -1));  
        sqlCommand.Parameters.Add(new SqlParameter("@packages_table", SqlDbType.Structured, ParameterDirection.Input, packageTable, -1));  
  
        var result = sqlCommand.Parameters.Add("RetVal", SqlDbType.Int);  
        result.Direction = ParameterDirection.ReturnValue;  
  
        sqlCommand.ExecuteNonQuery();  
    }  
}  
  
```  
  
###  <a name="MOMApi"></a> 使用管理物件模型 API 部署封裝  
 下列程式碼範例示範如何使用管理物件模型 API，將封裝部署到伺服器。  
  
```cs 
  
static void Main()  
 {  
     // Before deploying packages, make sure the destination project exists in SSISDB.  
     var connectionString = "Data Source=.;Integrated Security=True;MultipleActiveResultSets=false";  
     var catalogName = "SSISDB";  
     var folderName = "Folder";  
     var projectName = "Project";  
  
     // Get the folder instance.  
     var sqlConnection = new SqlConnection(connectionString);  
     var store = new Microsoft.SqlServer.Management.IntegrationServices.IntegrationServices(sqlConnection);  
     var folder = store.Catalogs[catalogName].Folders[folderName];  
  
     // Key is package name without extension and value is package binaries.  
     var packageDict = new Dictionary<string, string>();  
  
     var packageData = File.ReadAllText(@"C:\Folder\Package.dtsx");  
     packageDict.Add("Package", packageData);  
  
     // Deploy package to the destination project.  
     folder.DeployPackages(projectName, packageDict);  
 }  
  
```

## <a name="convert-to-package-deployment-model-dialog-box"></a>轉換成封裝部署模型對話方塊
  **[轉換成封裝部署模型]** 命令可讓您在檢查專案和專案中的每個封裝是否與該模型相容之後，將封裝轉換成封裝部署模型。 如果某個封裝使用專案部署模型獨有的功能 (例如參數)，則無法轉換該封裝。  
  
### <a name="task-list"></a>工作清單  
 將封裝轉換成封裝部署模型需要兩個步驟。  
  
1.  當您從 **[專案]** 功能表選取 **[轉換成封裝部署模型]** 命令時，會檢查專案和每個封裝是否與此模型相容。 結果會顯示在 **[結果]** 資料表中。  
  
     如果專案或封裝無法通過相容性測試，按一下 **[結果]** 資料行中的 **[失敗]** ，可取得詳細資訊。 按一下 **[儲存報表]** ，將此資訊的副本儲存到文字檔中。  
  
2.  如果專案和所有封裝通過相容性測試，則按一下 **[確定]** 以轉換封裝。  
  
> **注意：** 若要將專案轉換為專案部署模型，請使用 **[Integration Services 專案轉換精靈]** 。 如需相關資訊，請參閱 [Integration Services Project Conversion Wizard](deploy-integration-services-ssis-projects-and-packages.md)。  

## <a name="integration-services-deployment-wizard"></a>Integration Services 部署精靈
  [Integration Services 部署精靈]  支援兩種部署模型：
   - 專案部署模型
   - 套件部署模型 
   
 **專案部署模型** 可讓您將 SQL Server Integration Services (SSIS) 專案，以單一單位形式部署至 SSIS 目錄。
 
 **套件部署模型** 可讓您將已更新的套件部署至 SSIS 目錄，而無須部署整個專案。 
 
 > **注意：** 此精靈的預設部署為專案部署模型。  
  
### <a name="launch-the-wizard"></a>啟動精靈
透過下列其中一個方式來啟動精靈：

 - 在 Windows Search 中輸入「SQL Server 部署精靈」  

**OR**

 - 在 SQL Server 安裝資料夾下搜尋可執行檔 **ISDeploymentWizard.exe**，例如："C:\Program Files (x86)\Microsoft SQL Server\130\DTS\Binn"。 
 
 > **注意：** 若顯示 [簡介]  頁面，請按一下 [下一步]  切換至 [選取來源]  頁面。 
 
 此頁面上的設定視每種部署模型而異。 根據您在此頁面中選取的模型，遵循 [Project Deployment Model](#ProjectModel) 區段或 [Package Deployment Model](#PackageModel) 區段中的步驟執行。  
  
###  <a name="ProjectModel"></a> Project Deployment Model  
  
#### <a name="select-source"></a>選取來源  
 若要部署您建立的專案部署檔案，請選取 [專案部署檔案]  ，並輸入 .ispac 檔案的路徑。 若要部署位於 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中的專案，請選取 **[Integration Services 目錄]** ，然後輸入伺服器名稱以及該專案在目錄中的路徑。 按一下 [下一步]  ，以查看 [選取目的地]  頁面。  
  
#### <a name="select-destination"></a>選取目的地  
 若要選取專案在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中的目的地資料夾，請輸入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，或按一下 **[瀏覽]** ，從伺服器清單中選取。 在 SSISDB 中輸入專案路徑，或按一下 **[瀏覽]** 來選取路徑。 按一下 [下一步]  ，以切換至 [檢閱]  頁面。  
  
#### <a name="review-and-deploy"></a>檢閱 (和部署)  
 此頁面可讓您檢閱所選取的設定。 您可以按一下 **[上一步]** ，或按一下左窗格中的任何步驟來變更您的選取項目。 按一下 [部署]  開始部署程序。  
  
#### <a name="results"></a>結果  
 完成部署程序之後，您應該會看到 [結果]  頁面。 此頁面會顯示每個動作執行成功或失敗。 如果動作失敗，按一下 **[結果]** 資料行中的 **[失敗]** 以顯示錯誤的說明。 按一下 [儲存報表]  將結果儲存至 XML 檔案，或按一下 [關閉]  結束精靈。
  
###  <a name="PackageModel"></a> Package Deployment Model  
  
#### <a name="select-source"></a>選取來源  
 若您選取 [封裝部署]  選項做為 **部署模型** ，則 **Integration Services 部署精靈** 中的 [選取來源]  頁面會顯示封裝部署模型的特定設定。  
  
 若要選取來源封裝，請按一下 [瀏覽...]  按鈕以選取包含封裝的**資料夾**，或是在 [封裝資料夾路徑]  文字方塊中輸入資料夾路徑，然後在頁面底端按一下 [重新整理]  按鈕。 現在，您應會於清單方塊中的指定資料夾看見所有封裝。 根據預設，系統會選取所有封裝。 按一下第一個資料行的 **核取方塊** ，選擇您想要部署至伺服器的封裝。  
  
 參閱 [狀態]  和 [訊息]  資料行，以確認封裝的狀態。 若狀態設為 [準備就緒]  或 [警告]  ，則部署精靈不會封鎖部署處理程序。 然而，若狀態設為 [錯誤]  ，則精靈將不會繼續部署所選的封裝。 若要檢視詳細的警告/錯誤訊息，請按一下 [訊息]  資料行中的連結。  
  
 若使用密碼將敏感性資料或封裝資料加密處理，請在 [密碼]  資料行中輸入密碼，然後按一下 [重新整理]  按鈕確認密碼已獲接受。 若密碼正確，則狀態會變更為 [準備就緒]  ，且警告訊息會消失。 若有多個具相同密碼的封裝，請選取具相同加密密碼的封裝，在 [密碼]  文字方塊中輸入密碼，然後按一下 [套用]  按鈕。 密碼會套用至選取的封裝。  
  
 若所有選取的封裝狀態皆未設定為 [錯誤]  ，則會啟用 [下一步]  按鈕讓您得以繼續執行封裝部署處理程序。  
  
#### <a name="select-destination"></a>選取目的地  
 選取封裝來源後，按一下 [下一步]  按鈕切換至 [選取目的地]  頁面。 封裝必須部署至 SSIS 目錄 (SSISDB) 中的專案。 因此在部署封裝前，請確定目的地專案已存在於 SSIS 目錄。 否則會建立空白專案。在 [選取目的地]  頁面的 [伺服器名稱]  文字方塊中輸入伺服器名稱，或是按一下 [瀏覽...]  按鈕以選取伺服器執行個體。 然後按一下 [路徑]  文字方塊旁的 [瀏覽...]  按鈕，以指定目的地專案。 若專案不存在，請按一下 [新增專案...]  以建立空白專案做為目的地專案。 專案 **必須** 建立在資料夾下方。  
  
#### <a name="review-and-deploy"></a>檢閱和部署  
 在 [選取目的地]  頁面上，按一下 [下一步]  切換至 **Integration Services 部署精靈** 中的 [檢閱]  頁面。 在檢閱頁面上，檢閱有關部署動作的摘要報告。 驗證完成後，按一下 [部署]  按鈕以執行部署動作。  
  
#### <a name="results"></a>結果  
 部署完成後，您應該會看見 [結果]  頁面。 在 [結果]  頁面中，檢閱部署處理程序中每個步驟的結果。 在 [結果]  頁面上，按一下 [儲存報表]  以儲存部署報表，或是按一下 [關閉]  以關閉精靈。  

## <a name="create-and-map-a-server-environment"></a>建立和對應伺服器環境
  您可以建立伺服器環境，針對已部署至 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器之專案中所包含的封裝，指定執行值。 接著您可以針對特定封裝、進入點封裝，或給定專案中的所有封裝，將環境變數對應至參數。 進入點封裝通常是執行子封裝的父封裝。  
  
> [!IMPORTANT]  
>  對於某個特定執行，封裝只能藉由單一伺服器環境中包含的值執行。  
  
 您可以透過查詢檢視表，取得伺服器環境、環境參考和環境變數的清單。 您也可以呼叫預存程序來新增、刪除及修改環境、環境參考和環境變數。 如需詳細資訊，請參閱 [SSIS 目錄](../../integration-services/catalog/ssis-catalog.md)中的＜伺服器環境、伺服器變數和伺服器環境參考＞  一節。  
  
### <a name="to-create-and-use-a-server-environment"></a>若要建立和使用伺服器環境  
  
1.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 的物件總管中，展開 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄> **SSISDB** 節點，然後針對您要建立其環境的專案，尋找 [環境]  資料夾。  
  
2.  在以滑鼠右鍵按一下 [環境]  資料夾，然後按一下 [建立環境]  。  
  
3.  輸入環境的名稱，並選擇性地輸入描述，然後按一下 [確定]  。  
  
4.  以滑鼠右鍵按一下新環境，然後按一下 [屬性]  。  
  
5.  在 [變數]  頁面上執行下列動作，以加入變數。  
  
    1.  選取變數的 [類型]  。 變數的名稱**無須**與對應至該變數之專案參數的名稱相符。  
  
    2.  選擇性地輸入變數的 [描述]  。  
  
    3.  輸入環境變數的 [值]  。  
  
         如需環境變數名稱規則的資訊，請參閱 [SSIS 目錄](../../integration-services/catalog/ssis-catalog.md)中的＜環境變數＞  一節。  
  
    4.  選取或清除 [區分]  核取方塊，以指出此變數是否包含機密值。  
  
         如果您選取 [區分]  ，變數值就不會顯示在 [值]  欄位內。  
  
         機密值將在 SSISDB 目錄中進行加密。 如需加密的詳細資訊，請參閱 [SSIS 目錄](../../integration-services/catalog/ssis-catalog.md)。  
  
6.  在 [權限]  頁面上執行下列動作，對選取的使用者和角色授與或拒絕任何權限。  
  
    1.  按一下 [瀏覽]  ，然後從 [瀏覽所有主體]  對話方塊中選取一個或多個使用者和角色。  
  
    2.  在 [登入或角色]  區域內，選取您想要授與或拒絕其權限的使用者或角色。  
  
    3.  在 [明確]  區域內，按一下每項權限旁的 [授與]  或 [拒絕]  。  
  
7.  若要編寫環境的指令碼，請按一下 [指令碼]  。 預設情況下，指令碼會顯示在新的 [查詢編輯器] 視窗中。  
  
    > [!TIP]  
    >  只要環境屬性有所增減或變更 (例如加入變數)，您就必須按一下 [指令碼]  ，然後才按一下 [環境屬性]  對話方塊中的 [確定]  。 否則將不會產生指令碼。  
  
8.  按一下 [確定]  ，將變更儲存至環境屬性。  
  
9. 在物件總管中的 [SSISDB]  節點下，展開 [專案]  資料夾，以滑鼠右鍵按一下專案，然後按一下 [設定]  。  
  
10. 在 [參考]  頁面上，按一下 [加入]  加入環境，然後按一下 [確定]  將參考儲存至環境。  
  
11. 再次以滑鼠右鍵按一下專案，然後按一下 [設定]  。  
  
12. 若要將環境變數對應至您在設計階段加入封裝中的參數，或對應至您將 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案轉換為專案部署模型時所產生的參數，請執行下列操作。  
  
    1.  在 [參數]  頁面的 [參數]  索引標籤中，按一下 [值]  欄位旁的瀏覽按鈕。  
  
    2.  按一下 [使用環境變數]  ，然後選取您建立的環境變數。  
  
13. 若要將環境變數對應至連線管理員屬性，請執行下列操作。 SSIS 伺服器上會自動產生連接管理員屬性的參數。  
  
    1.  在 [參數]  頁面的 [連線管理員]  索引標籤中，按一下 [值]  欄位旁的瀏覽按鈕。  
  
    2.  按一下 [使用環境變數]  ，然後選取您建立的環境變數。  
  
14. 按兩次 [確定]  ，以儲存您的變更。  

## <a name="deploy-and-execute-ssis-packages-using-stored-procedures"></a>使用預存程序部署及執行 SSIS 封裝
  當您設定 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案來使用專案部署模型時，您可以使用 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 目錄中的預存程序來部署專案及執行封裝。 如需有關專案部署模型的詳細資訊，請參閱＜ [Deployment of Projects and Packages](https://msdn.microsoft.com/library/hh213290.aspx)＞。  
  
 您也可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 部署專案及執行封裝。 如需詳細資訊，請參閱＜ **另請參閱** ＞一節中的主題。  
  
> [!TIP]
>  您可以執行以下動作，輕鬆地針對底下程序中所列的預存程序產生 Transact-SQL 陳述式 (除了 catalog.deploy_project 以外)：  
> 
>  1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，展開 [物件總管] 中的 **Integration Services 目錄** 節點，並導覽到您要執行的封裝。  
> 2.  以滑鼠右鍵按一下封裝，然後按一下 [執行]  。  
> 3.  請視需要在 **[進階]** 索引標籤中設定參數值、連接管理員屬性和選項，例如記錄層次。  
> 
>      如需有關記錄層級的詳細資訊，請參閱＜ [在 SSIS 伺服器上啟用封裝執行的記錄功能](../../integration-services/performance/integration-services-ssis-logging.md#server_logging)＞。  
> 4.  在按一下 **[確定]** 執行封裝之前，請按一下 **[指令碼]** 。 Transact-SQL 會出現在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的 [查詢編輯器] 視窗中。  
  
### <a name="to-deploy-and-execute-a-package-using-stored-procedures"></a>若要使用預存程序部署及執行封裝  
  
1.  呼叫 [catalog.deploy_project &#40;SSISDB 資料庫&#41;](../../integration-services/system-stored-procedures/catalog-deploy-project-ssisdb-database.md) 將包含封裝的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案部署到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器。  
  
     若要擷取 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案部署檔案的二進位內容，請針對 *@project_stream* 參數使用 SELECT 陳述式搭配 OPENROWSET 函數和 BULK 資料列集提供者。 BULK 資料列集提供者可讓您從檔案讀取資料。 BULK 資料列集提供者的 SINGLE_BLOB 引數會傳回資料檔的內容當做類型為 varbinary(max) 的單一資料列、單一資料行資料列集。 如需詳細資訊，請參閱 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)。  
  
     在下列範例中，SSISPackages_ProjectDeployment 專案會部署到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器上的 [SSIS 封裝] 資料夾。 二進位資料會從專案檔 (SSISPackage_ProjectDeployment.ispac) 讀取，並且儲存在類型為 varbinary(max) 的 *@ProjectBinary* 參數中。 *@ProjectBinary* 參數值會指派給 *@project_stream* 參數。  
  
    ```sql
    DECLARE @ProjectBinary as varbinary(max)  
    DECLARE @operation_id as bigint  
    Set @ProjectBinary = (SELECT * FROM OPENROWSET(BULK 'C:\MyProjects\ SSISPackage_ProjectDeployment.ispac', SINGLE_BLOB) as BinaryData)  
  
    Exec catalog.deploy_project @folder_name = 'SSIS Packages', @project_name = 'DeployViaStoredProc_SSIS', @Project_Stream = @ProjectBinary, @operation_id = @operation_id out  
  
    ```  
  
2.  呼叫 [catalog.create_execution &#40;SSISDB 資料庫&#41;](../../integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database.md) 來建立封裝執行的執行個體，並選擇性地呼叫 [catalog.set_execution_parameter_value &#40;SSISDB 資料庫&#41;](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md) 來設定執行階段參數值。  
  
     在下列範例中，catalog.create_execution 會針對 SSISPackage_ProjectDeployment 專案中包含的 package.dtsx 建立執行個體。 此專案位於 SSIS 封裝資料夾內。 此預存程序傳回的 execution_id 是用在 catalog.set_execution_parameter_value 的呼叫中。 此第二個預存程序會將 LOGGING_LEVEL 參數設定為 3 (詳細資訊記錄)，並將名為 Parameter1 的封裝參數設定為 1 的值。  
  
     對於參數 (例如 LOGGING_LEVEL)，object_type 的值為 50。 若為封裝參數，object_type 的值為 30。  
  
    ```sql
    Declare @execution_id bigint  
    EXEC [SSISDB].[catalog].[create_execution] @package_name=N'Package.dtsx', @execution_id=@execution_id OUTPUT, @folder_name=N'SSIS Packages', @project_name=N'SSISPackage_ProjectDeployment', @use32bitruntime=False, @reference_id=1  
  
    Select @execution_id  
    DECLARE @var0 smallint = 3  
    EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,  @object_type=50, @parameter_name=N'LOGGING_LEVEL', @parameter_value=@var0  
  
    DECLARE @var1 int = 1  
    EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,  @object_type=30, @parameter_name=N'Parameter1', @parameter_value=@var1  
  
    GO  
  
    ```  
  
3.  呼叫 [catalog.start_execution &#40;SSISDB 資料庫&#41;](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md) 來執行封裝。  
  
     在下列範例中，catalog.start_execution 的呼叫會加入至 Transact-SQL 來開始執行封裝。 使用 catalog.create_execution 預存程序所傳回的 execution_id。  
  
    ```sql
    Declare @execution_id bigint  
    EXEC [SSISDB].[catalog].[create_execution] @package_name=N'Package.dtsx', @execution_id=@execution_id OUTPUT, @folder_name=N'SSIS Packages', @project_name=N'SSISPackage_ProjectDeployment', @use32bitruntime=False, @reference_id=1  
  
    Select @execution_id  
    DECLARE @var0 smallint = 3  
    EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,  @object_type=50, @parameter_name=N'LOGGING_LEVEL', @parameter_value=@var0  
  
    DECLARE @var1 int = 1  
    EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,  @object_type=30, @parameter_name=N'Parameter1', @parameter_value=@var1  
  
    EXEC [SSISDB].[catalog].[start_execution] @execution_id  
    GO  
  
    ```  
  
### <a name="to-deploy-a-project-from-server-to-server-using-stored-procedures"></a>若要使用預存程序在不同伺服器之間部署專案  
 您可以使用 [catalog.get_project &#40;SSISDB 資料庫&#41;](../../integration-services/system-stored-procedures/catalog-get-project-ssisdb-database.md) 和 [catalog.deploy_project &#40;SSISDB 資料庫&#41;](../../integration-services/system-stored-procedures/catalog-deploy-project-ssisdb-database.md) 預存程序在不同伺服器之間部署專案。  
  
 在執行預存程序之前，您必須執行下列動作。  
  
-   建立連結的伺服器物件。 如需詳細資訊，請參閱[建立連結的伺服器 &#40;SQL Server Database Engine&#41;](../../relational-databases/linked-servers/create-linked-servers-sql-server-database-engine.md)。  
  
     在 **[連結的伺服器屬性]** 對話方塊的 **[伺服器選項]** 頁面上，將 **[RPC]** 和 **[RPC 輸出]** 設定為 **[True]** 。 此外，也將 **[啟用 RPC 的分散式交易促銷]** 設定為 **[False]** 。  
  
-   若要針對您為連結的伺服器選取的提供者啟用動態參數，請在物件總管中展開 [連結的伺服器]  下方的 [提供者]  節點，以滑鼠右鍵按一下此提供者，然後按一下 [屬性]  。 選取 **[動態參數]** 旁邊的 **[啟用]** 。  
  
-   確認兩部伺服器上都已啟動分散式交易協調器 (DTC)。  
  
 呼叫 catalog.get_project 來傳回專案的二進位內容，然後呼叫 catalog.deploy_project。 catalog.get_project 傳回的值會插入 varbinary(max) 類型的資料表變數中。 連結的伺服器無法傳回屬於 varbinary(max) 的結果。  
  
 在下列範例中，catalog.get_project 會針對連結的伺服器上的 SSISPackages 專案傳回二進位內容。 catalog.deploy_project 會將專案部署到本機伺服器的 DestFolder 資料夾。  
  
```sql
declare @resultsTableVar table (  
project_binary varbinary(max)  
)  
  
INSERT @resultsTableVar (project_binary)  
EXECUTE [MyLinkedServer].[SSISDB].[catalog].[get_project] 'Packages', 'SSISPackages'  
  
declare @project_binary varbinary(max)  
select @project_binary = project_binary from @resultsTableVar  
  
exec [SSISDB].[CATALOG].[deploy_project] 'DestFolder', 'SSISPackages', @project_binary  
  
```  

## <a name="integration-services-project-conversion-wizard"></a>Integration Services 專案轉換精靈
  [Integration Services 專案轉換精靈]  會將專案轉換為專案部署模型。  
  
> [!NOTE]  
>  如果專案包含一個或多個資料來源，則在完成專案轉換時，會移除資料來源。 若要在專案中建立可以透過封裝共用的資料來源連接，請在專案層級加入連接管理員。 如需詳細資訊，請參閱 [加入、刪除或共用封裝中的連線管理員](https://msdn.microsoft.com/library/6f2ba4ea-10be-4c40-9e80-7efcf6ee9655)。  
  
 **您想要做什麼事？**  
  
-   [開啟 [Integration Services 專案轉換精靈]](#open_dialog)  
  
-   [設定 [尋找封裝] 頁面上的選項](#locate)  
  
-   [設定 [選取封裝] 頁面上的選項](#selectPackages)  
  
-   [設定 [選取目的地] 頁面上的選項](#destination)  
  
-   [設定 [指定專案屬性] 頁面上的選項](#projectProperties)  
  
-   [設定 [更新執行封裝工作] 頁面上的選項](#executePackage)  
  
-   [設定 [選取組態] 頁面上的選項](#configurations)  
  
-   [設定 [建立參數] 頁面上的選項](#createParameters)  
  
-   [設定 [設定參數] 頁面上的選項](#configureParameters)  
  
-   [設定 [檢閱] 頁面上的選項](#review)  
  
-   [設定 [執行轉換] 上的選項](#conversion)  
  
###  <a name="open_dialog"></a> 開啟 [Integration Services 專案轉換精靈]  
 執行下列其中一項作業來開啟 [Integration Services 專案轉換精靈]  。  
  
-   開啟 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 中的專案，然後在方案總管中，以滑鼠右鍵按一下該專案，並按一下 [轉換為專案部署模型]  。  
  
-   從 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 的物件總管中，以滑鼠右鍵按一下 [專案]  節點，然後選取 [匯入封裝]  。  
  
 根據您是從 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 還是從 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 執行 [Integration Services 專案轉換精靈]  ，此精靈會執行不同的轉換工作。   
  
###  <a name="locate"></a> 設定 [尋找封裝] 頁面上的選項  
  
> [!NOTE]  
>  只有在您從 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 執行此精靈時，才可以使用 [尋找封裝]  頁面。  
  
 當您選取 [來源]  下拉式清單中的 [檔案系統]  時，下列選項會顯示在頁面上。 當封裝位於檔案系統時，請選取此選項。  
  
 **資料夾**  
 輸入封裝路徑，或按一下 [瀏覽]  巡覽到封裝。  
  
 當您選取 [來源]  下拉式清單中的 [SSIS 封裝存放區]  時，下列選項會顯示在頁面上。 如需封裝存放區的詳細資訊，請參閱[封裝管理 &#40;SSIS 服務&#41;](../../integration-services/service/package-management-ssis-service.md)。  
  
 **Server**  
 輸入伺服器名稱，選取伺服器。  
  
 **資料夾**  
 輸入封裝路徑，或按一下 [瀏覽]  巡覽到封裝。  
  
 當您選取 [來源]  下拉式清單中的 [Microsoft SQL Server]  時，下列選項會顯示在頁面上。 當封裝位於 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]時，請選取此選項。  
  
 **Server**  
 輸入伺服器名稱，選取伺服器。  
  
 **使用 Windows 驗證**  
 Microsoft Windows 驗證模式允許使用者透過 Windows 使用者帳戶連接。 如果您使用 Windows 驗證，就不需要提供使用者名稱或密碼。  
  
 **使用 SQL Server 驗證**  
 當使用者透過不信任連接並指定登入名稱和密碼進行連接時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會驗證此連接，檢查是否已建立該 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入帳戶，而且指定的密碼是否符合先前記錄的密碼。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 沒有登入帳戶集，驗證將失敗，而使用者會收到錯誤訊息。  
  
 **User name**  
 使用 SQL Server 驗證時，請指定使用者名稱。  
  
 **密碼**  
 使用 SQL Server 驗證時，請提供密碼。  
  
 **資料夾**  
 輸入封裝路徑，或按一下 [瀏覽]  巡覽到封裝。  
  
###  <a name="selectPackages"></a> 設定 [選取封裝] 頁面上的選項  
 **封裝名稱**  
 列出封裝檔案。  
  
 **狀態**  
 指出封裝是否就緒，可以轉換成專案部署模型。  
  
 **訊息**  
 顯示與封裝相關聯的訊息。  
  
 **密碼**  
 顯示與封裝相關聯的密碼。 密碼文字是隱藏的。  
  
 **套用至選取項目**  
 按一下可將 [密碼]  文字方塊中的密碼套用至選取的一個或多個封裝。  
  
 **[重新整理]**  
 重新整理封裝的清單。  
  
###  <a name="destination"></a> 設定 [選取目的地] 頁面上的選項  
 在此頁面上，指定新專案部署檔案 (.ispac) 的名稱和路徑，或選取現有的檔案。  
  
> [!NOTE]  
>  只有在您從 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 執行此精靈時，才可以使用 [選取目的地]  頁面。  
  
 **輸出路徑**  
 輸入部署檔案的路徑，或按一下 [瀏覽]  巡覽到檔案。  
  
 **專案名稱**  
 輸入專案名稱。  
  
 **保護等級**  
 選取保護等級。 如需詳細資訊，請參閱 [Access Control for Sensitive Data in Packages](../../integration-services/security/access-control-for-sensitive-data-in-packages.md)。  
  
 **專案描述**  
 選擇性地輸入專案的描述。  
  
###  <a name="projectProperties"></a> 設定 [指定專案屬性] 頁面上的選項  
  
> [!NOTE]  
>  只有在您從 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 執行此精靈時，才可以使用 [指定專案屬性]  頁面。  
  
 **專案名稱**  
 列出專案名稱。  
  
 **保護等級**  
 選取專案中包含之封裝的保護等級。 如需保護等級的詳細資訊，請參閱 [封裝中的敏感性資料存取控制](../../integration-services/security/access-control-for-sensitive-data-in-packages.md)。  
  
 **專案描述**  
 選擇性地輸入專案描述。  
  
###  <a name="executePackage"></a> 設定 [更新執行封裝工作] 頁面上的選項  
 更新執行封裝工作包含在封裝中，以使用專案參考。 如需詳細資訊，請參閱＜ [Execute Package Task Editor](../../integration-services/control-flow/execute-package-task-editor.md)＞。  
  
 **父封裝**  
 列出使用「執行封裝」工作執行子封裝之封裝的名稱。  
  
 **工作名稱**  
 列出「執行封裝」工作的名稱。  
  
 **原始參考**  
 列出子封裝的目前路徑。  
  
 **指派參考**  
 選取專案中儲存的子封裝。  
  
###  <a name="configurations"></a> 設定 [選取組態] 頁面上的選項  
 選取您要以參數取代的封裝組態。  
  
 **封裝**  
 列出封裝檔案。  
  
 **型別**  
 列出組態類型，例如 XML 組態檔。  
  
 **組態字串**  
 列出組態檔的路徑。  
  
 **狀態**  
 顯示組態的狀態訊息。 按一下訊息可檢視完整訊息文字。  
  
 **加入組態**  
 將其他專案中包含的封裝組態加入至您要以參數取代的可用組態清單中。 您可以選取儲存在檔案系統或 SQL Server 中的組態。  
  
 **[重新整理]**  
 按一下可重新整理組態的清單。  
  
 **轉換後從所有封裝移除組態**  
 建議您選取此選項以便從專案中移除所有組態。  
  
 如果您沒有選取此選項，則只會移除您選擇以參數取代的組態。  
  
###  <a name="createParameters"></a> 設定 [建立參數] 頁面上的選項  
 選取每個組態屬性的參數名稱和範圍。  
  
 **封裝**  
 列出封裝檔案。  
  
 **參數名稱**  
 列出參數名稱。  
  
 **範圍。**  
 選取參數的範圍 (封裝或專案)。  
  
###  <a name="configureParameters"></a> 設定 [設定參數] 頁面上的選項  
 **名稱**  
 列出參數名稱。  
  
 **範圍。**  
 列出參數的範圍。  
  
 **ReplTest1**  
 列出參數值。  
  
 按一下值欄位旁邊的省略符號按鈕來設定參數屬性。  
  
 在 [設定參數詳細資料]  對話方塊中，您可以編輯參數值。 您也可以指定在執行封裝時是否必須提供此參數值。  
  
 您可以按一下參數旁邊的瀏覽按鈕，在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 之 [設定]  對話方塊的 [參數]  頁面中修改值。 [設定參數值]  對話方塊隨即出現。  
  
 [設定參數詳細資料]  對話方塊也會列出參數值的資料類型，以及參數的來源。  
  
###  <a name="review"></a> 設定 [檢閱] 頁面上的選項  
 使用 [檢閱]  頁面確認您已經針對專案的轉換選取的選項。  
  
 **[上一步]**  
 按一下可變更選項。  
  
 **轉換**  
 按一下可將專案轉換為專案部署模型。  
  
###  <a name="conversion"></a> 設定 [執行轉換] 上的選項  
 [執行轉換] 頁面會顯示專案轉換的狀態。  
  
 **動作**  
 列出特定的轉換步驟。  
  
 **結果**  
 列出每個轉換步驟的狀態。 如需詳細資訊，請按一下狀態訊息。  
  
 在專案儲存到 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]中之前，不會儲存專案轉換。  
  
 **儲存報表**  
 按一下可將專案轉換的摘要儲存在 .xml 檔案中。  
