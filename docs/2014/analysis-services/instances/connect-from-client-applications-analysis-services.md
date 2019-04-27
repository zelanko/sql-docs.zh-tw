---
title: 連接用戶端應用程式 (Analysis Services) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: b1e0f1d4-0b87-4ad3-8172-f746fe2f16a2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bd6264834efbafe65bc323f0e7bd3f5eb7a0490e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62730421"
---
# <a name="connect-from-client-applications-analysis-services"></a>從用戶端應用程式連接 (Analysis Services)
  如果您不熟悉 Analysis Services，請透過本主題中的資訊，使用常用的工具和應用程式連接至 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 現有的執行個體。 本主題也說明如何以不同的使用者識別進行連接，方便測試之用。  
  
-   [使用 SQL Server Management Studio (SSMS) 連接](#bkmk_SSMS)  
  
-   [使用 Excel 連接](#bkmk_excel)  
  
-   [使用 SQL Server Data Tools 連接](#bkmk_SSDT)  
  
-   [測試連接](#bkmk_tshoot)  
  
 連接字串參考文件為另外提供。 如需詳細資訊，請參閱[連接字串屬性 &#40;Analysis Services&#41;](connection-string-properties-analysis-services.md)。  
  
 成功的連接取決於有效的通訊埠組態和適當的使用者權限。 請按一下下列連結，深入了解每一個需求。  
  
-   [設定 Windows 防火牆以允許 Analysis Services 存取](configure-the-windows-firewall-to-allow-analysis-services-access.md)  
  
-   [物件和作業的存取權授權 &#40;Analysis Services&#41;](../multidimensional-models/authorizing-access-to-objects-and-operations-analysis-services.md)  
  
##  <a name="bkmk_SSMS"></a> 使用 SQL Server Management Studio (SSMS) 連接  
 您可以使用 SSMS 連接至 Analysis Services，以互動方式管理伺服器執行個體和資料庫。 您也可以執行 XMLA 或 MDX 查詢，以執行管理工作或擷取資料。 相較於在傳送查詢時只會載入資料庫的其他工具和應用程式，SSMS 會在您連接到伺服器時載入所有資料庫，前提是您有權檢視資料庫。 這表示，如果您在伺服器上擁有許多表格式資料庫，當您使用 SSMS 連接時，所有資料庫都會載入系統記憶體中。  
  
 您可以使用特定使用者識別來執行 SSMS，然後以該使用者的身分連接至 Analysis Services 來測試權限。  
  
 按住 Shift 鍵並以滑鼠右鍵按一下 [SQL Server Management Studio] 捷徑，即可存取 [以不同的使用者身分執行] 選項。  
  
1.  啟動 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。 在 [連接到伺服器] 對話方塊中，選取 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 伺服器類型。  
  
2.  在 [登入] 索引標籤中，輸入伺服器執行所在的電腦名稱來輸入伺服器名稱。 您可以使用其網路名稱或完整網域名稱來指定伺服器。  
  
     如果是具名執行個體，必須使用下列格式指定伺服器名稱：伺服器名稱\執行個體名稱。 這個命名慣例的可能範例如下：ADV-SRV062\Finance 代表網路名稱為 ADV-SRV062 的伺服器，其中 Analysis Services 已安裝為標題為 Finance 的具名執行個體。  
  
     如果是部署在容錯移轉叢集中的伺服器，請使用 SSAS 叢集的網路名稱連接。 SQL Server 安裝期間會將這個名稱指定為 [SQL Server 網路名稱]。 請注意，如果您在 Windows Server 容錯移轉叢集 (WSFC) 上安裝 SSAS 當做具名執行個體，絕對不要在連接上加入此執行個體名稱。 這對 SSAS 而言是唯一的作法；相反地，叢集關聯式資料庫引擎的具名執行個體有包含此執行個體名稱。 例如，如果您使用 SQL Server 網路名稱 SQL-CLU 安裝 SSAS 和資料庫引擎當做具名執行個體 (Contoso-Accounting)，您會使用 "SQL-CLU" 連接到 SSAS 並且以 "SQL-CLU\Contoso-Accounting" 身分連接到資料庫引擎。 如需詳細資訊和範例，請參閱 [How to Cluster SQL Server Analysis Services](https://go.microsoft.com/fwlink/p/?LinkId=396548) (如何將 SQL Server Analysis Services 叢集化)。  
  
     如果是部署在網路負載平衡叢集中的伺服器，則使用 NLB 的虛擬伺服器名稱連接。  
  
3.  驗證一定會是 Windows 驗證，而且使用者識別一定會是透過 Management Studio 連接的 Windows 使用者。  
  
     為了要讓連接成功，您必須擁有存取伺服器或伺服器上之資料庫的權限。 您要在 Management Studio 中執行的大部分工作都需要管理權限， 因此請確定您所連接的帳戶為伺服器管理員角色的成員。 如需詳細資訊，請參閱 <<c0> [ 授與伺服器系統管理員權限&#40;Analysis Services&#41;](grant-server-admin-rights-to-an-analysis-services-instance.md)。</c0>  
  
4.  按一下 [連接屬性] 指定特定的資料庫、設定逾時值或加密選項。 選擇性連接資訊包括只用於目前連接的連接屬性。  
  
5.  按一下 [其他連接參數] 索引標籤，設定 [連接到伺服器] 對話方塊中無法設定的連接屬性。 例如，您可以在文字方塊中輸入 `Roles=Reader`。  
  
     透過擁有較低權限的角色來連接時，如果這個角色已經生效，您就能測試資料庫行為。  
  
    ```  
    Provider=MSOLAP; Data Source=SERVERNAME; Initial Catalog=AdventureWorks2012; Roles=READER  
    ```  
  
##  <a name="bkmk_excel"></a> 使用 Excel 連接  
 Microsoft Excel 通常用來分析商務資料。 在 Excel 安裝過程中，Office 會安裝 Analysis Services OLE DB 提供者 (MSOLAP DLL)、ADOMD.NET 和其他資料提供者，好讓您可以更輕易地使用網路伺服器上的資料。 如果您搭配舊版的 Excel 使用較新版的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ，您很可能必須在連接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]的每一個工作站上安裝較新的資料提供者。 如需詳細資訊，請參閱 [用於 Analysis Services 連接的資料提供者](data-providers-used-for-analysis-services-connections.md) 。  
  
 當您設定與 Analysis Services Cube 或表格式模型資料庫的連接時，Excel 會將連接資訊儲存到 .odc 檔案中，以供將來使用。 連接是在目前 Windows 使用者的安全性內容中建立。 使用者帳戶必須擁有資料庫的讀取權限，才能連接成功。  
  
 當您使用 Excel 活頁簿中的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料時，查詢要求的持續期間將會保留連接。 這就是為什麼當您從 Excel 監視查詢工作負載時，您可能會看到每個工作階段都有許多連接，這些連接保留很短的時間。  
  
 您可以使用特定使用者識別啟動 Excel 來測試權限。  
  
 按住 Shift 鍵並以滑鼠右鍵按一下 [Excel] 捷徑，即可存取 [以不同的使用者身分執行] 選項。  
  
1.  在 Excel 的 [資料] 索引標籤中按一下 [從其他來源]，然後按一下 [從 Analysis Services]。 輸入伺服器名稱，然後選取要查詢的 Cube 或檢視方塊。  
  
     如果是部署在負載平衡叢集中的伺服器，請使用指派給叢集的虛擬伺服器名稱。  
  
2.  當您在 Excel 中設定連接時，您可以在資料連線精靈的最後一頁上指定 Excel Services 的驗證設定。 這些設定是用來設定活頁簿上的屬性，前提是您將活頁簿上傳到擁有 Excel Services 的 SharePoint 伺服器。 這些設定會用於資料重新整理作業。 選項包括 [Windows 驗證]、[Secure Store Service] (SSS) 和 [無]。  
  
     請避免使用 [無]。 Analysis Services 無法讓您指定連接字串上的使用者名稱和密碼，除非您連接到已經有設定 HTTP 存取的伺服器。 同樣地，除非您已經知道 SSS 目標應用程式識別碼會對應到擁有 Analysis Services 資料庫之使用者存取權的一組 Windows 使用者認證，否則請勿使用 SSS。 在大部分情況下，使用 Windows 驗證的預設選項是來自 Excel 之 Analysis Services 連接的最佳選擇。  
  
 如需詳細資訊，請參閱＜ [連接到 SQL Server Analysis Services 或是從中匯入資料](https://go.microsoft.com/fwlink/?linkID=215150)＞。  
  
##  <a name="bkmk_SSDT"></a> 使用 SQL Server Data Tools 連接  
 SQL Server Data Tools 用於建置 BI 方案，其中包括 Analysis Services 模型、Reporting Services 報表和 SSIS 封裝。 在建置報表或封裝時，您可能必須指定 Analysis Services 的連接。  
  
 下列連結說明如何從報表伺服器專案或 Integration Services 專案連接至 Analysis Services：  
  
-   [MDX 的 Analysis Services 連接類型 &#40;SSRS&#41;](../../reporting-services/report-data/analysis-services-connection-type-for-mdx-ssrs.md)  
  
-   [Analysis Services 連接管理員](../../integration-services/connection-manager/analysis-services-connection-manager.md)  
  
> [!NOTE]  
>  使用 SQL Server Data Tools 處理現有的 Analysis Services 專案時，以線上模式專案，請記住您可以使用本機或版本控制專案以離線方式連接，或者使用線上模式連接，在資料庫執行期間更新 Analysis Services 物件。 如需詳細資訊，請參閱 [在連線模式下連接至 Analysis Services 資料庫](../multidimensional-models/connect-in-online-mode-to-an-analysis-services-database.md)。 更常見的情況是，來自 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 的連接會處於專案模式，而且只有當您明確部署專案時，其中的變更才會部署到資料庫。  
  
##  <a name="bkmk_tshoot"></a> 測試連接  
 您可以使用 SQL Server Profiler 監視 Analysis Services 的連接。 「稽核登入」和「稽核登出」事件都會提供連接的辨識項。 識別欄位表示建立連接時遵循的安全性內容。  
  
1.  在 Analysis Services 執行個體上啟動 **SQL Server Profiler** ，然後啟動新的追蹤。  
  
2.  在 [事件選取範圍] 的 [安全性稽核] 區段，確認已核取 [`Audit Login`] 和 [`Audit Logout`]。  
  
3.  從遠端用戶端電腦透過應用程式服務 (例如 SharePoint 或 Reporting Services) 連接到 Analysis Services。 「稽核登入」事件將會顯示連接到 Analysis Services 的使用者之身分識別。  
  
 發生連接錯誤時，追蹤其原因通常是不完整或無效的伺服器組態所導致。 因此，請務必先檢查伺服器組態：  
  
-   從遠端電腦 Ping 伺服器，確保它允許遠端連接。  
  
-   **伺服器上的防火牆規則允許來自相同網域中用戶端的傳入連接**  
  
     除了 PowerPivot for SharePoint 以外，與遠端伺服器的所有連接都會要求您已經設定防火牆允許存取 Analysis Services 所接聽的通訊埠。 如果您得到連接錯誤，請確認此通訊埠確實可存取，而且已經授與使用者權限給適當的資料庫。  
  
     若要測試，請使用 Excel 或 SSMS 並指定 Analysis Services 執行個體使用的 IP 位址和通訊埠，然後連接到遠端電腦。 如果可以連接，表示防火牆規則允許執行個體的傳入連接，而且執行個體也允許遠端連接。  
  
     此外，使用 TCP/IP 做為連接通訊協定時，請記住用戶端必須位於相同網域或信任網域中才能連接 Analysis Services。 如果連接是跨安全性界限進行，您就必須設定 HTTP 存取。 如需詳細資訊，請參閱 [設定 Internet Information Services &#40;IIS&#41; 8.0 上 Analysis Services 的 HTTP 存取](configure-http-access-to-analysis-services-on-iis-8-0.md)(Microsoft BI 驗證及識別委派)。  
  
-   您是否能使用一些工具連接，但是其他工具就不行？ 這個問題可能是用戶端程式庫版本錯誤。 您可以從 SQL Server 功能套件下載頁面取得用戶端程式庫。  
  
 下列文件也能協助您解決連接失敗的問題：  
  
 [Resolving Common Connectivity Issues in SQL Server 2005 Analysis Services Connectivity Scenarios](https://technet.microsoft.com/library/cc917670.aspx)(在 SQL Server 2005 Analysis Services 連接狀況中解決常見的連接問題)。 這份文件已經有一些歲月，但是其中的資訊和方法仍然適用。  
  
## <a name="see-also"></a>另請參閱  
 [連接到 Analysis Services](connect-to-analysis-services.md)   
 [Analysis Services 支援的驗證方法](authentication-methodologies-supported-by-analysis-services.md)   
 [模擬 &#40;SSAS 表格式&#41;](../tabular-models/impersonation-ssas-tabular.md)   
 [建立資料來源 &#40;SSAS 多維度&#41;](../multidimensional-models/create-a-data-source-ssas-multidimensional.md)  
  
  
