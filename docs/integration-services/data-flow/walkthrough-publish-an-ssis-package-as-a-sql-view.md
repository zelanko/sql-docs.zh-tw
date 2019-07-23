---
title: 逐步解說：將 SSIS 套件發佈為 SQL 檢視 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.packagepublishwizard.f1
ms.assetid: d32d9761-93fb-4020-bf82-231439c6f3ac
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 401422fcd3c2e32dcd83bebc3ef51351ca83555f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68079817"
---
# <a name="walkthrough-publish-an-ssis-package-as-a-sql-view"></a>逐步解說：發行 SSIS 封裝做為 SQL 檢視

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  本逐步解說提供詳細的步驟來發行 SSIS 封裝，以做為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中的 SQL 檢視。  
  
## <a name="prerequisites"></a>Prerequisites  
 您必須先在電腦上安裝下列軟體，才能執行本逐步解說。  
  
1.  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或更新版本以及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]。  
  
2.  [SQL Server Data Tools](../../ssdt/download-sql-server-data-tools-ssdt.md)。  
  
## <a name="step-1-build-and-deploy-ssis-project-to-the-ssis-catalog"></a>步驟 1:建置 SSIS 專案並部署至 SSIS 目錄  
 在此步驟中，您會建立 SSIS 封裝，從 SSIS 支援的資料來源 (在此範例中，我們使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫) 擷取資料，並使用資料流目的地元件輸出資料。 然後您會建置 SSIS 專案並部署至 SSIS 目錄。  
  
1.  啟動 **SQL Server Data Tools**。 在 **[開始]** 功能表上，依序指向 **[所有程式]** 和 **[Microsoft SQL Server]** ，然後按一下 **[SQL Server Data Tools]** 。  
  
2.  建立新的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案。  
  
    1.  在功能表列上按一下 [檔案]  、指向 [新增]  ，然後按一下 [專案]  。  
  
    2.  在左窗格中展開 [商業智慧]  ，然後按一下樹狀檢視中的 [Integration Services]  。  
  
    3.  如果尚未選取，請選取 [Integration Services 專案]  。  
  
    4.  指定 **SSISPackagePublishing** 做為 **專案名稱**。  
  
    5.  指定專案的位置。  
  
    6.  按一下 [確定]  ，以關閉 [新增專案]  對話方塊。  
  
3.  將 [資料流程]  元件從 [SSIS 工具箱]  拖曳至 [控制流程]  索引標籤的設計介面。  
  
4.  按兩下 [控制流程]  中的 [資料流程]  元件，以開啟 [資料流程設計師]  。  
  
5.  將 **來源元件** 從工具箱拖曳至 [資料流程設計師]  ，並將它設定為從資料來源擷取資料。  
  
    1.  基於本逐步解說的目的，建立測試資料庫︰**TestDB** 以及資料表︰**Employee**。 建立具有下列三個資料行的資料表： **ID**、 **FirstName** 及 **LastName**。  
  
    2.  將 **ID** 設為主索引鍵。  
  
    3.  使用下列資料插入兩筆記錄。  
  
        |ID|FirstName|LastName|  
        |--------|---------------|--------------|  
        |1|John|Doe|  
        |2|Jane|Doe|  
  
    4.  將 [OLE DB 來源]  元件從 [SSIS 工具箱]  拖曳至 [資料流程設計師]  。  
  
    5.  設定元件以便從 **TestDB** 資料庫的 **Employee** 資料表中擷取資料。 針對 [OLE DB 連線管理員]  選取 [(local).TestDB]  、針對 [資料存取模式]  選取 [資料表或檢視表]  ，以及針對 [資料表或檢視表的名稱]  選取 [[dbo].[Employee]]  。  
  
         ![資料流目的地 - OLE DB 連線](../../integration-services/data-flow/media/dsd-oledbconnectionmanager.jpg "資料流目的地 - OLE DB 連線")  
  
6.  現在，將 [資料流目的地]  從工具箱拖曳至資料流程。 您應該可在工具箱的 [一般] 區段中找到此元件。  
  
7.  將資料流程中的 [OLE DB 來源]  元件連接到 [資料流目的地]  元件。  
  
8.  建置 SSIS 專案並部署至 SSIS 目錄。  
  
    1.  按一下功能表列上的 [專案]  ，然後按一下 [部署]  。  
  
    2.  遵循精靈中的指示，將專案部署至本機資料庫伺服器中的 SSIS 目錄。 下列範例使用 **Power BI** 做為資料夾名稱，以及使用 **SSISPackagePublishing** 做為 SSIS 目錄中的專案名稱。  
  
## <a name="step-2-use-the-ssis-data-feed-publishing-wizard-to-publish-ssis-package-as-a-sql-view"></a>步驟 2:使用 SSIS 資料摘要發行精靈將 SSIS 套件發佈為 SQL 檢視  
 在此步驟中，您將使用 SQL Server Integration Services (SSIS) 資料摘要發行精靈，來發行 SSIS 封裝做為 SQL Server 資料庫中的檢視。 封裝的輸出資料可藉由查詢這個檢視來取用。  
  
 SSIS 資料摘要發行精靈會使用適用於 SSIS 的 OLE DB 提供者 (SSISOLEDB) 建立連結的伺服器，然後建立 SQL 檢視，其中包含連結伺服器上的查詢。 此查詢包括 SSIS 目錄中的資料夾名稱、專案名稱和封裝名稱。  
  
 在執行階段，檢視會透過您建立的連結伺服器，將查詢傳送至適用於 SSIS 的 OLE DB 提供者。 適用於 SSIS 的 OLE DB 提供者會執行您在查詢中指定的封裝，並將表格式結果集傳回查詢。  
  
1.  從 C:\Program Files\Microsoft SQL Server\130\DTS\Binn 執行 ISDataFeedPublishingWizard.exe，或按一下 [開始\所有程式] 下方的 [Microsoft SQL Server 2016\SQL Server 2016 Data Feed Publishing Wizard (Microsoft SQL Server 2016\SQL Server 2016 資料摘要發行精靈)]，來啟動 [SSIS 資料摘要發行精靈]  。  
  
2.  在 [簡介]  頁面上，按 [下一步]  。  
  
     ![資料摘要發行精靈 - 簡介頁面](../../integration-services/data-flow/media/dsd-feedpublishingwizard-introductionpage.jpg "資料摘要發行精靈 - 簡介頁面")  
  
3.  在 [封裝設定]  頁面上，執行下列動作：  
  
    1.  輸入包含 SSIS 目錄的 SQL Server 執行個體 **名稱** ，或按一下 [瀏覽]  來選取伺服器。  
  
         ![資料摘要發行精靈 - 套件設定頁面](../../integration-services/data-flow/media/dsd-feedpublishingwizard-packagesettingspage.jpg "資料摘要發行精靈 - 套件設定頁面")  
  
    2.  按一下 [路徑] 欄位旁的 [瀏覽]  、瀏覽 SSIS 目錄、選取您要發行的 SSIS 套件 (例如︰[SSISDB]  ->[SSISPackagePublishing]  ->[Package.dtsx]  )，然後按一下 [確定]  。  
  
         ![資料摘要發行精靈 - 瀏覽套件](../../integration-services/data-flow/media/dsd-feedpublishingwizard-browseforpackage.jpg "資料摘要發行精靈 - 瀏覽套件")  
  
    3.  使用頁面底部的 [封裝參數]、[專案參數] 和 [連接管理員] 索引標籤，針對任何封裝參數、專案參數或適用於封裝的連接管理員設定來輸入值。 您也可以指定要用來進行封裝執行的環境參考，並將專案/封裝參數繫結至環境變數。  
  
         我們建議您將敏感性參數繫結至環境變數。 這是為了確保敏感性參數的值不會以純文字格式儲存於精靈所建立的 SQL 檢視中。  
  
    4.  按 [下一步]  以切換 [發行設定]  頁面。  
  
4.  在 [發行設定]  頁面上，執行下列動作：  
  
    1.  針對要建立的檢視選取 **資料庫** 。  
  
         ![資料摘要發行精靈 - 發行設定頁面](../../integration-services/data-flow/media/dsd-feedpublishingwizard-publishsettingspage.jpg "資料摘要發行精靈 - 發行設定頁面")  
  
    2.  輸入 **檢視** 的 **名稱**。 您也可以從下拉式清單選取現有的檢視。  
  
    3.  在 [設定]  清單中，指定要與檢視建立關聯的**連結的伺服器** **名稱**。 如果連結的伺服器尚未存在，精靈將會在建立檢視之前先建立連結的伺服器。 您也可以在這裡設定 **User32BitRuntime** 和 **Timeout** 的值。  
  
    4.  按一下 [進階]  按鈕。 您應該會看見 [進階設定]  對話方塊。  
  
    5.  在 [進階設定]  對話方塊中，執行下列動作︰  
  
        1.  指定您想要在其中建立檢視的資料庫結構描述 ([結構描述] 欄位)。  
  
        2.  指定在透過網路傳送資料之前，是否應先加密資料 ([加密] 欄位)。 如需此設定和 TrustServerCertificate 設定的詳細資訊，請參閱 [使用加密而不需驗證](../../relational-databases/native-client/features/using-encryption-without-validation.md) 主題。  
  
        3.  指定在啟用加密設定時，是否可以使用自我簽署的伺服器憑證 ([TrustServerCertificate]  欄位)。  
  
        4.  按一下 **[確定]** 以關閉 **[進階設定]** 對話方塊。  
  
    6.  按 [下一步]  ，切換到 [驗證]  頁面。  
  
5.  在 [驗證]  頁面上，檢閱驗證所有設定之值的結果。 在下列範例中，您會看到關於連結的伺服器是否存在的 **警告** ，因為連結的伺服器不存在於選取的 SQL Server 執行個體上。 如果您在 **結果** 中看見 **錯誤**，請將滑鼠游標移到 **錯誤** 上方，您將會看到關於此錯誤的詳細資料。 例如，如果您尚未針對 SSISOLEDB 提供者啟用 [允許 Inprocess] 選項，就會在 [連結伺服器的組態] 動作上得到錯誤。  
  
     ![資料摘要發行精靈 - 驗證頁面](../../integration-services/data-flow/media/dsd-feedpublishingwizard-validationpage.jpg "資料摘要發行精靈 - 驗證頁面")  
  
6.  若要將此報表儲存為 XML 檔案，可按一下 [儲存報表]。  
  
7.  在 [驗證]  頁面上按 [下一步]  ，切換到 [摘要]  頁面。  
  
8.  在 [摘要]  頁面中檢視您的選取項目，然後按一下 [發行]  來啟動發行程序，這將會建立連結的伺服器 (如果它尚未存在於伺服器上)，然後使用連接的伺服器建立檢視。  
  
     ![資料摘要發行精靈 - 摘要頁面](../../integration-services/data-flow/media/dsd-feedpublishingwizard-summarypage.jpg "資料摘要發行精靈 - 摘要頁面")  
  
     您現在可以針對 TestDB 資料庫執行下列 SQL 陳述式來查詢套件的輸出資料：SELECT * FROM [SSISPackageView]。  
  
9. 若要將此報表儲存為 XML 檔案，可按一下 [儲存報表]  。  
  
10. 檢閱發行程序的結果，然後按一下 [完成]  以關閉精靈。  
  
    > [!NOTE]  
    >  不支援下列資料類型︰text、ntext、image、nvarchar(max)、varchar(max) 及 varbinary(max)。  
  
## <a name="step-3-test-the-sql-view"></a>步驟 3：測試 SQL 檢視  
 在此步驟中，您將執行 SSIS 資料摘要發行精靈所建立的 SQL 檢視。  
  
1.  啟動 SQL Server Management Studio。  
  
2.  依序展開 [\<機器名稱>]  、[資料庫]  、[\<您在精靈中選取的資料庫>]  及 [檢視]  。  
  
3.  以滑鼠右鍵按一下精靈建立的 [\<精靈建立的檢視>]  ，然後按一下 [選取前 1000 個資料列]  。  
  
4.  確認您看到 SSIS 封裝的結果。  
  
## <a name="step-4-verify-the-ssis-package-execution"></a>步驟 4：確認 SSIS 封裝執行  
 在此步驟中，您將驗證已執行 SSIS 封裝。  
  
1.  在 SQL Server Management Studio 中，依序展開 [Integration Services 目錄]  、[SSISDB]  、您 SSIS 專案所在的 **資料夾** 、[專案]  、您的專案節點，以及 [封裝]  。  
  
2.  在 SSIS 封裝上按一下滑鼠右鍵，接著按一下以依序指向 [報表]  和 [標準報表]  ，然後按一下 [所有執行]  。  
  
3.  您應該會在報表中看到 SSIS 封裝執行。  
  
    > [!NOTE]  
    >  在 Windows Vista Service Pack 2 電腦上，您可能會在報表中看到兩個 SSIS 封裝執行 (一個成功執行和一個失敗執行)。 請忽略失敗的執行，因為它是由此版本中已知問題所引發。  
  
## <a name="more-info"></a>其他資訊  
 資料摘要發行精靈會執行下列重要步驟︰  
  
1.  建立連結的伺服器，並設定它來使用適用於 SSIS 的 OLE DB 提供者。  
  
2.  在指定的資料庫中建立 SQL 檢視，使用所選封裝的目錄資訊來查詢連結的伺服器。  
  
 本節提供建立連結的伺服器和 SQL 檢視的程序，而不使用資料摘要發行精靈。 它也會提供搭配適用於 SSIS 的 OLE DB 提供者使用 OPENQUERY 函式的其他相關資訊。  
  
### <a name="create-a-linked-server-using-the-ole-db-provider-for-ssis"></a>使用適用於 SSIS 的 OLE DB 提供者建立連結的伺服器  
 在 SQL Server Management Studio 中執行下列查詢，使用適用於 SSIS 的 OLE DB 提供者 (SSISOLEDB) 建立連結的伺服器。  
  
```sql 
  
USE [master]  
GO  
  
EXEC sp_addlinkedserver  
@server = N'SSISFeedServer',  
@srvproduct = N'Microsoft',  
@provider = N'SSISOLEDB',  
@datasrc = N'.'  
GO  
  
```  
  
### <a name="create-a-view-using-linked-server-and-ssis-catalog-information"></a>使用連結的伺服器和 SSIS 目錄資訊建立檢視  
 在此步驟中，您將建立 SQL 檢視，於您在上一節中建立的連結伺服器上執行查詢。 查詢將包括 SSIS 目錄中的資料夾名稱、專案名稱和封裝名稱。  
  
 在執行階段中執行檢視時，檢視中定義的連結伺服器查詢會啟動查詢中指定的 SSIS 封裝，並接收封裝輸出做為表格式結果集。  
  
1.  建立檢視之前，在新的查詢視窗中輸入並執行下列查詢。 OPENQUERY 是 SQL Server 所支援的資料列集函式。 它會使用與連結的伺服器相關聯的 OLE DB 提供者，在指定的連結伺服器上執行指定的傳遞查詢。 您可以依照資料表名稱的相同方式，在查詢的 FROM 子句中參考 OPENQUERY。 如需詳細資訊，請參閱 [MSDN Library 上的 OPENQUERY 文件](../../t-sql/functions/openquery-transact-sql.md) 。  
  
    ```sql
    SELECT * FROM OPENQUERY(SSISFeedServer,N'Folder=Eldorado;Project=SSISPackagePublishing;Package=Package.dtsx')   
    GO  
    ```  
  
    > [!IMPORTANT]  
    >  視需要更新資料夾名稱、專案名稱和封裝名稱。 如果 OPENQUERY 函式失敗，可在 **SQL Server Management Studio**中，依序展開 [伺服器物件]  、[連結的伺服器]  及 [提供者]  ，然後按兩下 [SSISOLEDB]  提供者，並確定已啟用 [允許 inprocess]  選項。  
  
2.  執行下列查詢，在資料庫 **TestDB** 中建立檢視以供本逐步解說使用。  
  
    ```sql
  
    USE [TestDB]   
    GO   
  
    CREATE VIEW SSISPackageView AS   
    SELECT * FROM OPENQUERY(SSISFeedServer, 'Folder=Eldorado;Project=SSISPackagePublishing;Package=Package.dtsx')   
    GO  
  
    ```  
  
3.  執行下列查詢來測試檢視。  
  
    ```sql
    SELECT * FROM SSISPackageView  
    ```  
  
### <a name="openquery-function"></a>OPENQUERY 函式  
 OPENQUERY 函式的語法是︰  
  
```sql 
SELECT * FROM OPENQUERY(<LinkedServer Name>, N'Folder=<Folder Name from SSIS Catalog>; Project=<SSIS Project Name>; Package=<SSIS Package Name>; Use32BitRuntime=[True | False];Parameters="<parameter_name_1>=<value1>; parameter_name_2=<value2>";Timeout=<Number of Seconds>;')  
```  
  
 Folder、Project 及 Package參數都是必要項。 Use32BitRuntime、Timeout 及 Parameters 則是選擇性的。  
  
 Use32BitRuntime 的值可以是 0、1、true 或 false。 此值會指出當 SQL Server 的平台為 64 位元時，封裝是否應使用 32 位元執行階段 (1 或 true) 來執行。  
  
 Timeout 表示在來自 SSIS 封裝的新資料到達之前，適用於 SSIS 的 OLE DB 提供者可以等待的秒數。 預設逾時為 60 秒。 您可以為逾時指定介於 20 和 32000 之間的整數值。  
  
 Parameters 包含封裝參數和專案參數的值。 參數的規則與 [DTExec](https://msdn.microsoft.com/library/hh231187.aspx)中的參數相同。  
  
 下列清單指定查詢子句中允許的特殊字元︰  
  
-   單一引號 (') - 標準 OPENQUERY 支援此字元。 如果您想要在查詢子句中使用單引號，請使用兩個單引號 ('')。  
  
-   雙引號 (") - 查詢的參數部分會以雙引號括住。 如果參數值本身包含雙引號，請使用逸出字元。 例如： \"＞。  
  
-   左和右方括弧 ([ 和 ]) - 這些字元可用來表示前置/後端空格。 例如，「[ 一些空格 ]」代表「 一些空格 」字串，其中有一個前置空格和一個尾端空格。 如果這些字元本身會在查詢子句中使用，則必須逸出它們。 例如， \\和 \\]。  
  
-   正斜線 (\\) - 查詢子句中使用的每個 \ 都必須使用逸出字元。 例如，系統會將查詢子句中的 \\\ 評估為 \。  
  
 正斜線 (\\) - 查詢子句中使用的每個 \ 都必須使用逸出字元。 例如，系統會將查詢子句中的 \\\ 評估為 \。  
  
## <a name="see-also"></a>另請參閱  
 [資料流目的地](../../integration-services/data-flow/data-streaming-destination.md)   
 [設定資料流目的地](../../integration-services/data-flow/configure-data-streaming-destination.md)  
  
  
