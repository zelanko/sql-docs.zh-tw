---
title: 設定 Analysis Services 進行 Kerberos 限制委派 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 6d751477-6bf1-48b4-8833-5a631bbe7650
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 20e8a9d7b360b9b161d994805ff713840962be41
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62730895"
---
# <a name="configure-analysis-services-for-kerberos-constrained-delegation"></a>設定 Analysis Services 進行 Kerberos 限制委派
  將 Analysis Services 設定為 Kerberos 驗證時，若能獲致下列其中一項或兩項結果，對您來說可能最有用處：讓 Analysis Services 在查詢資料時模擬使用者識別，或是由 Analysis Services 將使用者識別委派給下層服務。 每一種情況的組態需求略有不同。 這兩種情況都需要驗證以確保組態設定正確。  
  
> [!TIP]  
>  **[!INCLUDE[msCoName](../../includes/msconame-md.md)] Kerberos Configuration Manager for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** 是一種診斷工具，可幫助排除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發生的 Kerberos 相關連接問題。 如需詳細資訊，請參閱 [Microsoft Kerberos Configuration Manager for SQL Server](https://www.microsoft.com/download/details.aspx?id=39046)。  
  
 本主題包含下列幾節：  
  
-   [允許 Analysis Services 模擬使用者識別](#bkmk_impersonate)  
  
-   [設定 Analysis Services 進行受信任委派](#bkmk_delegate)  
  
-   [測試模擬或委派的身分識別](#bkmk_test)  
  
> [!NOTE]  
>  如果與 Analysis Services 的連接是單一躍點，或者您的方案使用 SharePoint Secure Store Service 或 Reporting Services 提供的預存認證，便不需要委派。 若所有的連接都是從 Excel 到 Analysis Services 資料庫的直接連接，或是以預存認證為基礎，您就可以使用 Kerberos (或 NTLM)，無須設定限制委派。  
>   
>  如果使用者身分識別必須經過多重電腦連接 （稱為 「 雙躍點 」），則需要 Kerberos 限制委派。 若情況是 Analysis Services 資料存取權視使用者識別而定且連接要求來自委派的服務，請使用下一節的檢查清單以確保 Analysis Services 能夠模擬原始呼叫端。 如需有關 Analysis Services 驗證流程的詳細資訊，請參閱 [Microsoft BI 驗證及識別授權](https://go.microsoft.com/fwlink/?LinkID=286576)。  
>   
>  為了安全起見，Microsoft 始終建議使用限制委派，而不要使用非限制委派。 非限制委派是主要的安全性風險，因其可允許服務識別在「任一」  下游電腦、服務或應用程式上模擬其他使用者 (而不只是透過限制委派明確定義的那些服務)。  
  
##  <a name="bkmk_impersonate"></a> 允許 Analysis Services 模擬使用者識別  
 若要允許上層服務 (如 Reporting Services、IIS 或 SharePoint) 模擬 Analysis Services 的使用者身分識別，您必須為這些服務設定 Kerberos 限制委派。 在此情況下，Analysis Services 會使用委派服務提供的身分識別來模擬目前的使用者，根據該使用者身分識別的角色成員資格傳回結果。  
  
|工作|描述|  
|----------|-----------------|  
|步驟 1:確認帳戶適合於委派|確認用以執行服務的帳戶在 Active Directory 中具有正確的屬性。 服務帳戶在 Active Directory 中不得標示為機密帳戶，或是明確地從委派狀況排除。 如需詳細資訊，請參閱 [了解使用者帳戶](https://go.microsoft.com/fwlink/?LinkId=235818)。<br /><br /> **\*\* 重要\* \*** 一般而言，所有帳戶及伺服器必須都屬於相同的 Active Directory 網域或相同樹系中的受信任網域。 不過，由於 Windows Server 2012 支援跨網域界限委派，若網域功能層級是 Windows Server 2012，您就可以設定跨網域界限的 Kerberos 限制委派。 另一種替代方式則是設定 Analysis Services 進行 HTTP 存取並對用戶端連接使用 IIS 驗證方法。 如需詳細資訊，請參閱 [設定 Internet Information Services &#40;IIS&#41; 8.0 上 Analysis Services 的 HTTP 存取](configure-http-access-to-analysis-services-on-iis-8-0.md)(Microsoft BI 驗證及識別委派)。|  
|步驟 2:註冊 SPN|設定限制委派之前，您必須為 Analysis Services 執行個體註冊服務主要名稱 (SPN)。 在您為中介層服務設定 Kerberos 限制委派時，將需要 Analysis Services SPN。 如需相關指示，請參閱＜ [SPN registration for an Analysis Services instance](spn-registration-for-an-analysis-services-instance.md) ＞。<br /><br /> 服務主要名稱 (SPN) 係指定某項服務在設定為 Kerberos 驗證之網域中的唯一識別。 使用整合式安全性的用戶端連接通常會在 SSPI 驗證期間要求 SPN。 如果用戶端出示的 SPN 與 Active Directory 中的 SPN 註冊相符，此要求便會轉送至 Active Directory 網域控制站 (DC)，並由 KDC 授與票證。|  
|步驟 3：設定限制的委派|驗證要使用的帳戶以及註冊該等帳戶的 SPN 之後，下一個步驟是設定上層服務如 IIS、Reporting Services 或 SharePoint Web 服務進行限制委派，將 Analysis Services SPN 指定為允許委派的特定服務。<br /><br /> 在 SharePoint 中執行的服務 (例如 Excel Services 或 SharePoint 模式的 Reporting Services) 通常裝載了取用 Analysis Services 多維度或表格式資料的活頁簿和報表。 為這些服務設定限制委派既是常見的組態工作，也是支援從 Excel Services 進行資料重新整理的必備要件。 下列連結提供有關 SharePoint 服務以及可能向 Analysis Services 資料提出下游資料連接要求之其他服務的指示：<br /><br /> [Excel Services 的身分識別委派 (SharePoint Server 2010)](https://go.microsoft.com/fwlink/?LinkId=299826) 或 [How to configure Excel Services in SharePoint Server 2010 for Kerberos authentication](https://support.microsoft.com/kb/2466519)<br /><br /> [PerformancePoint Services 的身分識別委派 (SharePoint Server 2010)](https://go.microsoft.com/fwlink/?LinkId=299827)<br /><br /> [SQL Server Reporting Services 的身分識別委派 (SharePoint Server 2010)](https://go.microsoft.com/fwlink/?LinkId=299828)<br /><br /> 如需 IIS 7.0 方面的資訊，請參閱 [Configure Windows Authentication (IIS 7.0)](https://technet.microsoft.com/library/cc754628\(v=ws.10\).aspx) (設定 Windows 驗證 (IIS 7.0)) 或 [How to configure SQL Server 2008 Analysis Services and SQL Server 2005 Analysis Services to use Kerberos authentication](https://support.microsoft.com/kb/917409)(如何設定 SQL Server 2008 Analysis Services 和 SQL Server 2005 Analysis Services 使用 Kerberos 驗證)。|  
|步驟 4：測試連接|進行測試時，請以不同的身分識別從遠端電腦連接，並且使用與商務使用者所用相同的應用程式查詢 Analysis Services。 您可以使用 SQL Server Profiler 監視連接。 您應該會看到提出要求的使用者識別。 如需詳細資訊，請參閱本節中的 [測試模擬或委派的身分識別](#bkmk_test) 。|  
  
##  <a name="bkmk_delegate"></a> 設定 Analysis Services 進行受信任委派  
 設定 Analysis Services 進行 Kerberos 限制委派讓本服務得以模擬下層服務如關聯式資料庫引擎的用戶端識別，從而能夠有如用戶端直接連接般地查詢資料。  
  
 Analysis Services 的委派狀況乃限制為設定 `DirectQuery` 模式的表格式模型。 唯有在此狀況下 Analysis Services 才能將委派的認證傳遞給其他服務。 在其他所有案例 (如上一節提及的 SharePoint 案例) 中，Analysis Services 位於委派鏈結的接收端。 如需 DirectQuery 的詳細資訊，請參閱 [DirectQuery 模式 &#40;SSAS 表格式&#41;](../tabular-models/directquery-mode-ssas-tabular.md)。  
  
> [!NOTE]  
>  經常造成誤解的是，ROLAP 儲存、處理作業或遠端資料分割的存取會因不明原因而有限制委派的需求。 事實並非如此。 這些作業全部是由服務帳戶 (亦稱為處理帳戶) 自行直接執行。 如果 Analysis Services 中的這些作業的權限會直接授與服務帳戶 (例如關聯式資料庫上的 granting db_datareader 權限，讓服務可以處理資料)，這些作業就不需要委派。 如需伺服器作業和權限的詳細資訊，請參閱[設定服務帳戶 &#40;Analysis Services&#41;](configure-service-accounts-analysis-services.md)。  
  
 本節說明如何設定 Analysis Services 進行受信任委派。 完成此工作後，Analysis Services 可將委派的認證傳送給 SQL Server，以支援表格式解決方案中使用的 DirectQuery 模式。  
  
 在開始之前：  
  
-   確認 Analysis Services 已啟動。  
  
-   確認您為 Analysis Services 註冊的 SPN 有效。 如需指示，請參閱＜ [SPN registration for an Analysis Services instance](spn-registration-for-an-analysis-services-instance.md)＞。  
  
 當上述兩項必要條件都符合時，繼續進行以下步驟。 請注意，您必須是網域管理員才能設定限制委派。  
  
1.  在 [Active Directory 使用者及電腦] 中，找出執行 Analysis Services 所使用的服務帳戶。 以滑鼠右鍵按一下該服務帳戶並選擇 **[內容]**。  
  
     為方便說明，下列螢幕擷取畫面分別使用 OlapSvc 和 SQLSvc 代表 Analysis Services 和 SQL Server。  
  
     OlapSvc 是設定為對 SQLSvc 進行限制委派的帳戶。 當您完成這項工作後，OlapSvc 即有權透過服務票證將委派的認證傳遞給 SQLSvc，以在要求資料時模擬原始呼叫端。  
  
2.  在 [委派] 索引標籤上，選取 **[信任這個使用者，但只委派指定的服務]**，接著選取 **[只使用 Kerberos]**。 按一下 **[新增]** 以指定允許由 Analysis Services 委派認證的服務。  
  
     只有當服務 (Analysis Services) 已獲指派使用者帳戶 (OlapSvc) 而且該服務已註冊 SPN 時，才會出現 [委派] 索引標籤。 SPN 註冊需要該服務為執行中。  
  
     ![SSAS_Kerberos_1_AccountProperties](../media/ssas-kerberos-1-accountproperties.gif "SSAS_Kerberos_1_AccountProperties")  
  
3.  在 [新增服務] 頁面上，按一下 **[使用者或電腦]**。  
  
     ![SSAS_Kerberos_2_](../media/ssas-kerberos-2.gif "SSAS_Kerberos_2_")  
  
4.  在 [選取使用者或電腦] 頁面上，輸入用來執行 SQL Server 執行個體以提供資料給 Analysis Services 表格式模型資料庫的帳戶。 按一下 **[確定]** 接受該服務帳戶。  
  
     如果您無法選取所需帳戶，請確認 SQL Server 正在執行且其帳戶已註冊 SPN。 如需有關資料庫引擎 SPN 的詳細資訊，請參閱＜ [}註冊 Kerberos 連接的服務主體名稱](../../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md)＞。  
  
     ![SSAS_Kerberos_3_SelectUsers](../media/ssas-kerberos-3-selectusers.gif "SSAS_Kerberos_3_SelectUsers")  
  
5.  SQL Server 執行個體應該會隨即出現在 [新增服務] 中。 同樣使用該帳戶的各項服務也將出現在此清單內。 請選擇您要使用的 SQL Server 執行個體。 按一下 **[確定]** 接受此執行個體。  
  
     ![SSAS_Kerberos_4_](../media/ssas-kerberos-4.gif "SSAS_Kerberos_4_")  
  
6.  Analysis Services 服務帳戶的內容頁面現在看起來應該類似於以下螢幕擷取畫面。 按一下 **[確定]** 儲存您的變更。  
  
     ![SSAS_Kerberos_5_Finished](../media/ssas-kerberos-5-finished.gif "SSAS_Kerberos_5_Finished")  
  
7.  以不同的身分識別，從遠端用戶端電腦連接並查詢表格式模型，測試委派是否成功。 您應該會在 SQL Server Profiler 中看到提出要求的使用者識別。  
  
##  <a name="bkmk_test"></a> 測試模擬或委派的身分識別  
 使用 SQL Server Profiler 監視查詢資料的使用者其身分識別。  
  
1.  在 Analysis Services 執行個體上啟動 **SQL Server Profiler** ，然後啟動新的追蹤。  
  
2.  在 [事件選取範圍] 的 [安全性稽核] 區段，確認已核取 [`Audit Login`] 和 [`Audit Logout`]。  
  
3.  從遠端用戶端電腦透過應用程式服務 (例如 SharePoint 或 Reporting Services) 連接到 Analysis Services。 「稽核登入」事件將會顯示連接到 Analysis Services 的使用者之身分識別。  
  
 若要進行徹底測試，必須使用能夠擷取網路上的 Kerberos 要求與回應的網路監視工具。 這項工作會使用可篩選 Kerberos 的網路監視器公用程式 (netmon.exe)。 如需使用 Netmon 3.4 和其他工具測試 Kerberos 驗證的詳細資訊，請參閱[設定 Kerberos 驗證：核心設定 (SharePoint Server 2010)](https://technet.microsoft.com/library/gg502602\(v=office.14\).aspx)。  
  
 此外，如需 Active Directory 物件內容對話方塊之 [委派] 索引標籤中每個選項的完整描述，請參閱 [Active Directory 中最易混淆的對話方塊](http://windowsitpro.com/windows/most-confusing-dialog-box-active-directory) 。 本文也說明如何使用 LDP 來測試和解譯測試結果。  
  
## <a name="see-also"></a>另請參閱  
 [Microsoft BI 驗證及識別委派](https://go.microsoft.com/fwlink/?LinkID=286576)   
 [使用 Kerberos 進行相互驗證](https://go.microsoft.com/fwlink/?LinkId=299283)   
 [連接到 Analysis Services](connect-to-analysis-services.md)   
 [SPN registration for an Analysis Services instance](spn-registration-for-an-analysis-services-instance.md)   
 [連接字串屬性 &#40;Analysis Services&#41;](connection-string-properties-analysis-services.md)  
  
  
