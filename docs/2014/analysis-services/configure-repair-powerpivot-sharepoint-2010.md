---
title: 設定或修復 PowerPivot for SharePoint 2010 （PowerPivot 組態工具） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: d61f49c5-efaa-4455-98f2-8c293fa50046
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 350aadcdd44dcc4424b94792286a7421e2613b2e
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66087391"
---
# <a name="configure-or-repair-powerpivot-for-sharepoint-2010-powerpivot-configuration-tool"></a>設定或修復 PowerPivot for SharePoint 2010 (PowerPivot 組態工具)
  若要設定或修復 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] PowerPivot for SharePoint 2010 的安裝，請使用 PowerPivot 組態工具。 此組態工具一開始先掃描系統，然後傳回完成或修復安裝所需的動作清單。 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 安裝精靈會安裝適用於 SharePoint 2010 的 PowerPivot 組態工具，以及適用於 SharePoint 2013 的 PowerPivot 組態工具。 本主題描述適用於 SharePoint 2010 的 PowerPivot 組態工具。 如需有關 SharePoint 2010 的詳細資訊，請參閱 <<c0> [ 設定或修復 PowerPivot for SharePoint 2013 &#40;PowerPivot 組態工具&#41;](power-pivot-sharepoint/configure-or-repair-power-pivot-for-sharepoint-2013.md)。</c0>  
  
 **[!INCLUDE[applies](../includes/applies-md.md)]**  SharePoint 2010  
  
 
  
##  <a name="bkmk_before"></a> 開始之前  
 PowerPivot for SharePoint 組態工具會掃描程式檔案、登錄設定和可用的通訊埠。 若要充分利用這些工具，請檢閱下列各項。  
  
-   執行＜ [PowerPivot Configuration Tools](power-pivot-sharepoint/power-pivot-configuration-tools.md)＞組態工具的一般需求。  
  
-   PowerPivot for SharePoint 2010 需要針對傳統模式驗證設定的 Web 應用程式。 如果 PowerPivot for SharePoint 2010 組態工具自動建立應用程式，則應用程式會針對傳統模式進行設定。  
  
-   通訊埠 80 必須可用，其中一項選取的工作才會要求組態工具建立及設定 Web 應用程式。  
  
##  <a name="bkmk_using"></a> 使用 PowerPivot 組態工具  
 此工具的第一頁提供用於設定 SharePoint 伺服器陣列的輸入值摘要。 除了您提供的輸入值之外，也會使用預設值來設定系統。 預設名稱用於服務應用程式、服務應用程式資料庫和服務應用程式屬性。  
  
> [!TIP]  
>  如果 PowerPivot 組態工具掃描電腦並於左側窗格傳回空白的工作清單，表示不需要設定任何功能或進行設定。 若要修改 SharePoint 或 PowerPivot 組態，請使用 Windows PowerShell 或 SharePoint 管理中心的管理頁面。 如需詳細資訊，請參閱 <<c0> [ 管理中心的 PowerPivot 伺服器管理和組態](power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md)。  
  
 服務帳戶的值可用於多個服務。 例如，PowerPivot 組態工具使用第一頁上的預設帳戶來設定所有應用程式集區識別。 您可以稍後透過在管理中心修改服務應用程式屬性，變更這些帳戶。  
  
-   在 PowerPivot for SharePoint 2010 組態工具中，這項規則的例外狀況是 Analysis Services 服務帳戶。 此帳戶是在安裝期間指定，而且您會在 **[在本機伺服器上註冊 SQL Server Analysis Services (PowerPivot)]** 動作中提供此帳戶的密碼。 摘要頁面未包含用於此密碼的欄位，因此請務必在該動作的頁面中輸入此密碼。  
  
 此工具提供索引標籤式介面，其中包含參數輸入、Windows PowerShell 指令碼和狀態訊息。  
  
 PowerPivot 組態工具會使用 Windows PowerShell 設定伺服器。 您可以按一下 **[指令碼]** 索引標籤檢閱 Windows PowerShell 指令碼。  
  
 ![組態工具使用者介面](media/ssas-pctui.gif "組態工具使用者介面")  
  
##  <a name="bkmk_steps"></a> 組態步驟  
 只有在本機伺服器上安裝了 PowerPivot for SharePoint 2010 時，才看得見組態工具的連結。  
  
1.  指向 **[開始]** 功能表上的 **[所有程式]**，按一下 [ [!INCLUDE[ssCurrentUI](../includes/sscurrentui-md.md)]]，然後按一下 **[組態工具]**，再按一下 **[PowerPivot 組態工具]**。  
  
2.  按一下 **[設定或修復 PowerPivot for SharePoint]**。  
  
3.  將視窗展開為全螢幕。 您應該會在視窗底部看到一個按鈕列，其中包含 **[驗證]**、 **[執行]** 和 **[結束]** 命令。  
  
4.  **預設帳戶：** 在 參數 索引標籤中，輸入 網域使用者帳戶**預設帳戶使用者名稱**。 此帳戶會用來佈建主要服務，包括 PowerPivot 服務應用程式集區。 請勿指定內建帳戶，例如 Network Service 或 Local System。 此工具會封鎖指定內建帳戶的組態。  
  
     **複雜密碼** ：輸入複雜密碼。 對於新的 SharePoint 伺服器陣列，複雜密碼是在新的伺服器或應用程式加入至 SharePoint 伺服器陣列時使用。 如果是現有的伺服器陣列，則輸入可讓您將伺服器應用程式加入至該伺服器陣列的複雜密碼。  
  
5.  **連接埠：** 選擇性地輸入連接埠號碼連線至管理中心 web 應用程式，或使用提供的隨機產生的編號。 組態工具會先檢查這個編號是否可以使用，然後再提供它當做選項。  
  
6.  按一下 **[在本機伺服器上註冊 SQL Server Analysis Services (PowerPivot)]**。  
  
     指定 Analysis Services 服務帳戶的密碼。  
  
7.  (選擇性) 檢閱用來完成每個動作的其餘輸入值。 如需有關每個的詳細資訊，請參閱本主題中的 [用於設定伺服器的輸入值](#bkmk_input) 。  
  
8.  選擇性地移除您不想處理的任何動作。 例如，如果您想要在稍後設定 Secure Store Service，請按一下 **[設定 Secure Store Service]**，然後清除 **[在工作清單中包含這個動作]** 核取方塊。  
  
9. 按一下 **[驗證]** ，檢查此工具是否有足夠的資訊來處理清單中的動作。  
  
    > [!NOTE]  
    >  如果發生伺服器陣列組態錯誤，這可能是因為未安裝 SharePoint 2010 Server SP1。  
  
10. 按一下 **[執行]** ，處理工作清單中的所有動作。 在您驗證動作之後， **[執行]** 按鈕便會啟用。 如果 **[執行]** 未啟用，請先按一下 **[驗證]** 。  
  
11. [Verify a PowerPivot for SharePoint Installation](instances/install-windows/verify-a-power-pivot-for-sharepoint-installation.md)：  
  
##  <a name="bkmk_input"></a> 用於設定伺服器的輸入值  
 PowerPivot 組態工具會使用輸入值 (您所輸入) 以及預設值 (它偵測到或自動使用) 的組合。  
  
 組態工具中列出的動作清單取決於 SharePoint 伺服器陣列目前的組態。 例如，如果已設定 SharePoint 伺服器陣列，則工具中不會列出任何動作。 您可以隨時執行工具以設定、修復或偵測組態錯誤。 如果必要服務 (例如 Excel Services 或 Secure Store Service) 未在伺服器陣列中執行，此工具會偵測遺漏的服務並且提供用於啟用這些服務的選項。 如果無需執行任何動作，則工作清單將是空的。  
  
 下表說明用於設定伺服器的值。  
  
|頁面|輸入值|`Source`|描述|  
|----------|-----------------|------------|-----------------|  
|**設定或修復 PowerPivot for SharePoint**|預設帳戶|目前使用者|預設帳戶是用於在伺服器陣列中佈建共用服務的網域 Windows 使用者帳戶。 此帳戶用於佈建 PowerPivot 服務應用程式、Secure Store Service、Excel Services、Web 應用程式集區識別、網站集合管理員和 PowerPivot 無人看管的資料重新整理帳戶。<br /><br /> 根據預設，工具會輸入目前使用者的網域帳戶。 除非伺服器是設定做為評估之用，否則應該以其他網域使用者帳戶取代此預設帳戶。<br /><br /> 您之後也可以使用管理中心變更服務識別。<br /><br /> 您可以選擇在 PowerPivot 組態工具中為下列項目指定專用帳戶：<br /><br /> Web 應用程式，使用 **[建立預設 Web 應用程式]** 頁面 (假設此工具正在為伺服器陣列建立 Web 應用程式)。<br /><br /> PowerPivot 無人看管的資料重新整理帳戶，使用此工具中的 **[建立無人看管的資料重新整理帳戶]** 頁面。|  
||資料庫伺服器|本機 PowerPivot 具名執行個體 (如果有的話)|如果資料庫引擎執行個體安裝為 PowerPivot 具名執行個體，此工具會使用此執行個體擴展資料庫伺服器欄位。 如果您沒有安裝資料庫引擎，此欄位是空的。 您必須提供執行個體。 此執行個體可以是 SharePoint 伺服器陣列所支援的任何 SQL Server 版本或版別。|  
||複雜密碼|使用者輸入|如果您要建立新的伺服器陣列，您所輸入的複雜密碼將是此伺服器陣列的複雜密碼。 如果您要將 PowerPivot for SharePoint 加入至現有的伺服器陣列，則必須提供在建立時為此伺服器陣列定義的複雜密碼。|  
||SharePoint 管理中心通訊埠|預設值 (如果需要)|如果未設定伺服器陣列，則此工具會提供用於建立伺服器陣列的選項，包括指向管理中心的 HTTP 端點。 它預設為未使用的隨機產生通訊埠編號。|  
|**設定新伺服器陣列**|資料庫伺服器<br /><br /> 伺服器陣列帳戶<br /><br /> 複雜密碼<br /><br /> SharePoint 管理中心通訊埠|預設值 (如果需要)|設定會預設為您在主頁面中輸入的內容。|  
|**設定本機服務執行個體**|Analysis Services 服務帳戶密碼|使用者輸入|您必須在 **[在本機伺服器上註冊 SQL Server Analysis Services (PowerPivot)]** 頁面中輸入 Analysis Services 服務帳戶的密碼。<br /><br /> 此服務帳戶是在安裝期間指定。 您現在必須輸入密碼，以便向 SharePoint 註冊本機服務執行個體。|  
|**建立 PowerPivot 服務應用程式**|PowerPivot 服務應用程式名稱|預設|預設名稱是「預設的 PowerPivot 服務應用程式」。 您可以在工具中取代為不同的值。|  
||PowerPivot 服務應用程式資料庫伺服器|預設|裝載 PowerPivot 服務應用程式資料庫的資料庫伺服器。 預設伺服器名稱就是用於伺服器陣列的資料庫伺服器。 您可以在工具中取代為不同的值。|  
||PowerPivot 服務應用程式資料庫名稱|預設|預設資料庫名稱以服務應用程式名稱為基礎，後面跟著 GUID，以確保名稱是唯一的。 您可以在工具中取代為不同的值。|  
||升級活頁簿以啟用資料重新整理|使用者輸入|資料重新整理失敗，而且在 SQL Server 2008 R2 PowerPivot 活頁簿中不支援。 **[升級活頁簿以啟用資料重新整理]** 選項會將活頁簿升級為 SQL Server 2012 PowerPivot 版。|  
|**建立預設 Web 應用程式**|Web 應用程式名稱|預設值 (如果需要)|如果沒有任何 Web 應用程式，此工具會建立一個。 Web 應用程式將針對傳統模式驗證設定，並且在 **通訊埠 80**上接聽。 上傳檔案大小上限設為 2047 MB，這是 SharePoint 所允許的最大值。 較大的檔案上傳大小在於容納大型 PowerPivot 檔案。|  
||URL|預設值 (如果需要)|此工具會根據伺服器名稱，使用與 SharePoint 相同的檔案命名慣例來建立 URL。|  
||Web 應用程式集區|預設值 (如果需要)|此工具會在 IIS 中建立預設應用程式集區。|  
||Web 應用程式集區帳戶和密碼|預設值 (如果需要)|應用程式集區帳戶以預設帳戶為基礎，但您可以在工具中覆寫它。|  
||Web 應用程式資料庫伺服器|預設值 (如果需要)|將預先選取預設資料庫執行個體以儲存應用程式資料庫，但您可以在此工具中指定不同的 SQL Server 執行個體。|  
||Web 應用程式資料庫名稱|預設值 (如果需要)|資料庫名稱以 SharePoint 的檔案命名慣例為基礎，但您可以選擇其他名稱。|  
|**部署 Web 應用程式方案**|URL|預設值 (如果需要)|[預設 URL] 是來自預設 Web 應用程式。|  
||檔案大小上限 (MB)|預設值 (如果需要)|預設值是 2047。 SharePoint 文件庫也有大小上限，而 PowerPivot 設定不應超過文件庫設定。 如需詳細資訊，請參閱 <<c0> [ 設定最大檔案上傳大小 &#40;PowerPivot for SharePoint&#41;](power-pivot-sharepoint/configure-maximum-file-upload-size-power-pivot-for-sharepoint.md)。</c0>|  
|**建立網站集合**|網站管理員|預設值 (如果需要)|此工具使用預設帳戶。 您可以在 **[建立網站集合]** 頁面中覆寫預設帳戶。|  
||連絡人電子郵件|預設值 (如果需要)|如果伺服器上設定了 Microsoft Outlook，此工具會使用目前使用者的電子郵件地址， 否則會使用預留位置值。|  
||網站 URL|預設值 (如果需要)|此工具會使用與 SharePoint 相同的 URL 命名慣例來建立網站 URL。|  
||網站標題|預設值 (如果需要)|此工具會加入 **[PowerPivot 網站]** 做為預設標題。|  
|**啟用網站集合中的 PowerPivot 功能**|網站 URL||您要啟用 PowerPivot 功能之網站集合的 URL。|  
||啟用這個網站的高階功能||啟用 SharePoint 網站功能"PremiumSite"。|  
|**建立 Secure Store Service 應用程式**|服務應用程式名稱||輸入 Secure Store Service 應用程式的名稱。|  
||資料庫伺服器||輸入用於 Secure Store Service 應用程式的資料庫伺服器名稱。|  
|**建立 Secure Store Service 應用程式 Proxy**|服務應用程式名稱||輸入 Secure Store Service 應用程式的名稱。|  
||服務應用程式 Proxy||輸入 Secure Store Service 應用程式 Proxy 的名稱。  這個名稱將顯示在預設連接群組中，藉由群組可以將應用程式與 SharePoint 內容 Web 應用程式產生關聯。|  
|**更新 Secure Store Service 主要金鑰**|服務應用程式 Proxy||輸入 Secure Store Service 應用程式 Proxy 的名稱|  
||複雜密碼||主要金鑰會用於資料加密。 根據預設，用來產生金鑰的複雜密碼與用來在伺服器陣列中佈建新伺器所用的複雜密碼相同。 您可以用唯一的複雜密碼取代預設複雜密碼。|  
|**建立無人看管的帳戶**|目標應用程式識別碼||應用程式識別碼可以是描述性文字。|  
||目標應用程式的易記名稱|||  
||無人看管帳戶的使用者名稱和密碼||輸入由目標應用程式所使用且用來執行無人看管之資料重新整理的 Windows 使用者帳戶認證。|  
||網站 URL||輸入與目標應用程式相關聯之網站集合的網站 URL。 若要與其他網站集合產生關聯，請使用 SharePoint 管理中心。|  
|**建立 Excel Services 服務應用程式**|服務應用程式名稱||輸入服務應用程式名稱。 在 SharePoint 伺服器陣列的資料庫伺服器上，會建立具有相同名稱的服務應用程式資料庫。|  
|**加入 MSOLAP.5 做為受信任的提供者**|服務應用程式名稱||SharePoint 2010 中的 Excel Services 會使用 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] OLE DB 提供者連接 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料。 這個步驟會將隨 PowerPivot for SharePoint 一起安裝的 OLE DB 提供者版本做為受信任的提供者加入 Excel Services 中。|  
||PowerPivot 伺服器名稱|||  
|||||  
  
 如果 PowerPivot 組態工具建立伺服器陣列，它會使用與 SharePoint 相同的檔案命名慣例，在資料庫伺服器上建立必要資料庫。 您無法變更伺服器陣列資料庫名稱。  
  
 如果工具建立網站集合，它會使用與 SharePoint 相同的檔案命名慣例，在資料庫伺服器上建立內容資料庫。 您無法變更內容資料庫名稱。  
  
##  <a name="bkmk_nextsteps"></a> 後續步驟  
 完成伺服器安裝之後，有幾個您應該執行的後置安裝工作：  
  
-   授與 SharePoint 權限給個人與群組。 若要存取網站及內容，這是必要的工作。  
  
-   變更服務應用程式集區識別，以不同的帳戶執行。 為服務和應用程式指定不同的識別是 SharePoint 對於安全部署的最佳作法建議。  
  
-   在 Excel Services 中建立其他信任的網站，讓您可以變更最適合 PowerPivot 資料存取權限和組態設定。  
  
-   安裝 ADO.NET Data Services 3.5 SP1 來啟用從 SharePoint 清單匯出的資料摘要。  
  
-   安裝常用的資料提供者，以啟用伺服器端資料重新整理。  
  
-   下載 PowerPivot 撰寫工具到工作站電腦上，以建立 PowerPivot 活頁簿，然後將其發行至 SharePoint。 安裝工具與發行 PowerPivot 活頁簿會透過確認您剛才安裝之伺服器元件的互通性來完成安裝程序。  
  
### <a name="grant-sharepoint-permissions-to-workbook-users"></a>將 SharePoint 權限授與活頁簿使用者  
 使用者需要有 SharePoint 權限，才能發行或檢視活頁簿。 請務必將 **[檢視]** 權限授與給需要檢視已發行之活頁簿的使用者，並將 **[參與]** 權限授與給發行或管理活頁簿的使用者。 您必須是網站集合管理員，才能授與權限。  
  
1.  在網站中，按一下 **[網站動作]**。  
  
2.  按一下 **[網站權限]**。  
  
3.  如果您希望其中一組使用者具有 **[參與]** 權限，而另一個使用者群組只有 **[檢視]** 權限，則視需要建立群組。  
  
4.  輸入應該擁有群組成員資格的 Windows 網域使用者或群組帳戶。 如同上面所述，如果應用程式有設定傳統驗證，請勿使用電子郵件地址或通訊群組。  
  
### <a name="install-adonet-data-services-35-sp1"></a>安裝 ADO.NET Data Services 3.5 SP1  
 從 SharePoint 清單匯出資料摘要需要 ADO.NET Data Services。 SharePoint 2010 不會在 PrerequisiteInstaller 程式中包含這個元件，所以您必須手動安裝它。  
  
1.  移至 SharePoint 2010 的硬體和軟體需求文件集： [判斷硬體和軟體需求 (SharePoint 2010)](https://go.microsoft.com/fwlink/?LinkId=169734)  
  
2.  在 [Installing software prerequisites] 中，尋找對應到您所使用之作業系統的 ADO.NET Data Services 3.5 連結。  
  
3.  按一下該連結，並執行安裝程式來安裝服務。  
  
### <a name="install-data-providers-used-in-data-refresh-and-check-user-permissions"></a>安裝資料重新整理中使用的資料提供者並檢查使用者權限  
 伺服器端資料重新整理可讓使用者以自動安裝模式將更新的資料重新匯入其活頁簿中。 為了讓資料重新整理成功，伺服器必須擁有原先用來匯入資料的同一個資料提供者。 此外，用來執行資料重新整理的使用者帳戶經常會需要外部資料來源的讀取權限。 請您務必檢查啟用和設定資料重新整理的需求，以確保獲得成功的結果。 如需詳細資訊，請參閱 < [PowerPivot Data Refresh with SharePoint 2010](powerpivot-data-refresh-with-sharepoint-2010.md)。  
  
### <a name="change-application-pool-and-service-identities-in-sharepoint"></a>在 SharePoint 中變更應用程式集區和服務識別  
 PowerPivot 組態工具會提供在單一帳戶之下執行的伺服器陣列功能、應用程式和服務。 這樣會簡化安裝，但是不會產生一個符合 SharePoint 伺服陣列安全性需求的部署。 若要建立更強固的部署，請變更應用程式集區和服務識別，使其在安裝完成之後於不同的帳戶之下執行。 如需詳細資訊，請參閱 <<c0> [ 設定 PowerPivot 服務帳戶](power-pivot-sharepoint/configure-power-pivot-service-accounts.md)。  
  
### <a name="create-additional-trusted-sites-in-excel-services"></a>在 Excel Services 中建立其他信任的網站  
 您可以在 Excel Services 中加入信任的網站，以便在提供 Excel 活頁簿和 PowerPivot 資料的網站上變更權限和組態設定。 如需相關資訊，請參閱 [在管理中心建立 PowerPivot 網站的信任位置](power-pivot-sharepoint/create-a-trusted-location-for-power-pivot-sites-in-central-administration.md)。  
  
### <a name="add-servers-or-applications"></a>加入伺服器或應用程式  
 一段時間之後，如果您判斷需要額外的資料儲存和處理功能，您可以將另一個 PowerPivot for SharePoint 伺服器執行個體加入到伺服器陣列中。 如需指示，請參閱[部署檢查清單：藉由將 PowerPivot 伺服器加入至 SharePoint 2010 伺服器陣列的向外](../../2014/sql-server/install/deployment-checklist-scale-out-adding-powerpivot-servers-sharepoint-2010-farm.md)。  
  
## <a name="additional-resources"></a>其他資源  
 ![SharePoint 設定](media/as-sharepoint2013-settings-gear.gif "SharePoint 設定")[透過 Microsoft SQL Server Connect 提交意見與連絡資訊](https://connect.microsoft.com/SQLServer/Feedback)(https://connect.microsoft.com/SQLServer/Feedback)。  
  
## <a name="see-also"></a>另請參閱  
 [PowerPivot 組態工具](power-pivot-sharepoint/power-pivot-configuration-tools.md)   
 [管理中心的 PowerPivot 伺服器管理和設定](power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md)  
  
  
