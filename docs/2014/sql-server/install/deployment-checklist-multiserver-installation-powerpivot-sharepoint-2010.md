---
title: 部署檢查清單： Powerpivot for SharePoint 2010 的多伺服器安裝 |Microsoft 文件
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 4380040a-1368-4a47-8930-47c65a192e59
caps.latest.revision: 17
author: markingmyname
ms.author: maghan
manager: jhubbard
ms.openlocfilehash: 9d8fbfc04e3f0ae0e16ae55d3730667c60e0d323
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36032703"
---
# <a name="deployment-checklist-multi-server-installation-of-powerpivot-for-sharepoint-2010"></a>部署檢查清單：PowerPivot for SharePoint 2010 的多伺服器安裝
  這份檢查清單會引導您逐步完成新增[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]從頭建立向上三層式 SharePoint 2010 伺服陣列的 sharepoint。 三層伺服陣列包含資料庫、應用程式和 Web 層。 加入[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]此拓撲會要求您執行 SQL Server 安裝程式安裝[!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]應用程式層上。 當您部署 web 應用程式方案時，PowerPivot 程式檔案會加入至 web 層，而只會做為後續安裝工作。 即使有部署步驟，但是在您需要執行的 Web 層或資料層並沒有個別的安裝步驟。 正在安裝您要執行的唯一安裝步驟[!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]應用程式伺服器上。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2010|  
  
  
  
## <a name="prerequisites"></a>必要條件  
 您必須是本機系統管理員，才能安裝 SQL Server 和 SharePoint 2010。  
  
 安裝 SharePoint 的人員也必須設定伺服器陣列。 若要設定伺服陣列，您必須擁有資料庫伺服器的 SQL Server 登入。 登入必須指派給下列角色：`dbcreator`、`securityadmin` 及 `public`。  
  
 您必須擁有 SharePoint Server 2010 Enterprise 或 Enterprise Evaluation Edition。  
  
 電腦必須加入網域。  
  
 您必須知道將用來執行 Database Engine、伺服器陣列中之服務，以及 SharePoint 整合模式下之 Analysis Services 的帳戶。 雖然您可以稍後變更這些帳戶，不過將在安裝期間第一次指定它們。  
  
 您在安裝期間所指定的服務帳戶必須是網域使用者帳戶。  
  
 開始安裝之前，請檢查您的瀏覽器設定以確認您擁有網際網路連線。 必要條件安裝程式會開啟網際網路連線以下載所需的軟體。 您應該進行下列變更以確保您取得所有需要的軟體：  
  
-   在「伺服器管理員」中，暫時停用 [Internet Explorer 增強式安全性設定] 以允許下載至伺服器。 為下載所需的軟體，您可以僅針對系統管理員關閉 IE ESC。  
  
-   在 Internet Explorer 中，您可能也需要將瀏覽器設定為略過 Proxy 伺服器以允許 localhost 存取網際網路 URL。  
  
    1.  在 Internet Explorer 的 [工具] 功能表中，按一下 [網際網路選項]。  
  
    2.  在 [連線] 索引標籤的 [區域網路 (LAN) 設定] 區域中，按一下 [區域網路設定]。  
  
    3.  在 [自動設定] 區域中，清除 [自動偵測設定] 核取方塊。  
  
    4.  在 [Proxy 伺服器] 區域中，選取 [在您的區域網路使用 Proxy 伺服器] 核取方塊。  
  
    5.  在 [位址] 方塊中輸入 Proxy 伺服器的位址。  
  
    6.  在 [連接埠] 方塊中輸入 Proxy 伺服器的通訊埠編號。  
  
    7.  選取 [近端網址不使用 Proxy] 核取方塊。  
  
    8.  按一下 [確定]，關閉 [區域網路 (LAN) 設定] 對話方塊。  
  
    9. 按一下 [確定] 關閉 [網際網路選項] 對話方塊。  
  
##  <a name="installdb"></a> 安裝資料庫伺服器  
 本主題假設您的伺服器陣列拓撲為基礎文件所述的一個[三層式伺服器陣列的多部伺服器](http://go.microsoft.com/fwlink/?LinkId=182771)。 如果您已經有可運作的伺服器陣列時，跳到[安裝 PowerPivot for SharePoint](#installppapp)。  
  
 如果您剛要開始使用拓撲，請從安裝 SQL Server Database Engine 開始。 這些指示會導致 SharePoint 伺服器可以在伺服陣列中存取的資料庫伺服器。  
  
1.  在您使用的資料庫伺服器的電腦，執行 SQL Server 安裝程式安裝 SQL Server Database Engine (請參閱[從安裝精靈安裝 SQL Server 2014&#40;安裝&#41;](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md))。  
  
     選取要安裝的功能之後，選擇下列各項：  
  
    -   Database Engine 服務  
  
    -   用戶端工具連接性  
  
    -   管理工具 - 完整 (基本功能將會自動隨附)  
  
2.  安裝 Database Engine 後，為遠端連線啟用 TCP/IP，然後重新啟動服務：  
  
    1.  啟動 SQL Server 組態管理員。  
  
    2.  開啟 SQL Server 網路組態。  
  
    3.  選取 [MSSQLSERVER 的通訊協定] 。  
  
    4.  以滑鼠右鍵按一下**TCP/IP**選取**啟用**。  
  
    5.  按一下**SQL Server 服務**。  
  
    6.  以滑鼠右鍵按一下**SQL Server (MSSQLSERVER)**，然後按一下**重新啟動**。  
  
3.  透過 Windows 防火牆啟用對資料庫伺服器的傳入存取。 這可讓伺服陣列中的 SharePoint 伺服器連接至 SharePoint 資料庫。 如需詳細資訊，請參閱 [設定 Windows 防火牆以允許 SQL Server 存取](../../../2014/sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)。  
  
    1.  在 Windows 控制台中，系統管理工具 中按一下**具有進階安全性的 Windows 防火牆**。  
  
    2.  按一下**輸入規則**。  
  
    3.  按一下**新規則**。  
  
    4.  在 [規則類型] 中按一下**自訂**。  
  
    5.  按 [下一步] 。  
  
    6.  在 程式 的 服務 區段中，按一下 **自訂**。  
  
    7.  按一下**套用至此服務**。  
  
    8.  選取**SQL Server (MSSQLSERVER)** 您安裝 SQL Server 的預設執行個體，然後再按一下**確定**。  
  
    9. 按 [下一步] 。  
  
    10. 在通訊協定及連接埠，接受預設值，然後按一下**下一步**。  
  
    11. 在範圍內，接受預設值，然後按一下**下一步**。  
  
    12. 在動作中，接受預設值，然後按一下**下一步**。  
  
    13. 在設定檔，清除核取方塊**私人**和**公用**，然後按一下 **下一步**。  
  
    14. 在 名稱 輸入 輸入規則的描述性名稱 (例如， **SQL Server**)。  
  
    15. 按一下 **[完成]**。  
  
##  <a name="installsp"></a> 安裝及設定三層式 SharePoint 2010 伺服陣列  
 在您要當做 SharePoint 伺服器使用的每部電腦上，執行 SharePoint 必要條件安裝程式，然後再執行 SharePoint Server 安裝程式。  
  
 使用 SharePoint 2010 文件集中的下列指示，安裝及設定包含兩個 Web 伺服器與一個應用程式伺服器的 SharePoint 2010 伺服器陣列：  
  
 [多部伺服器的三層式伺服器陣列 (SharePoint Server 2010)](http://go.microsoft.com/fwlink/?LinkId=182771)  
  
 當系統要求您指定資料庫伺服器時，請指定您稍早安裝的資料庫伺服器。  
  
 在下列程序中，假設您使用三層伺服器陣列設定所提供的指示，設定伺服器陣列。 伺服器陣列應包含下列服務和功能：  
  
-   Excel Services、搜尋服務與 Secure Store Service  
  
-   Web 應用程式和網站集合  
  
-   使用量和健全資料收集  
  
-   診斷記錄  
  
##  <a name="installppapp"></a> 應用程式伺服器上安裝 PowerPivot for SharePoint  
 執行 SQL Server 安裝程式，將 PowerPivot for SharePoint 加入至 SharePoint 伺服器陣列。 如果此伺服器陣列是由多部 SharePoint 伺服器所組成，您必須在已經加入此伺服器陣列的應用程式伺服器上執行 SQL Server 安裝程式。  
  
 一律在應用程式伺服器上安裝 PowerPivot for SharePoint。 雖然 Web 前端伺服器也會執行 PowerPivot for SharePoint 伺服器元件，但是在 Web 前端執行的元件會在 PowerPivot for SharePoint 組態步驟中安裝 (在伺服器陣列中部署方案時)。 如需安裝程式的詳細資訊，請參閱[安裝 PowerPivot for SharePoint 2010](../../../2014/sql-server/install/install-powerpivot-for-sharepoint-2010.md)。  
  
 如果您的部署拓撲需要兩個 PowerPivot for SharePoint 執行個體，請在每部應用程式伺服器上執行 SQL Server 安裝程式。 單一電腦上只能有一個 PowerPivot for SharePoint 執行個體。 如果需要多個執行個體，則必須使用其他伺服器。 如需有關如何將多個 PowerPivot for SharePoint 伺服器加入至相同的伺服陣列的詳細資訊，請參閱[部署檢查清單： 將 PowerPivot 伺服器加入至 SharePoint 2010 伺服陣列的向外](../../../2014/sql-server/install/deployment-checklist-scale-out-adding-powerpivot-servers-sharepoint-2010-farm.md)。  
  
##  <a name="installclientlib"></a> 並沒有安裝 PowerPivot for SharePoint 的 SharePoint 應用程式伺服器上安裝 Analysis Services 用戶端程式庫  
 如果某個伺服器陣列拓撲包含執行下列應用程式的 Web 前端或應用程式伺服器，但是並未在同一部電腦上安裝 PowerPivot for SharePoint，則需要使用其他軟體才能支援 PowerPivot 資料存取和功能：  
  
-   Excel Services 或 PerformancePoint Services  
  
-   在自己的伺服器上當做獨立應用程式執行的管理中心  
  
 Excel Services 和 PerformancePoint Services 都需要較新版的 Analysis Services OLE DB 提供者才能支援 PowerPivot 資料存取。 如果您在沒有最新版 OLE DB 提供者的電腦上執行任何一種應用程式，就必須手動安裝提供者。 如需詳細資訊，請參閱[SharePoint 伺服器上安裝 Analysis Services OLE DB 提供者](../../../2014/sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md)  
  
 同樣地，如果某部電腦只有管理中心，但是並未在同一部電腦上安裝 PowerPivot for SharePoint，則需要 ADOMD.NET 用戶端程式庫。 PowerPivot 管理儀表板會使用此程式庫來存取擴展儀表板所用的內部資料。 如需詳細資訊，請參閱 [在執行管理中心的 Web 前端伺服器上安裝 ADOMD.NET](../../../2014/sql-server/install/install-adomd-net-on-web-front-end-servers-running-central-administration.md)。  
  
##  <a name="configsrvr"></a> 設定伺服器  
 您可以使用 PowerPivot 組態工具來設定 PowerPivot for SharePoint。 此工具會掃描伺服器陣列的現有組態，並提供安裝或啟用 PowerPivot for SharePoint 所需之 SharePoint 功能的選項。 在此步驟中，會啟動「對 Windows Token 服務的宣告」。 此外，如果尚未啟用其他必要的 SharePoint 功能，組態工具會將這些功能加入清單，並加入啟用功能的動作。  
  
 如需詳細資訊，請參閱[設定或修復 PowerPivot for SharePoint 2010 &#40;PowerPivot 組態工具&#41;](../../../2014/analysis-services/configure-repair-powerpivot-sharepoint-2010.md)。  
  
##  <a name="AAM"></a> 設定 Web 前端伺服器的備用存取對應  
 若要確認 PowerPivot 資料存取或資料重新整理的要求是由每部 Web 前端伺服器所處理，您必須將每部伺服器的不同 URL 對應到相同的 Web 應用程式。  
  
1.  在 管理中心 應用程式管理 中按一下**設定備用存取對應**。  
  
2.  在 [備用存取對應集合] 中，選取您的 Web 應用程式。  
  
3.  按一下**新增內部 URL**。  
  
4.  指定第一部 Web 前端伺服器的 URL。  
  
5.  重複先前的步驟，加入第二部 Web 前端伺服器的 URL。  
  
##  <a name="activatePP"></a> 為網站集合啟用 PowerPivot 功能整合  
 網站集合層級的功能啟用可以將應用程式頁面和範本提供給網站使用，包括排程資料重新整理的組態頁面，以及 PowerPivot 圖庫和資料摘要文件庫的應用程式頁面。  
  
 PowerPivot 組態工具會為您指定的網站集合啟用功能整合。 您可以多次執行工具，以選取其他網站集合。 或者，網站管理員可以從 SharePoint 中設定功能啟用。 如需詳細資訊，請參閱[在管理中心為網站集合啟用 PowerPivot 功能整合](../../analysis-services/power-pivot-sharepoint/activate-power-pivot-integration-for-site-collections-in-ca.md)。  
  
##  <a name="verify"></a> 驗證整合與伺服器的可用性  
 當使用者或應用程式開啟含有 PowerPivot 資料的 Excel 活頁簿時，就會在伺服陣列中進行 PowerPivot 查詢處理。 您至少可以檢查 SharePoint 網站上的頁面，以確認 PowerPivot 功能是可用的。 但是，為了完整確認安裝作業，您必須擁有可以發行到 SharePoint 並從文件庫存取的 PowerPivot 活頁簿。 為了測試用途，您可以發行已經包含 PowerPivot 資料的範例活頁簿，並用它來確認 SharePoint 整合已正確設定。  
  
 若要確認 PowerPivot 可與 SharePoint 網站整合，請執行下列動作：  
  
1.  在瀏覽器中，開啟您建立的 Web 應用程式。 如果您使用預設值，您可以指定 http://\<您的電腦名稱 > 中的 URL 位址。  
  
2.  確認應用程式中可以使用 PowerPivot 資料存取和處理功能。 若要這樣做，您可以確認 PowerPivot 提供的文件庫範本是否存在：  
  
    1.  在 網站動作上按一下**更多選項...**.  
  
    2.  在程式庫，您應該會看到**資料摘要庫**和**PowerPivot 圖庫**。 這些文件庫範本是由 PowerPivot 功能所提供，如果此功能已正確整合，就可以在文件庫清單中看到這些範本。  
  
 若要在伺服器上確認 PowerPivot 資料存取，請執行以下作業：  
  
1.  [下載](http://go.microsoft.com/fwlink/?LinkID=219108) Reporting Services 教學課程隨附的野餐資料範例。 您將使用此下載中的範例活頁簿確認 PowerPivot 資料存取。 解壓縮檔案。  
  
2.  將 PowerPivot 活頁簿上傳至 PowerPivot 圖庫或任何 SharePoint 文件庫。  
  
3.  按一下文件，從文件庫中加以開啟。  
  
4.  按一下交叉分析篩選器或篩選資料來啟動 PowerPivot 查詢。 伺服器將會在背景載入 PowerPivot 資料，然後傳回結果。 在下一個步驟中，您將會連接到伺服器，並確認已經載入及快取資料。  
  
5.  在 [開始] 功能表中，從 Microsoft SQL Server 2008 R2 程式群組啟動 SQL Server Management Studio。 如果伺服器上未安裝這個工具，您可以跳到最後一個步驟，確認快取檔案存在。  
  
6.  在 [伺服器類型] 中，選取 [Analysis Services]。  
  
7.  在 伺服器名稱輸入**\<伺服器名稱 > \powerpivot**，其中**\<伺服器名稱 >** 是具有 PowerPivot for SharePoint 安裝的電腦名稱。  
  
8.  按一下 **[連接]**。  
  
9. 在 物件總管 中，按一下 **資料庫**，檢視載入的 PowerPivot 資料檔案的清單。  
  
10. 在電腦檔案系統上，檢查下列資料夾來決定檔案是否要快取到磁碟。 快取檔案的存在會進一步驗證您的部署是否可以運作。 若要檢視檔案快取，請移至 \Program Files\Microsoft SQL Server\MSAS10_50.POWERPIVOT\OLAP\Backup 資料夾。  
  
##  <a name="nextsteps"></a> 安裝後步驟  
 在確認安裝之後，請建立 PowerPivot 圖庫或微調個別組態設定來完成服務組態。 若要充分利用剛才安裝的伺服器元件，您可以下載 [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)] 以建立您的第一個 PowerPivot 活頁簿，然後發行。  
  
####  <a name="bkmk_disk"></a> 設定磁碟空間使用量上限  
 您可以設定快取到磁碟之 PowerPivot 資料檔案所能使用的磁碟空間上限。 預設值是使用所有可用的磁碟空間。 如需有關如何限制磁碟空間使用量的指示，請參閱[設定磁碟空間使用量&#40;PowerPivot for SharePoint&#41;](../../analysis-services/power-pivot-sharepoint/configure-disk-space-usage-power-pivot-for-sharepoint.md)。  
  
####  <a name="Upload"></a> 增加 SharePoint Web 應用程式檔案上傳大小上限  
 因為 PowerPivot 活頁簿可能很龐大，所以您可能會想要增加檔案上傳大小上限。 要設定的檔案大小設定有兩個：Web 應用程式的 [最大上傳大小] 以及 Excel Services 中的 [最大活頁簿大小]。 檔案大小上限應該在兩個應用程式中設定為相同的值。 如需指示，請參閱[設定檔案上傳大小上限&#40;PowerPivot for SharePoint&#41;](../../analysis-services/power-pivot-sharepoint/configure-maximum-file-upload-size-power-pivot-for-sharepoint.md)。  
  
#### <a name="grant-sharepoint-permissions-to-workbook-users"></a>將 SharePoint 權限授與活頁簿使用者  
 使用者需要有 SharePoint 權限，才能發行或檢視活頁簿。 務必將授與**檢視**給需要檢視已發行的活頁簿的使用者權限和**參與**給發行或管理活頁簿的使用者權限。 您必須是網站集合管理員，才能授與權限。  
  
1.  在網站中，按一下 **[網站動作]**。  
  
2.  按一下 **[網站權限]**。  
  
3.  選取網站集合的核取方塊**成員**群組。  
  
4.  在功能區中，按一下 **授與權限**。  
  
5.  輸入應該擁有加入或移除文件之權限的 Windows 網域使用者或群組帳戶。  
  
6.  按一下 [確定] 。  
  
7.  選取網站集合的核取方塊**訪客**群組。  
  
8.  在功能區中，按一下 **授與權限**。  
  
9. 輸入應該擁有檢視文件之權限的 Windows 網域使用者或群組帳戶。 如同上面所述，如果應用程式有設定傳統驗證，請勿使用電子郵件地址或通訊群組。  
  
10. 按一下 [確定] 。  
  
#### <a name="install-adonet-data-services-35-sp1"></a>安裝 ADO.NET Data Services 3.5 SP1  
 從 SharePoint 清單匯出資料摘要需要 ADO.NET Data Services。 SharePoint 2010 不會在 PrerequisiteInstaller 程式中包含這個元件，所以您必須手動安裝它。 如需有關如何安裝 ADO.NET Data Services 的詳細資訊，請參閱[安裝 ADO.NET Data Services 以支援資料摘要的 SharePoint 清單匯出](../../../2014/sql-server/install/install-ado-net-data-services-to-support-data-feed-exports-of-sharepoint-lists.md)。  
  
#### <a name="install-data-providers-used-in-data-refresh-and-check-user-permissions"></a>安裝資料重新整理中使用的資料提供者並檢查使用者權限  
 伺服器端資料重新整理可讓使用者以自動安裝模式將更新的資料重新匯入其活頁簿中。 為了讓資料重新整理成功，伺服器必須擁有原先用來匯入資料的同一個資料提供者。 此外，用來執行資料重新整理的使用者帳戶經常會需要外部資料來源的讀取權限。 請您務必檢查啟用和設定資料重新整理的需求，以確保獲得成功的結果。 如需詳細資訊，請參閱[PowerPivot Data Refresh with SharePoint 2010](../../../2014/analysis-services/powerpivot-data-refresh-with-sharepoint-2010.md)。  
  
#### <a name="create-a-powerpivot-gallery"></a>建立 PowerPivot 圖庫  
 PowerPivot 圖庫是一種文件庫，其中包含用來在 SharePoint 網站上檢視 PowerPivot 活頁簿的預覽和呈現選項。 建議針對它的預覽功能使用 PowerPivot 圖庫來發行及檢視 PowerPivot 活頁簿。 此外，如果您也將 Reporting Services 部署到相同的 SharePoint 伺服器，PowerPivot 圖庫可讓您輕鬆建立報表。 您可以從 PowerPivot 圖庫啟動報表產生器，讓新的報表根據發行的 PowerPivot 活頁簿。 如需有關建立和使用程式庫的詳細資訊，請參閱[Create and Customize PowerPivot](../../analysis-services/power-pivot-sharepoint/create-and-customize-power-pivot-gallery.md)和[使用 PowerPivot 圖庫](../../analysis-services/power-pivot-sharepoint/use-power-pivot-gallery.md)。  
  
#### <a name="tune-configuration-settings"></a>微調組態設定  
 PowerPivot 服務應用程式是使用預設屬性和值所建立。 您可以修改個別服務應用程式的組態設定，以變更配置要求所依據的方法、設定伺服器逾時、變更查詢回應報告事件的臨界值，或是指定保留使用量資料的時間長度。 如需有關在 [管理中心] 的組態或 SharePoint Web 應用程式中使用 PowerPivot 功能的詳細資訊，請參閱[管理中心的 PowerPivot 伺服器管理和組態](../../analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 2012 版本支援的功能](http://go.microsoft.com/fwlink/?linkid=232473)   
 [安裝 PowerPivot for SharePoint 2010](../../../2014/sql-server/install/install-powerpivot-for-sharepoint-2010.md)   
 [部署檢查清單： 向外延展至 SharePoint 2010 伺服器陣列加入 PowerPivot 伺服器](../../../2014/sql-server/install/deployment-checklist-scale-out-adding-powerpivot-servers-sharepoint-2010-farm.md)  
  
  