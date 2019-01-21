---
title: 如何：從 Team Foundation Build 執行 SQL Server 單元測試 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 24f5b85d-d6f9-415f-b09f-933b78dc0b67
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8faabc4655cd3aff4d6f15790a4f0e03dd60b8e8
ms.sourcegitcommit: 170c275ece5969ff0c8c413987c4f2062459db21
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/11/2019
ms.locfileid: "54226535"
---
# <a name="how-to-run-sql-server-unit-tests-from-team-foundation-build"></a>如何：從 Team Foundation Build 執行 SQL Server 單元測試
您可以使用 Team Foundation Build，在執行組建驗證測試 (BVT) 時執行 SQL Server 單元測試。 您可以設定單元測試以部署資料庫、產生測試資料，然後執行選取的測試。 如果您不熟悉 Team Foundation Build，就應該先檢閱下列資訊，然後再依照本主題的程序進行：  
  
-   [建立和定義 SQL Server 單元測試](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
  
-   [操作說明：在建置應用程式之後設定和執行已排定的測試](https://msdn.microsoft.com/library/ms182465(VS.100).aspx) \(機器翻譯\)  
  
-   [建立基本組建定義](https://msdn.microsoft.com/library/ms181716(VS.100).aspx)  
  
使用這些程序之前，您必須先執行下列工作來設定工作環境：  
  
-   安裝 Team Foundation Build 和 Team Foundation 版本控制。 您或許需要在不同的電腦上安裝 Team Foundation Build 和 Team Foundation 版本控制。  
  
-   將 MicrosoftSQL Server Data Tools Build Utilities 安裝在與 Team Foundation Build 相同的電腦上。 若要安裝 SQL Server Data Tools Build Utilities，請先執行系統管理安裝點。 如需有關系統管理安裝點的詳細資訊，請參閱[安裝 SQL Server Data Tools](../ssdt/install-sql-server-data-tools.md)。 然後從用於管理安裝點的位置 (/location)，將 SSDTBuildUtilties.msi 安裝到組建伺服器。  
  
-   連線到 Visual Studio Team Foundation Server 的執行個體。  
  
設定工作環境之後，您必須接著依照這些步驟進行：  
  
1.  建立資料庫專案。  
  
2.  匯入或建立資料庫專案的結構描述和物件。  
  
3.  設定組建和部署的資料庫專案屬性。  
  
4.  建立一個或多個單元測試。  
  
5.  將包含資料庫專案和單元測試專案的方案加入至版本控制，並且簽入所有檔案。  
  
本主題中的程序將描述如何建立組建定義，以便在自動化測試回合中執行您的單元測試：  
  
1.  [設定測試設定以在 x64 組建代理程式上執行資料庫單元測試](#ConfigureX64)  
  
2.  [將測試指派給測試分類 (選擇性)](#CreateATestList)  
  
3.  [修改測試專案](#ModifyTestProject)  
  
4.  [簽入方案](#CheckInTheTestList)  
  
5.  [建立組建定義](#CreateBuildDef)  
  
6.  [執行新的組建定義](#RunBuild)  
  
**在組建電腦上執行 SQL Server 單元測試**  
  
當您在組建電腦上執行單元測試時，單元測試可能找不到資料庫專案檔 (.sqlproj)。 發生這個問題的原因是 app.config 檔案會使用相對路徑來參考這些檔案。 此外，如果您的單元測試找不到要用來執行單元測試之 SQL Server 的執行個體，這些單元測試可能會失敗。 如果儲存在 app.config 檔案中的連接字串無法從組建電腦執行，就可能會發生這個問題。  
  
若要解決這些問題，您必須在 app.config 中指定覆寫區段，以便使用 Team Foundation Build 環境專用的組態檔來覆寫 app.config。 如需詳細資訊，請參閱本主題後面的[修改測試專案](#ModifyTestProject)。  
  
## <a name="ConfigureX64"></a>設定測試設定以在 x64 組建代理程式上執行 SQL Server 單元測試  
針對 x64 組建代理程式執行單元測試之前，您必須先進行測試設定以變更主機處理序平台。  
  
#### <a name="to-specify-the-host-process-platform"></a>若要指定主機處理序平台  
  
1.  開啟包含您想要進行設定之測試專案的方案。  
  
2.  在 [方案總管] 的 [方案項目] 資料夾中，按兩下 **Local.testsettings** 檔案。  
  
    [測試設定] 對話方塊隨即出現。  
  
3.  在清單中，按一下 [主機]。  
  
4.  在詳細資料窗格的 [主機處理序平台] 中，按一下 [MSIL] 以設定在 x64 組建代理程式上執行測試。  
  
5.  按一下 **[套用]**。  
  
## <a name="CreateATestList"></a>將測試指派給測試分類 (選擇性)  
一般而言，當您建立組建定義以執行單元測試時，可以指定一個或多個測試分類。 指定之分類中的所有測試都會在組建執行時執行。  
  
#### <a name="to-assign-tests-to-a-test-category"></a>若要將測試指派給測試分類  
  
1.  開啟 [測試檢視] 視窗。  
  
2.  選取測試。  
  
3.  在 [屬性] 窗格中，按一下 [測試分類]，然後按一下最右側欄中的省略符號 (...)。  
  
4.  在 [測試分類] 視窗的 [加入新分類] 方塊中，輸入新測試分類的名稱。  
  
5.  按一下 [加入]，然後按一下 [確定]。  
  
    新的測試分類將會指派給您的測試，而且將透過屬性提供給其他測試。  
  
## <a name="ModifyTestProject"></a>修改測試專案  
根據預設，Team Foundation Build 會在建置單元測試專案時，根據專案的 app.config 檔案建立組態檔。 資料庫專案的路徑在 app.config 檔案中是儲存為相對路徑。 可在 Visual Studio 中運作的相對路徑將無法運作，因為 Team Foundation Build 會將建置的檔案放入相對於單元測試執行位置的不同位置。 此外，您的 app.config 檔案包含指定要測試之資料庫的連接字串。 如果單元測試必須連接的資料庫與建立測試專案時使用的資料庫不同，您也需要針對 Team Foundation Build 建立個別的 app.config 檔案。 藉由進行下一項程序的修改，您可以設定測試專案和組建伺服器，讓 Team Foundation Build 使用不同的組態。  
  
> [!IMPORTANT]  
> 您必須針對每個測試專案 (.vbproj 或 .vsproj) 執行這個程序。  
  
#### <a name="to-specify-an-appconfig-file-for-team-foundation-build"></a>若要指定 Team Foundation Build 的 app.config 檔案  
  
1.  在 [方案總管] 中，以滑鼠右鍵按一下 app.config 檔案，然後按一下 [複製]。  
  
2.  以滑鼠右鍵按一下測試專案，然後按一下 [貼上]。  
  
3.  以滑鼠右鍵按一下名為 [複本 - app.config] 的檔案，然後按一下 [重新命名]。  
  
4.  輸入 _BuildComputer_**.sqlunitttest.config** 並按 ENTER，其中 *BuildComputer* 是執行組建代理程式的電腦名稱。  
  
5.  按兩下 *BuildComputer*.sqlunitttest.config。  
  
    組態檔就會在編輯器中開啟。  
  
6.  加入 Sources 資料夾的資料夾層級以及與方案具有相同名稱的子資料夾，藉以變更 .sqlproj 檔案的相對路徑。 例如，如果組態檔一開始包含下列項目：  
  
    ```  
    <DatabaseDeployment DatabaseProjectFileName="..\..\..\Database3\Database3.sqlproj"      Configuration="Debug" />  
    ```  
  
    請更新檔案為下列內容：  
  
    ```  
    <DatabaseDeployment DatabaseProjectFileName="..\..\..\Database3\Database3.sqlproj"      Configuration="Debug" />  
    ```  
  
    完成之後，您的 *BuildComputer*.sqlunitttest.config 檔案應該類似下列 Visual Studio 2010 的範例：  
  
    ```  
    <SqlUnitTesting_VS2010>  
        <DatabaseDeployment DatabaseProjectFileName="..\..\..\Database4\Database4.sqlproj"  
            Configuration="Debug" />  
        <DataGeneration ClearDatabase="true" />  
        <ExecutionContext Provider="System.Data.SqlClient" ConnectionString="Data Source=(localdb)\Projects;Initial Catalog=Database4;Integrated Security=True;Pooling=False"  
            CommandTimeout="30" />  
        <PrivilegedContext Provider="System.Data.SqlClient" ConnectionString="Data Source=(localdb)\Projects;Initial Catalog=Database4;Integrated Security=True;Pooling=False"  
            CommandTimeout="30" />  
    </SqlUnitTesting_VS2010>  
    ```  
  
    或者，如果您是使用 Visual Studio 2012：  
  
    ```  
    <SqlUnitTesting_VS2012>  
            <DatabaseDeployment DatabaseProjectFileName="..\..\..\Database4\Database4.sqlproj"  
                Configuration="Debug" />  
            <DataGeneration ClearDatabase="true" />  
            <ExecutionContext Provider="System.Data.SqlClient" ConnectionString="Data Source=(localdb)\Projects;Initial Catalog=Database4;Integrated Security=True;Pooling=False"  
                CommandTimeout="30" />  
            <PrivilegedContext Provider="System.Data.SqlClient" ConnectionString="Data Source=(localdb)\Projects;Initial Catalog=Database4;Integrated Security=True;Pooling=False"  
                CommandTimeout="30" />  
        </SqlUnitTesting_VS2012>  
    ```  
  
7.  更新 ExecutionContext 和 PrivilegedContext 的 ConnectionString 屬性以指定您想要部署之目標資料庫的連接。  
  
8.  按一下 [ **檔案** ] 功能表上的 [ **全部儲存**]。  
  
9. 在 [方案總管] 中，按兩下 app.config。  
  
10. 在編輯器中，針對每個 \<SqlUnitTesting_*VSVersion*> 節點，加入 `AllowConfigurationOverride="true"`。 例如：  
  
    ```  
    -- Update SqlUnitTesting_VS2010 node to:  
    <SqlUnitTesting_VS2010 AllowConfigurationOverride="true">   
  
    -- Update SqlUnitTesting_VS2012 node to:  
    <SqlUnitTesting_VS2012 AllowConfigurationOverride="true">  
    ```  
  
    透過進行這項變更，您便允許 Team Foundation Build 使用已建立的取代組態檔。  
  
11. 按一下 [ **檔案** ] 功能表上的 [ **全部儲存**]。  
  
    接下來，您必須更新 Local.testsettings 以包含自訂的組態檔。  
  
#### <a name="to-customize-localtestsettings-to-deploy-the-customized-configuration-file"></a>若要自訂 Local.testsettings 以部署自訂的組態檔  
  
1.  在 [方案總管] 中，按兩下 Local.testsettings。  
  
    [測試設定] 對話方塊隨即出現。  
  
2.  在分類目錄清單中，按一下 [部署]。  
  
3.  選取 [啟用部署] 核取方塊。  
  
4.  按一下 [加入檔案]。  
  
5.  在 [加入部署檔案] 對話方塊中，指定您建立的 *BuildComputer*.sqlunitttest.config 檔案。  
  
6.  按一下 **[套用]**。  
  
7.  按一下 [ **關閉**]。  
  
8.  按一下 [ **檔案** ] 功能表上的 [ **全部儲存**]。  
  
    接下來，您必須將方案簽入至版本控制。  
  
## <a name="CheckInTheTestList"></a>簽入方案  
在這個程序中，您會簽入方案的所有檔案。 這些檔案包括方案的測試中繼資料檔案，其中包含您的測試分類關聯和測試。 每當您加入、刪除、重新組織或變更測試的內容時，您的測試中繼資料檔案就會自動更新以反映這些變更。  
  
> [!NOTE]  
> 這個程序所描述的步驟適用於 Team Foundation 版本控制。 如果您使用不同的版本控制軟體，就必須依照該軟體適用的步驟進行。  
  
#### <a name="to-check-in-the-solution"></a>若要簽入方案  
  
1.  連接到執行 Team Foundation Server 的電腦。  
  
    如需詳細資訊，請參閱[使用原始檔控制總管](https://msdn.microsoft.com/library/ms181370(VS.100).aspx)。  
  
2.  如果您的方案原本不在原始檔控制中，請將它加入至原始檔控制。  
  
    如需詳細資訊，請參閱[將專案或方案加入至版本控制](https://msdn.microsoft.com/library/ms181374(VS.100).aspx)。  
  
3.  按一下 [檢視]，然後按一下 [暫止簽入]。  
  
4.  簽入方案的所有檔案。  
  
    如需詳細資訊，請參閱[簽入暫止的變更](https://msdn.microsoft.com/library/ms181411(VS.100).aspx)。  
  
    > [!NOTE]  
    > 您可能會有控管自動化測試之建立與管理方式的特定小組程序。 例如，此程序可能會要求您必須先在本機驗證組建，然後再簽入該程式碼以及將要針對程式碼執行的測試。  
  
    在 [方案總管] 中，掛鎖圖示會出現在每一個檔案的旁邊，指出它已簽入。 如需詳細資訊，請參閱[檢視版本控制檔案和資料夾屬性](https://msdn.microsoft.com/library/ms245468(VS.100).aspx)。  
  
    您的測試可用於 Team Foundation Build。 您現在可以建立包含想要執行之測試的組建定義。  
  
## <a name="CreateBuildDef"></a>建立組建定義  
  
#### <a name="to-create-a-build-definition"></a>若要建立組建定義  
  
1.  在 Team Explorer 中，按一下您的 Team 專案、以滑鼠右鍵按一下 [組建] 節點，然後按一下 [新增組建定義]。  
  
    [新增組建定義] 視窗隨即出現。  
  
2.  在 [組建定義名稱] 中，輸入您想要用於組建定義的名稱。  
  
3.  在巡覽列中，按一下 [組建預設值]。  
  
4.  在 [將組建輸出複製到下列置放資料夾 (UNC 路徑，例如 \\\server\share)] 中，指定要包含組建輸出的資料夾。  
  
    您可以指定本機電腦上的共用資料夾或是組建處理序將擁有權限的任何網路位置。  
  
5.  在巡覽列中，按一下 [處理序]。  
  
6.  在 [必要項] 群組的 [要建置的項目] 中，按一下瀏覽 (...) 按鈕。  
  
7.  在 [建置專案清單編輯器] 對話方塊中，按一下 [加入]。  
  
8.  指定您先前在本逐步解說中加入至版本控制的方案檔 (.sln)，然後按一下 [確定]。  
  
    此方案就會顯示在 [要建置的專案或方案檔] 清單中。  
  
9. 按一下 [確定] 。  
  
10. 在 [基本] 群組的 [自動化測試] 中，指定您要執行的測試。 根據預設，系統將會執行解決方案中名為 \*test\*.dll 之檔案所包含的測試。  
  
11. 在 [檔案] 功能表上，按一下 [儲存 *ProjectName*]。  
  
    您已建立組建定義。 接下來，您必須修改測試專案。  
  
## <a name="RunBuild"></a>執行新的組建定義  
  
#### <a name="to-run-the-new-build-type"></a>若要執行新的組建類型  
  
1.  在 [Team 總管] 中，展開 Team 專案節點、展開 [組建] 節點、以滑鼠右鍵按一下您想要執行的組建定義，然後按一下 [佇列新組建]。  
  
    [佇列組建 {_TeamProjectName_}] 對話方塊隨即出現，並列出所有現有的組建類型。  
  
2.  必要時，請在 [組建定義] 中按一下您的新組建定義。  
  
3.  確認 [組建定義]、[組建代理程式] 和 [此組建的置放資料夾] 欄位中的值都正確無誤，然後按一下 [佇列]。  
  
    [Build 總管] 的 [已佇列] 索引標籤隨即出現。 如需詳細資訊，請參閱[管理和檢視已完成的組建 (Visual Studio 2010)](https://msdn.microsoft.com/library/ms181730(VS.100).aspx) 或[在 Build 總管中管理您的組建 (Visual Studio 2012)](https://msdn.microsoft.com/library/ms181732.aspx)。  
  
## <a name="see-also"></a>另請參閱  
[執行 SQL Server 單元測試](../ssdt/running-sql-server-unit-tests.md)  
[建立基本組建定義](https://msdn.microsoft.com/library/ms181716(VS.100).aspx)  
[將組建排入佇列](https://msdn.microsoft.com/library/ms181722(VS.100).aspx)  
[監視執行中組建的進度](https://msdn.microsoft.com/library/ms181724(VS.100).aspx)  
  
