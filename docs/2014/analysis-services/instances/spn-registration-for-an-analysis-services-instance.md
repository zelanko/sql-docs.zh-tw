---
title: Analysis Services 執行個體註冊 SPN |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 9e78dc37-a3f0-415d-847c-32fec69efa8c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d13d7b7f65ca1f121145815555afa055926c81fe
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/13/2018
ms.locfileid: "53374270"
---
# <a name="spn-registration-for-an-analysis-services-instance"></a>SPN registration for an Analysis Services instance
  使用 Kerberos 相互驗證用戶端和服務識別時，服務主要名稱 (SPN) 可唯一識別在 Active Directory 網域中的服務執行個體。 SPN 與服務執行個體的執行登入帳戶有關。  
  
 對透過 Kerberos 驗證連接至 Analysis Services 的用戶端應用程式而言，Analysis Services 用戶端程式庫會使用連接字串中的主機名稱和所有 Analysis Services 之指定版本中固有的已知變數 (例如服務類別) 來建構 SPN。  
  
 用戶端建構的 SPN 必須符合 Active Directory 網域控制站 (DC) 上的對應 SPN 物件，才能進行相互驗證。 這表示您可能需要註冊多個 SPN，讓單一 Analysis Services 執行個體可以涵蓋使用者在連接字串上指定主機名稱的所有方式。 例如，您可能需要兩個 SPN 處理伺服器的完整網域名稱 (FQDN) 以及簡短電腦名稱。 您必須正確註冊 Analysis Services SPN 才能成功連接。 如果 SPN 不存在、格式不正確或重複，連接就會失敗。  
  
 Analysis Services 管理員必須手動註冊 SPN。 不同於 SQL Server Database Engine，Analysis Services 從來不會在服務啟動時自動註冊其 SPN。 以預設虛擬帳戶、網域使用者帳戶或內建帳戶身分 (包括個別服務 SID) 執行 Analysis Services 時，就必須手動註冊。  
  
 如果服務在網域管理員所建立之預先定義的受管理服務帳戶之下執行，就不需要註冊 SPN。 請注意，視您網域的功能層級而定，可能需要網域管理員權限才能註冊 SPN。  
  
> [!TIP]  
>  **[!INCLUDE[msCoName](../../includes/msconame-md.md)] Kerberos Configuration Manager for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** 是一種診斷工具，可幫助排除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發生的 Kerberos 相關連接問題。 如需詳細資訊，請參閱 [Microsoft Kerberos Configuration Manager for SQL Server](https://www.microsoft.com/download/details.aspx?id=39046)。  
  
> [!TIP]  
>  **[!INCLUDE[msCoName](../../includes/msconame-md.md)] Kerberos Configuration Manager for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** 是一種診斷工具，可幫助排除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發生的 Kerberos 相關連接問題。 如需詳細資訊，請參閱 [Microsoft Kerberos Configuration Manager for SQL Server](https://www.microsoft.com/download/details.aspx?id=39046)。  
  
 本主題包含下列幾節：  
  
 [必須註冊 SPN 的時機](#bkmk_scnearios)  
  
 [Analysis Services 的 SPN 格式](#bkmk_SPNSyntax)  
  
 [虛擬帳戶的 SPN 註冊](#bkmk_virtual)  
  
 [網域帳戶的 SPN 註冊](#bkmk_domain)  
  
 [內建帳戶的 SPN 註冊](#bkmk_builtin)  
  
 [為具名執行個體註冊 SPN](#bkmk_spnNamed)  
  
 [為 SSAS 叢集註冊 SPN](#bkmk_spnCluster)  
  
 [為設定使用 HTTP 存取的 SSAS 執行個體註冊 SPN](#bkmk_spnHTTP)  
  
 [為接聽固定通訊埠的 SSAS 執行個體註冊 SPN](#bkmk_spnFixedPorts)  
  
##  <a name="bkmk_scnearios"></a> 必須註冊 SPN 的時機  
 所有用戶端連接，指定"SSPI = Kerberos"連接字串將介紹 Analysis Services 執行個體的 SPN 註冊需求。  
  
 在下列情況下，您必須註冊 SPN。 如需更詳細的資訊，請參閱＜ [Configure Analysis Services for Kerberos constrained delegation](configure-analysis-services-for-kerberos-constrained-delegation.md)＞。  
  
-   將使用者識別從用戶端應用程式或中介層服務流到 Analysis Services 需要身分識別委派。 在特定物件上定義每個使用者的權限或篩選時，通常會使用身分識別委派。  
  
     與身分識別委派有關的常見情況如下：在 Analysis Services 中擷取資料時，針對限制委派設定中介層服務 (例如 Excel Services 或 Reporting Services)，以模擬使用者識別。 若要支援這個行為，當您為限制委派設定 Excel Services 或 Reporting Services 時，必須提供 Analysis Services SPN 當做目的地服務。  
  
-   使用 DirectQuery 模式從表格式資料庫的 SQL Server 關聯式資料庫擷取資料時，Analysis Services 會委派使用者識別。 唯有在此狀況下 Analysis Services 才會將使用者識別委派給其他服務。  
  
##  <a name="bkmk_SPNSyntax"></a> Analysis Services 的 SPN 格式  
 使用 **setspn** 註冊 SPN。 在新版作業系統上， **setspn** 是以系統公用程式的形式安裝。 如需詳細資訊，請參閱＜ [SetSPN](https://technet.microsoft.com/library/cc731241\(WS.10\).aspx)＞。  
  
 下表說明 Analysis Services SPN 的每一個部分。  
  
|元素|描述|  
|-------------|-----------------|  
|服務類別|MSOLAPSvc.3 會將服務識別為 Analysis Services 執行個體， 其中 .3 是 Analysis Services 傳輸時所使用 XMLA-over-TCP/IP 通訊協定版本的參考， 與產品版本無關。 因此，除非通訊協定本身有異動，否則 MSOLAPSvc.3 都會是 SQL Server 2005、2008、2008 R2、2012 以及未來所有 Analysis Services 版本的正確服務類別。|  
|主機名稱|識別執行服務的電腦。 可以是完整網域名稱或 NetBIOS 名稱 您應該針對這兩者註冊 SPN。<br /><br /> 當您針對伺服器的 NetBIOS 名稱註冊 SPN 時，請務必使用 `SetupSPN -S` 來檢查是否有重複註冊。 樹系中可能會有重複的 NetBIOS 名稱，而重複的 SPN 註冊將會導致連接失敗。<br /><br /> 如果是 Analysis Services 負載平衡叢集，主機名稱必須是指派給叢集的虛擬名稱。<br /><br /> 請絕對不要使用 IP 位址來建立 SPN， 因為 Kerberos 會使用 DNS 網域解析功能， 如果指定 IP 位址則會略過這項功能。|  
|通訊埠編號|雖然通訊埠編號是 SPN 語法的一部分，但是在註冊 Analysis Services SPN 時，請絕對不要指定通訊埠編號。 冒號 (:) 字元在標準 SPN 語法中通常是用來提供通訊埠編號，但是 Analysis Services 則是用來指定執行個體名稱。 Analysis Services 執行個體的通訊埠會假設是預設的通訊埠 (TCP 2383) 或 SQL Server Browser 服務指派的通訊埠 (TCP 2382)。|  
|執行個體名稱|Analysis Services 是可在相同電腦上安裝多次的可複寫服務。 每個執行個體都是透過其執行個體名稱加以識別。<br /><br /> 執行個體名稱會以冒號 (:) 字元當做開頭。 例如，有名稱為 SRV01 的主機電腦和名稱為 SSAS-Tabular 的執行個體，則 SPN 應該是 SRV01:SSAS-Tabular。<br /><br /> 請注意，指定的 Analysis Services 具名執行個體的語法與其他 SQL Server 執行個體所使用的語法有所不同。 其他服務都會使用反斜線 (\) 在 SPN 中附加執行個體名稱。|  
|服務帳戶|這是 **MSSQLServerOLAPService** Windows 服務的啟動帳戶。 可以是 Windows 網域使用者帳戶、虛擬帳戶、受管理的服務帳戶 (MSA) 或內建帳戶 (如個別服務 SID、NetworkService 或 LocalSystem)。 Windows 網域使用者帳戶可格式化為 「 網域 \ 使用者或user@domain。|  
  
##  <a name="bkmk_virtual"></a> 虛擬帳戶的 SPN 註冊  
 虛擬帳戶是 SQL Server 服務的預設帳戶類型。 虛擬帳戶是**NT Service\MSOLAPService**的預設執行個體並**NT Service\MSOLAP$**\<執行個體名稱 > 的具名執行個體。  
  
 如同名稱所指示，這些帳戶在 Active Directory 中並不存在。 虛擬帳戶只存在於本機電腦上。 當連接到外部服務、應用程式或裝置時，將會使用本機帳戶進行連接。 因此，在虛擬帳戶之下執行之 Analysis Services 的 SPN 註冊實際上是電腦帳戶的 SPN 註冊。  
  
 **以 NT Service\MSOLAPService 身分執行之預設執行個體的範例語法**  
  
 這個範例會針對在預設虛擬帳戶之下執行的 Analysis Services 預設執行個體顯示 **setspn** 語法。 在此範例中，電腦主機名稱為 **AW-SRV01**。 如前所述，SPN 註冊必須指定 *「電腦帳戶」* ，而不是虛擬帳戶 **NT Service\MSOLAPService**。  
  
```  
Setspn -s MSOLAPSvc.3/AW-SRV01.AdventureWorks.com AW-SRV01  
```  
  
> [!NOTE]  
>  請記得建立兩個 SPN 註冊，一個用於 NetBIOS 主機名稱，另一個則用於主機的完整網域名稱。 當連接到 Analysis Services 時，不同的用戶端應用程式會使用不同的主機名稱慣例。 有兩個 SPN 註冊可確保這兩個版本的主機名稱都計算在內。  
  
 **以 NT Service\MSOLAP$ 身分執行的具名執行個體的範例語法\<執行個體名稱 >**  
  
 這個範例會針對在預設虛擬帳戶之下執行的具名執行個體顯示 **setspn** 語法。 在此範例中，電腦主機名稱為 **AW-SRV02**，執行個體名稱則為 **AW-FINANCE**。 同樣地，它是 SPN，針對指定的電腦帳戶，而不是虛擬帳戶時**NT Service\MSOLAP$**\<執行個體名稱 >。  
  
```  
Setspn -s MSOLAPSvc.3/AW-SRV02.AdventureWorks.com:AW-FINANCE AW-SRV02  
```  
  
##  <a name="bkmk_domain"></a> 網域帳戶的 SPN 註冊  
 使用網域帳戶執行 Analysis Services 執行個體是常見的作法。  
  
 如果是在網路或硬體負載平衡叢集內執行的 Analysis Services 執行個體，將需要網域帳戶，而叢集內的每個執行個體都會在相同的網域帳戶之下執行。  
  
 **以網域使用者身分執行之預設執行個體的範例語法**  
  
 此範例會顯示在 AdventureWorks 網域中，以網域使用者帳戶 **SSAS-Service** 執行之 Analysis Services 預設執行個體的 **setspn**語法。  
  
```  
Setspn -s msolapsvc.3\AW-SRV01.Adventureworks.com AdventureWorks\SSAS-Service  
```  
  
> [!TIP]  
>  請藉由執行 `Setspn -L <domain account>` 或 `Setspn -L <machinename>`(根據如何註冊 SPN) 來確認是否已針對 Analysis Services 伺服器建立 SPN。 您應該會看到 msolapsvc.3 /\<主機名稱 > 清單中。  
  
##  <a name="bkmk_builtin"></a> 內建帳戶的 SPN 註冊  
 雖然不建議採取這個作法，但是舊版的 Analysis Services 安裝有時會設定為在內建帳戶 (如 Network Service、Local Service 或 Local System) 之下執行。  
  
 **在內建帳戶之下執行之預設執行個體的範例語法**  
  
 在內建帳戶或個別服務 SID 之下執行之服務的 SPN 註冊相當於用於虛擬帳戶的 SPN 語法。 請使用電腦帳戶，而不是帳戶名稱：  
  
```  
Setspn -s MSOLAPSvc.3/AW-SRV01.AdventureWorks.com AW-SRV01  
```  
  
##  <a name="bkmk_spnNamed"></a> 為具名執行個體註冊 SPN  
 Analysis Services 的具名執行個體會使用 SQL Server Browser 服務所偵測到的動態通訊埠指定。 當使用具名執行個體時，請同時為 SQL Server Browser 服務和 Analysis Services 具名執行個體註冊 SPN。 如需詳細資訊，請參閱 [建立連接至 SQL Server Analysis Services 或 SQL Server 的具名執行個體時，需要 SQL Server Browser 服務的 SPN](https://support.microsoft.com/kb/950599)(機器翻譯)。  
  
 **以 LocalService 身分執行之 SQL Browser 服務的 SPN 語法範例**  
  
 服務類別為 **MSOLAPDisco.3**。 根據預設，這個服務會以 NT AUTHORITY\LocalService 身分執行，這表示已針對電腦帳戶設定 SPN 註冊。 在此範例中，電腦帳戶是 **AW-SRV01**(對應到電腦名稱)。  
  
```  
Setspn -S MSOLAPDisco.3/AW-SRV01.AdventureWorks.com AW-SRV01  
```  
  
##  <a name="bkmk_spnCluster"></a> 為 SSAS 叢集註冊 SPN  
 如果是 Analysis Services 容錯移轉叢集，主機名稱必須是指派給叢集的虛擬名稱。 這是當您安裝在現有的 WSFC 上安裝 Analysis Services 時，SQL Server 安裝程式所指定的 SQL Server 網路名稱。 您可以在 Active Directory 中找到此名稱。 您也可以在 [容錯移轉叢集管理員]  |  |  索引標籤中尋找。[資源] 索引標籤上的伺服器名稱是在 SPN 命令中，要用為「虛擬名稱」的名稱。  
  
 **Analysis Services 叢集的 SPN 語法**  
  
```  
Setspn -s msolapsvc.3/<virtualname.FQDN > <domain user account>  
```  
  
 請記得 Analysis Services 叢集中的節點都必須使用預設通訊埠 (TCP 2383)，而且必須以相同的網域使用者帳戶來執行，如此每個節點才有相同的 SID。 如需詳細資訊及範例，請參閱 [如何建立 SQL Server Analysis Services 叢集](https://msdn.microsoft.com/library/dn736073.aspx) 。  
  
##  <a name="bkmk_spnHTTP"></a> 為設定使用 HTTP 存取的 SSAS 執行個體註冊 SPN  
 根據方案需求，您可能已經設定使用 HTTP 存取 Analysis Services。 如果您的方案包含 IIS 做為中間層元件，而且必須使用 Kerberos 驗證，則必須為 IIS 手動註冊 SPN。 如需詳細資訊，請參閱 [設定執行 IIS 的電腦上的設定]，在[如何設定 SQL Server 2008 Analysis Services 和 SQL Server 2005 Analysis Services 使用 Kerberos 驗證](https://support.microsoft.com/kb/917409)。  
  
 為 Analysis Services 執行個體註冊 SPN 時，設定要使用 TCP 還是 HTTP 來存取執行個體並沒有差異。 使用 MSMDPUMP ISAPI 擴充程式從 IIS 連接至 Analysis Services 時，通訊協定一律是 TCP。  
  
 這表示您可以沿用上一節中為預設或具名執行個體註冊 SPN 的指示。 指定主機名稱時，請務必使用您在設定使用 HTTP 存取服務時，於 msmdpump.ini 檔案中指定的主機名稱。  
  
 如需 HTTP 存取的詳細資訊，請參閱[設定 Internet Information Services &#40;IIS&#41; 8.0 上 Analysis Services 的 HTTP 存取](configure-http-access-to-analysis-services-on-iis-8-0.md)。  
  
##  <a name="bkmk_spnFixedPorts"></a> 為接聽固定通訊埠的 SSAS 執行個體註冊 SPN  
 您無法在註冊 Analysis Services SPN 時指定通訊埠編號。 如果已安裝 Analysis Services 做為預設執行個體並設定為接聽固定通訊埠，現在就必須改設定為接聽預設通訊埠 (TCP 2383)。 如果是具名執行個體，您必須使用 SQL Server Browser 服務與動態通訊埠指派。  
  
 Analysis Services 執行個體只能接聽單一通訊埠， 因此不支援使用多個通訊埠。 如需通訊埠組態的詳細資訊，請參閱＜ [Configure the Windows Firewall to Allow Analysis Services Access](configure-the-windows-firewall-to-allow-analysis-services-access.md)＞。  
  
## <a name="see-also"></a>另請參閱  
 [Microsoft BI 驗證及識別委派](https://go.microsoft.com/fwlink/?LinkID=286576)   
 [使用 Kerberos 進行相互驗證](https://go.microsoft.com/fwlink/?LinkId=299283)   
 [如何設定 SQL Server 2008 Analysis Services 和 SQL Server 2005 Analysis Services 使用 Kerberos 驗證](https://support.microsoft.com/kb/917409)   
 [服務主體名稱 (SPN) SetSPN 語法 (Setspn.exe)](https://social.technet.microsoft.com/wiki/contents/articles/717.service-principal-names-spns-setspn-syntax-setspn-exe.aspx)   
 [我應使用何種 SPN？其運作方式為何？](https://social.technet.microsoft.com/wiki/contents/articles/717.service-principal-names-spns-setspn-syntax-setspn-exe.aspx)   
 [SetSPN](https://technet.microsoft.com/library/cc731241\(WS.10\).aspx)   
 [服務帳戶的逐步指南](https://technet.microsoft.com/library/dd548356\(WS.10\).aspx)   
 [設定 Windows 服務帳戶與權限](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)   
 [在設定 Internet Information Services 所裝載的 Web 應用程式時如何使用 SPN](https://support.microsoft.com/kb/929650)   
 [什麼是服務帳戶的新功能](https://technet.microsoft.com/library/dd367859\(WS.10\).aspx)   
 [設定適用於 SharePoint 2010 產品的 Kerberos 驗證 (白皮書)](https://technet.microsoft.com/library/ff829837.aspx)  
  
  
