---
title: 初始設定 (PowerPivot for SharePoint) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 3a0ec2eb-017a-40db-b8d4-8aa8f4cdc146
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: e331f25811255569261fb30c2869b428843ebfc5
ms.sourcegitcommit: 187f6d327421e64f1802a3085f88bbdb0c79b707
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/16/2019
ms.locfileid: "69530906"
---
# <a name="initial-configuration-powerpivot-for-sharepoint"></a>初始組態 (PowerPivot for SharePoint)
  您可以使用本主題的步驟，設定 PowerPivot for SharePoint 的初始安裝。 設定初始安裝最簡單的方式為使用 PowerPivot 組態工具， 以自動化下列所述的各項組態步驟。  
  
 或者，您如果想要對伺服器的設定擁有更多控制權，可以使用管理中心及本主題的資訊，執行各種步驟。  
  
 
  
## <a name="prerequisites"></a>先決條件  
 SharePoint 伺服器先使用 SharePoint 安裝程式中的伺服器陣列安裝選項加以安裝。 使用內建資料庫的獨立 SharePoint 伺服器不予支援。 如需詳細資訊, 請參閱[在 SharePoint 2010 伺服器陣列中使用 SQL SERVER BI 功能的指導](../../../2014/sql-server/install/guidance-for-using-sql-server-bi-features-in-a-sharepoint-2010-farm.md)方針。  
  
> [!IMPORTANT]  
>  您必須先安裝 SharePoint 2010 SP1，才可設定 PowerPivot for SharePoint 或使用 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 資料庫伺服器的 SharePoint 伺服器陣列。 如果您尚未安裝該 Service Pack，請在開始設定伺服器之前先加以安裝。  
  
 您必須安裝 PowerPivot for SharePoint。 至少必須部署伺服器陣列方案。 您可以使用 PowerPivot 組態工具或 PowerShell 指令碼部署伺服器陣列方案。 本主題將提供此步驟的指示。  
  
 電腦必須加入網域。 您為服務指定的帳戶必須是網域使用者帳戶。 PowerPivot 服務應用程式至少需要一個網域帳戶。 如果您要設定其他服務 (例如 Excel Services)，則每一項提供的服務都應該有個別的帳戶。  
  
 您必須是伺服陣列管理員，才能將 PowerPivot for SharePoint 加入到伺服陣列中。 您必須知道複雜密碼，才可將伺服器及應用程式加入伺服器陣列。  
  
##  <a name="deploywsp"></a> 步驟 1：部署 PowerPivot 方案  
 您必須安裝及部署伺服器陣列方案及 Web 應用程式方案。  
  
 **安裝和部署伺服器陣列方案**  
  
 在前一版中，SQL Server 安裝程式會安裝及部署伺服器陣列方案。 在本版中，您必須使用 PowerPivot 組態工具或 PowerShell 指令碼部署伺服器陣列方案。 您無法使用管理中心部署伺服器陣列方案。 這是 PowerPivot for SharePoint 組態步驟中，唯一無法在管理中心執行的步驟。 部署伺服器陣列方案之後，您即可使用管理中心及本主題的步驟設定 PowerPivot for SharePoint 安裝。  
  
 在此步驟中，您將執行 PowerShell，以安裝及部署伺服器陣列方案。 如需詳細資訊, 請參閱[使用 Windows PowerShell 的 PowerPivot](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/power-pivot-configuration-using-windows-powershell)設定。  
  
1.  使用 **[以系統管理員身分執行]** 選項，開啟 SharePoint 2010 管理命令介面。  
  
2.  執行第一個 Cmdlet：  
  
    ```  
    Add-SPSolution -LiteralPath "C:\Program Files\Microsoft SQL Server\120\Tools\PowerPivotTools\ConfigurationTool\Resources\PowerPivotFarm.wsp"  
    ```  
  
     此指令程式會傳回方案的名稱、方案識別碼及 Deployed=False。 在下個步驟中，您將部署方案。  
  
3.  執行第二個 Cmdlet 部署方案：  
  
    ```  
    Install-SPSolution -Identity PowerPivotFarm.wsp -GACDeployment -Force  
    ```  
  
 **部署 web 應用程式方案**  
  
1.  依序按一下 [開始] 按鈕、[**所有程式**]、[ **Microsoft SharePoint 產品 2010**], 然後選取 [ **SharePoint 2010 管理中心**]。  
  
2.  在 SharePoint 2010 管理中心的 [系統設定] 中，按一下 **[管理伺服陣列方案]** 。  
  
     您應該會看到兩個不同的方案套件：powerpivotfarm.wsp 和 powerpivotwebapp.wsp。 您必須先完成第一個方案 (powerpivotfarm.wsp) 的部署。 當其完成部署之後，即無須再行部署。 第二個方案 (powerpivotwebapp.wsp) 會針對管理中心來部署，但是您必須針對支援 PowerPivot 資料存取的每一個 SharePoint Web 應用程式來手動部署這個方案。  
  
3.  按一下 **[powerpivotwebapp.wsp]** 。  
  
4.  按一下 [**部署方案]。**  
  
5.  在 [**部署至？** ] 中, 選取您要加入 PowerPivot 功能支援的 SharePoint web 應用程式。  
  
6.  按一下 [確定]。  
  
7.  針對其他也支援 PowerPivot 資料存取的 SharePoint Web 應用程式重複以上步驟。  
  
##  <a name="Geneva"></a> 步驟 2：啟動伺服器上的服務  
 PowerPivot for SharePoint 部署需要您的伺服器陣列包含下列服務:Excel Calculation Services、Secure Store Service 和對 Windows token 服務的宣告。  
  
 對於 Excel Services 和 PowerPivot for SharePoint，需要對 Windows Token Service 的宣告。 它會透過目前 SharePoint 使用者的 Windows 識別，用來建立外部資料來源的連線。 此服務必須在啟用 Excel Services 或 PowerPivot for SharePoint 的每部 SharePoint 伺服器上執行。 如果此服務尚未啟動，您必須立即將它啟動，以便讓 Excel Services 將經過驗證的要求轉送給 PowerPivot 系統服務。  
  
1.  在管理中心的 [系統設定] 中，按一下 **[管理伺服器上的服務]** 。  
  
2.  啟動對 Windows Token Service 的宣告。  
  
3.  啟動 Excel Calculation Services。  
  
4.  啟動 Secure Store Service。  
  
5.  確認 SQL Server Analysis Services 和 SQL Server PowerPivot 系統服務都已啟動。  
  
##  <a name="createapp"></a> 步驟 3：建立 PowerPivot 服務應用程式  
 下一步是建立 PowerPivot 服務應用程式。  
  
1.  在 [管理中心] 的 [應用程式管理] 中，按一下 **[管理服務應用程式]** 。  
  
2.  在 **[服務應用程式]** 功能區中，按一下 **[新增]** 。  
  
3.  選取 [ **SQL Server PowerPivot 服務應用程式**]。 如果它沒有出現在清單中，表示未安裝 PowerPivot for SharePoint 或是未部署此方案。  
  
4.  在 [**建立新的 PowerPivot 服務應用程式**] 頁面中, 輸入應用程式的名稱。 預設值為 new-powerpivotserviceapplication\<number >。 如果您要建立多個 PowerPivot 服務應用程式，描述性名稱將可協助其他系統管理員，了解如何使用應用程式。  
  
5.  在 [應用程式集區] 中，建立新的應用程式集區，並為它選取安全性帳戶。 需要網域使用者帳戶。  
  
6.  在 [**資料庫伺服器**] 中, 選擇要在其上建立服務應用程式資料庫的資料庫伺服器。 預設值是主控伺服陣列組態資料庫的 SQL Server Database Engine 執行個體。  
  
7.  在 [**資料庫名稱**] 中, 預設值\<為 PowerPivotServiceApplication1_ guid >。 預設的資料庫名稱會對應至服務應用程式的預設名稱。 如果您輸入唯一的服務應用程式名稱，請依照類似的命名慣例來命名資料庫名稱，以利同時管理它們。  
  
8.  在 **[資料庫驗證]** 中，預設值是 Windows 驗證。 如果您選擇 **[SQL 驗證]** ，請參考 SharePoint 管理員指南，以了解有關如何在 SharePoint 部署中使用這個驗證類型的最佳作法。  
  
9. 選取 [**將這個 PowerPivot 服務應用程式的 Proxy 加入至預設 proxy 群組**] 核取方塊。 這會將服務應用程式連接加入到預設的服務連接群組。 預設連接群組中至少必須有一個 PowerPivot 服務應用程式。  
  
     如果 PowerPivot 服務應用程式已經列在預設連接群組中，請勿將第二個服務應用程式加入到該群組。 加入預設連接群組的兩個相同類型的服務應用程式並不是支援的組態。 如需如何在連接群組中使用其他服務應用程式的詳細資訊, 請參閱[在管理中心將 PowerPivot 服務應用程式連接到 SharePoint Web 應用程式](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/connect-power-pivot-service-app-to-sharepoint-web-app-in-ca)。  
  
10. 按一下 **[確定].** 此服務將會與伺服器陣列服務應用程式清單中的其他受管理的服務一起顯示。  
  
##  <a name="ExcelServ"></a> 步驟 4：啟用 Excel Services  
 PowerPivot for SharePoint 會要求 Excel Services 支援伺服陣列中的 PowerPivot 資料存取。 您可以判斷是否已經啟用 Excel Services，其方式是確認 Excel Services 應用程式是否出現在管理中心的服務應用程式清單內。 如果未列出 Excel Services，請立即遵循以下步驟來將它啟用。  
  
1.  在 [管理中心] 的 [應用程式管理] 中，按一下 **[管理服務應用程式]** 。  
  
2.  在 [服務應用程式] 功能區的 [建立] 中, 按一下 [**新增**]。  
  
3.  選取 [ **Excel Services 應用程式**]。  
  
4.  在 [建立新的 Excel Services 應用程式] 中，指定名稱 (例如 Excel Services 應用程式)。  
  
5.  在 [應用程式集區] 中，選取 [建立新的應用程式集區]，並為它提供描述性名稱 (例如 Excel Services 應用程式集區)。  
  
6.  在 [可設定] 中，針對這個應用程式集區識別選取 Windows 網域使用者帳戶。  
  
7.  保留預設核取方塊，將服務應用程式 Proxy 加入到預設的服務連接清單。  
  
8.  按一下 [確定]。  
  
9. 按一下您剛才建立的 Excel Services 應用程式。  
  
10. 按一下 [信任的檔案**位置**], 然後在此頁面上選取您信任的位置。 (一般而言, 這會在 [位址] 資料行中列為**HTTP://** )。若要確保 Excel Services 和 PowerPivot 服務可存取活頁簿，您必須將 SharePoint 併入為 Excel Services 信任的位置。 PowerPivot 系統服務無法存取儲存在 SharePoint 伺服陣列外面的活頁簿。  
  
11. 在 [活頁簿屬性] 區域中, 將 [**最大活頁簿大小**] 設定為50。  
  
12. 在 [外部資料] 中, 將 [**允許外部資料**] 設定為**信任的資料連線庫和 [內嵌**]。 活頁簿中的 PowerPivot 資料存取需要這項設定。  
  
13. 清除 [**在資料重新整理時警告**] 核取方塊, 以允許預覽 PowerPivot 圖庫中個別工作表的影像。 如果您選擇保留警告，而活頁簿設定指定在開啟時重新整理，您可能會得到警告的單一預覽影像，而不是活頁簿中的頁面。  
  
14. 按一下 [確定]。  
  
##  <a name="SSS"></a> 步驟 5：啟用 Secure Store Service 並設定資料重新整理  
 PowerPivot for SharePoint 需要 Secure Store Service 來儲存認證和無人看管的執行帳戶，以便重新整理資料。 您可以判斷是否已經啟用 Secure Store Service，其方式是確認它是否出現在服務應用程式清單內。  
  
> [!IMPORTANT]  
>  如果已啟用 Secure Store Service，您仍然應該確認是否已經為它產生主要金鑰。 如需指示, 請參閱第2部分:在下列程式中產生主要金鑰。  
  
 如果未列出 Secure Store Service，請立即遵循以下步驟來將它啟用。 啟用安全存放之後，當活頁簿作者和文件擁有者在排程其發行之活頁簿的資料重新整理時，就可以存取更大範圍的資料來源連接選項。  
  
##### <a name="part-1-enable-secure-store-service"></a>第 1 部分：啟用 Secure Store Service  
  
1.  在 [管理中心] 的 [應用程式管理] 中，按一下 **[管理服務應用程式]** 。  
  
2.  在 [服務應用程式] 功能區的 [建立] 中, 按一下 [**新增**]。  
  
3.  選取 [ **Secure Store Service**]。  
  
4.  在 [**建立 Secure Store 應用程式**] 頁面中, 輸入應用程式的名稱。  
  
5.  在 [**資料庫**] 中, 指定將裝載此服務應用程式之資料庫的 SQL Server 實例。 預設值是主控伺服陣列組態資料庫的 SQL Server Database Engine 執行個體。  
  
6.  在 [**資料庫名稱**] 中, 輸入服務應用程式資料庫的名稱。 預設值為 Secure_Store_Service_DB_\<guid >。 預設名稱會對應至服務應用程式的預設名稱。 如果您輸入唯一的服務應用程式名稱，請依照類似的命名慣例來命名資料庫名稱，以利同時管理它們。  
  
7.  在 **[資料庫驗證]** 中，預設值是 Windows 驗證。 如果您選擇 [SQL 驗證]，請參考 SharePoint 管理員指南，以取得如何在伺服陣列中使用這個驗證類型的指引。  
  
8.  在應用程式集區中, 選取 [**建立新應用程式集**區]。 指定描述性名稱，將可協助其他伺服器系統管理員識別如何使用應用程式集區。  
  
9. 選取應用程式集區的安全性帳戶。 指定受管理的帳戶，以使用網域使用者帳戶。  
  
10. 接受其餘的預設值, 然後按一下 **[確定]。** 服務應用程式將會和伺服陣列的服務應用程式清單中其他受管理的服務一起並排顯示。  
  
##### <a name="part-2-generate-the-master-key"></a>第 2 部分：產生主要金鑰  
  
1.  從清單按一下 Secure Store Service 應用程式。  
  
2.  在 [服務應用程式] 功能區中, 按一下 [**管理**]。  
  
3.  在 [金鑰管理] 中, 按一下 [**產生新金鑰**]。  
  
4.  輸入複雜密碼，然後進行確認。 此複雜密碼將用於加入其他安全存放共用服務應用程式。  
  
5.  按一下 [確定]。  
  
##### <a name="part-3-configure-the-unattended-powerpivot-data-refresh-account"></a>第 3 部分：設定無人看管的 PowerPivot 資料重新整理帳戶  
 在資料重新整理期間使用外部資料存取時，通常需要針對 PowerPivot 資料存取建立自動資料重新整理帳戶。 例如，如果未啟用 Kerberos，您必須建立一個自動帳戶，PowerPivot 服務可以使用此帳戶來連接外部資料來源。  
  
 如需有關如何建立自動 PowerPivot 資料重新整理帳戶或資料重新整理中所用其他預存認證的指示, 請參閱[設定 PowerPivot 無人&#40;看管&#41;的資料重新整理帳戶 PowerPivot for SharePoint](../../analysis-services/configure-unattended-data-refresh-account-powerpivot-sharepoint.md)和[設定 PowerPivot 資料重新整理&#40;PowerPivot for SharePoint&#41;的預存認證](../../../2014/analysis-services/configure-stored-credentials-data-refresh-powerpivot-sharepoint.md)。  
  
##  <a name="Usage"></a> 步驟 6：啟用使用量資料收集  
 PowerPivot for SharePoint 會使用 SharePoint 使用量資料收集基礎結構，以蒐集整個伺服陣列中有關 PowerPivot 使用量的資訊。 雖然使用量資料一定是 SharePoint 安裝的一部分，但是您可能必須先啟用這個功能才可以使用。 如需指示, 請參閱[設定 PowerPivot for SharePoint 的&#40;使用量資料收集](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/configure-usage-data-collection-for-power-pivot-for-sharepoint)。  
  
##  <a name="Upload"></a>步驟 7:增加 SharePoint Web 應用程式和 Excel Services 的上傳大小上限  
 因為 PowerPivot 活頁簿可以很大，所以您可能會想要增加檔案大小上限。 有兩個要設定的檔案大小設定:Web 應用程式的最大上傳大小, 以及 Excel Services 中的活頁簿大小上限。 檔案大小上限應該在兩個應用程式中設定為相同的值。 如需指示, 請參閱[設定最大&#40;檔案&#41;上傳大小 PowerPivot for SharePoint](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/configure-maximum-file-upload-size-power-pivot-for-sharepoint)。  
  
##  <a name="activatePP"></a>步驟 8:為網站集合啟用 PowerPivot 功能整合  
 網站集合層級的功能啟用可以將應用程式頁面和範本提供給網站使用，包括排程資料重新整理的組態頁面，以及 PowerPivot 圖庫和資料摘要文件庫的應用程式頁面。  
  
1.  按一下 SharePoint 網站上的 [網站動作]。  
  
     根據預設，SharePoint Web 應用程式會經由通訊埠 80 進行存取。 這表示您通常可以藉由輸入 HTTP://\<電腦名稱稱 > 來存取 SharePoint 網站, 以開啟根網站集合。  
  
2.  按一下 **[站台設定]** 。  
  
3.  按一下 [網站集合管理] 中的 [網站集合功能]。  
  
4.  在您找到**PowerPivot 整合網站集合功能**之前, 請向下流覽頁面。  
  
5.  按一下 **[啟用]** 。  
  
6.  開啟每個網站並按一下 [網站動作]，為其他網站集合重複執行。  
  
 如需詳細資訊, 請參閱為[管理中心的網站集合啟用 PowerPivot 功能整合](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/activate-power-pivot-integration-for-site-collections-in-ca)。  
  
##  <a name="bkmk_redist"></a>步驟 9:在 SQL Server 2012 PowerPivot for SharePoint 實例上安裝 SQL Server 2008 R2 版的 OLE DB 提供者  
 如果您想要在相同的伺服器上並存執行舊版與新版的 PowerPivot 活頁簿，就必須安裝 Analysis Services OLE DB 提供者，其隨附於 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] PowerPivot for SharePoint 伺服器的 SQL Server 2008 R2 中。  
  
 安裝提供者可讓參考資料連接字串中 MSOLAP.4 的活頁簿在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] PowerPivot 伺服器上正常運作。 安裝 SQL Server 2008 R2 OLE DB 提供者是升級舊版 PowerPivot for Excel 所建立之活頁簿的替代方式。  
  
 您可以從[SQL Server 2008 R2 功能套件 頁面](https://go.microsoft.com/fwlink/?LinkId=159570)下載提供者。 尋找適用于**microsoft® SQL Server® 2008 R2 的 microsoft® Analysis Services OLE DB Provider**, 然後下載`SQLServer2008_ASOLEDB10.msi`安裝程式的 x64 封裝。  
  
 如需安裝提供者的詳細資訊, 包括驗證步驟, 請參閱[在 SharePoint 伺服器上安裝 Analysis Services OLE DB Provider](../../../2014/sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md)。  
  
##  <a name="verifyinstall"></a>步驟 10:確認安裝  
 當使用者或應用程式開啟含有 PowerPivot 資料的 Excel 活頁簿時，就會在伺服陣列中進行 PowerPivot 查詢處理。 您至少可以檢查 SharePoint 網站上的頁面，以確認 PowerPivot 功能是可用的。 但是，為了完整確認安裝作業，您必須擁有可以發行到 SharePoint 並從文件庫存取的 PowerPivot 活頁簿。 為了測試用途，您可以發行已經包含 PowerPivot 資料的範例活頁簿，並用它來確認 SharePoint 整合已正確設定。  
  
 若要確認 PowerPivot 可與 SharePoint 網站整合，請執行下列動作：  
  
1.  在瀏覽器中，開啟您建立的 Web 應用程式。 如果您使用預設值, 您可以在 URL\<位址中指定 HTTP://電腦名稱稱 >。  
  
2.  確認應用程式中可以使用 PowerPivot 資料存取和處理功能。 若要這樣做，您可以確認 PowerPivot 提供的文件庫範本是否存在：  
  
    1.  在 [網站動作] 上, 按一下 [**更多選項**]。  
  
    2.  在 [程式庫] 中, 您應該會看到**資料摘要庫**和**PowerPivot 圖庫**。 這些文件庫範本是由 PowerPivot 功能所提供，如果此功能已正確整合，就可以在文件庫清單中看到這些範本。  
  
 若要在伺服器上確認 PowerPivot 資料存取，請執行以下作業：  
  
1.  將 PowerPivot 活頁簿上傳至 PowerPivot 圖庫或任何 SharePoint 文件庫。  
  
2.  按一下文件，從文件庫中加以開啟。  
  
3.  按一下交叉分析篩選器或篩選資料來啟動 PowerPivot 查詢。 伺服器將會在背景載入 PowerPivot 資料，然後傳回結果。 在下一個步驟中，您將會連接到伺服器，並確認已經載入及快取資料。  
  
4.  在 [開始] 功能表中，從 Microsoft SQL Server 2008 R2 程式群組啟動 SQL Server Management Studio。 如果伺服器上未安裝這個工具，您可以跳到最後一個步驟，確認快取檔案存在。  
  
5.  在 [伺服器類型] 中，選取 [Analysis Services]。  
  
6.  在 [伺服器名稱] 中, 輸入 **\<伺服器名稱 > \powerpivot**, 其中 **\<伺服器名稱 >** 是具有 PowerPivot for SharePoint 安裝的電腦名稱稱。  
  
7.  按一下 **[連接]** 。  
  
8.  在物件總管中, 按一下 [**資料庫**] 以查看已載入的 PowerPivot 資料檔案清單。  
  
9. 在電腦檔案系統上，檢查下列資料夾來決定檔案是否要快取到磁碟。 快取檔案的存在會進一步驗證您的部署是否可以運作。 若要檢視檔案快取，請移至 \Program Files\Microsoft SQL Server\MSAS10_50.POWERPIVOT\OLAP\Backup 資料夾。  
  
##  <a name="nextsteps"></a>後續安裝步驟  
 在確認安裝之後，請建立 PowerPivot 圖庫或微調個別組態設定來完成服務組態。 若要充分利用剛才安裝的伺服器元件，您可以下載 [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)] 以建立您的第一個 PowerPivot 活頁簿，然後發行。  
  
### <a name="install-data-providers-used-for-data-refresh"></a>安裝用於資料重新整理的資料提供者  
 如果您已啟用資料重新整理，伺服器將需要 PowerPivot 用戶端應用程式針對外部資料存取使用的相同資料提供者，才能匯入原始資料 (例如，如果資料原本是使用 32 位元提供者匯入，那麼當伺服器端資料重新整理存取相同的外部資料來源時，也會需要 32 位元提供者)。 如需詳細資訊, 請參閱[PowerPivot Data Refresh With SharePoint 2010](../../../2014/analysis-services/powerpivot-data-refresh-with-sharepoint-2010.md)。  
  
### <a name="install-adonet-data-services"></a>安裝 ADO.NET Data Services  
 如果您想要將 SharePoint 清單當做資料摘要匯出，您必須安裝 ADO.NET Data Services 3.5 SP1。 如需指示, 請參閱[Install ADO.NET 資料服務以支援 SharePoint 清單的資料摘要匯出](../../../2014/sql-server/install/install-ado-net-data-services-to-support-data-feed-exports-of-sharepoint-lists.md)。  
  
### <a name="create-a-powerpivot-gallery"></a>建立 PowerPivot 圖庫  
 PowerPivot 圖庫是一種文件庫，其中包含用來在 SharePoint 網站上檢視 PowerPivot 活頁簿的預覽和呈現選項。 建議針對它的預覽功能使用 PowerPivot 圖庫來發行及檢視 PowerPivot 活頁簿。 此外，如果您也將 Reporting Services 部署到相同的 SharePoint 伺服器，PowerPivot 圖庫可讓您輕鬆建立報表。 您可以從 PowerPivot 圖庫啟動報表產生器，讓新的報表根據發行的 PowerPivot 活頁簿。 如需建立和使用程式庫的詳細資訊, 請參閱[建立和自訂 Powerpivot 圖庫](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/create-and-customize-power-pivot-gallery)和[使用 powerpivot 圖庫](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/use-power-pivot-gallery)。  
  
### <a name="create-additional-trusted-sites-in-excel-services"></a>在 Excel Services 中建立其他信任的網站  
 您可以在 Excel Services 中加入信任的網站，以便在提供 Excel 活頁簿和 PowerPivot 資料的網站上變更權限和組態設定。 如需相關資訊，請參閱 [Create a trusted location for PowerPivot sites in Central Administration](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/create-a-trusted-location-for-power-pivot-sites-in-central-administration)。  
  
### <a name="tune-configuration-settings"></a>微調組態設定  
 PowerPivot 服務應用程式是使用預設屬性和值所建立。 您可以修改個別服務應用程式的組態設定，以變更配置要求所依據的方法、設定伺服器逾時、變更查詢回應報告事件的臨界值，或是指定保留使用量資料的時間長度。 如需有關 [管理中心] 或有關在 SharePoint Web 應用程式中使用 PowerPivot 功能之設定的詳細資訊, 請參閱[管理中心的 Powerpivot 伺服器管理和](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration)設定。  
  
### <a name="install-powerpivot-for-excel-and-build-a-powerpivot-workbook"></a>安裝 PowerPivot for Excel 及建立 PowerPivot 活頁簿  
 當您在伺服陣列中安裝了伺服器元件之後，您可以先建立使用內嵌 PowerPivot 資料的第一本 Excel 2010 活頁簿，然後將它發行到 Web 應用程式中的 SharePoint 文件庫。 在您可以建立包含 PowerPivot 資料的 Excel 活頁簿之前，您必須先從安裝 Excel 2010 開始，隨後安裝 PowerPivot for Excel 增益集來擴充 Excel，以支援 PowerPivot 資料匯入和豐富性。  
  
### <a name="add-servers-or-applications"></a>加入伺服器或應用程式  
 當您部署 PowerPivot 方案時，將會在網站集合層級針對 Web 應用程式中的所有網站集合啟用功能整合。 當您經過一段時間建立新的 Web 應用程式時，您必須將 powerpivotwebapp 方案部署到每一個應用程式。 如需指示, 請參閱[將 PowerPivot 方案部署到 SharePoint](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/deploy-power-pivot-solutions-to-sharepoint)。  
  
 根據您設定 PowerPivot 服務應用程式的方式而定，PowerPivot 系統服務將會加入到預設連接群組，將它提供給使用預設連接的所有 Web 應用程式使用。 但是，如果您已設定 Web 應用程式使用自訂服務應用程式連接清單，您需要將 PowerPivot 服務應用程式加入到您想要啟用 PowerPivot 資料處理的每一個 SharePoint Web 應用程式。 如需詳細資訊, 請參閱[在管理中心將 PowerPivot 服務應用程式連接到 SharePoint Web 應用程式](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/connect-power-pivot-service-app-to-sharepoint-web-app-in-ca)。  
  
 一段時間之後，如果您判斷需要額外的資料儲存和處理功能，您可以將另一個 PowerPivot for SharePoint 伺服器執行個體加入到伺服器陣列中。 其安裝程序與您加入第一部伺服器的步驟相同，唯一例外的是您指定執行個體名稱和服務帳戶資訊的需求會不同。 如需指示, [請參閱部署檢查清單:將 PowerPivot 服務器加入至 SharePoint 2010 伺服器](../../../2014/sql-server/install/deployment-checklist-scale-out-adding-powerpivot-servers-sharepoint-2010-farm.md)陣列, 以相應放大。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 2014 版本所支援的功能](../../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)   
 [設定 PowerPivot 服務帳戶](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/configure-power-pivot-service-accounts)   
 [在管理中心建立和設定 PowerPivot 服務應用程式](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/create-and-configure-power-pivot-service-application-in-ca)   
 [將 PowerPivot 方案部署到 SharePoint](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/deploy-power-pivot-solutions-to-sharepoint)   
 [為在 [管理中心] 的 網站集合啟用 PowerPivot 功能整合](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/activate-power-pivot-integration-for-site-collections-in-ca)   
 [PowerPivot for SharePoint 2010 安裝](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)  
  
  
