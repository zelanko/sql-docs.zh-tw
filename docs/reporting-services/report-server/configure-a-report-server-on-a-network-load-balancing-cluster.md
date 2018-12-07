---
title: 在網路負載平衡叢集上設定報表伺服器 | Microsoft Docs
author: markingmyname
ms.author: maghan
manager: kfile
ms.prod: reporting-services, reporting-services-sharepoint, reporting-services-native
ms.technology: report-server
ms.topic: conceptual
ms.date: 10/3/2018
ms.openlocfilehash: f9b56ce33635d51b989801b34eea279b53bd4041
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2018
ms.locfileid: "52396131"
---
# <a name="configure-a-report-server-on-a-network-load-balancing-cluster"></a>在網路負載平衡叢集上設定報表伺服器

  如果您要將報表伺服器向外延展設定為在網路負載平衡 (NLB) 叢集上執行，就必須進行下列動作：  
  
- 確定此 NLB 叢集可透過對應至虛擬伺服器 IP 位址的虛擬伺服器名稱存取。 虛擬伺服器名稱是必要的項目，如此您才能夠設定 NLB 叢集的單一進入點。 當您針對每個報表伺服器執行個體設定 URL 時，就會將此虛擬伺服器名稱指定為主機。  
  
- 設定檢視狀態驗證，以便支援互動式報表檢視。 為了回應使用者動作，互動式報表通常會在單一使用者工作階段期間轉譯許多次，以便視覺化全新或不同的資料。 透過設定檢視狀態驗證，不論哪一個報表伺服器服務實際的要求，接近程度都會保留在使用者工作階段中。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 不會提供用於向外延展部署的負載平衡或是用於透過共用 URL 定義單一存取點的功能。 您必須實作個別的軟體或硬體 NLB 叢集方案，以便支援 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 向外延展部署。  
  
 您可以將 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安裝在已經屬於 NLB 叢集之一部分的節點上，也可以先設定向外延展部署，然後再安裝叢集軟體。  
  
## <a name="steps-for-report-server-deployment-on-an-nlb-cluster"></a>在 NLB 叢集上部署報表伺服器的步驟

 您可以使用下列指導方針來安裝和設定部署：  
  
|步驟|Description|詳細資訊|  
|----------|-----------------|----------------------|  
|1|在 NLB 叢集的伺服器節點上安裝 Reporting Services 之前，請先檢查向外延展部署的需求。|《[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》中的[向外延展部署 - Reporting Services 原生模式 &#40;設定管理員&#41;](https://msdn.microsoft.com/library/4df38294-6f9d-4b40-9f03-1f01c1f0700c)|  
|2|設定 NLB 叢集並確認它是否正常運作。<br /><br /> 請務必將主機標頭名稱對應至 NLB 叢集的虛擬伺服器 IP。 此主機標頭名稱會用於報表伺服器 URL 中，而且比 IP 位址更容易記得和輸入。|如需詳細資訊，請參閱 Windows Server 產品文件集來了解您所執行的 Windows 作業系統版本。|  
|3|將主機標頭的 NetBIOS 和完整網域名稱 (FQDN) 加入至 Windows 登錄內儲存的 **BackConnectionHostNames** 清單。 使用 [KB 896861](https://support.microsoft.com/kb/896861) (https://support.microsoft.com/kb/896861) 中的**方法 2：指定主機名稱**，並進行下列調整。 KB 文章中的**步驟 7** 說「Quit Registry Editor, and then restart the IISAdmin service. (結束登錄編輯程式，然後重新啟動 IISAdmin 服務)。」 而不是將電腦重新開機以確認變更是否生效。<br /><br /> 例如，若主機標頭名稱 \<MyServer> 是 "contoso" 之 Windows 電腦名稱的虛擬名稱，您或許可以參考 FQDN 形式的 "contoso.domain.com"。 您需要將主機標頭名稱 (MyServer) 及 FQDN 名稱 (contoso.domain.com) 均加入 **BackConnectionHostNames**中的清單。|若您伺服器環境中包含本機電腦上的 NTLM 驗證，則必須執行此步驟，以建立回送連接。<br /><br /> 在此情況下，您將發現報表管理員與報表伺服器之間的要求會是失敗的 401 狀態 (未經授權)。|  
|4|在僅限檔案模式中，於已經屬於 NLB 叢集之一部分的節點上安裝 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ，並設定報表伺服器執行個體來進行向外延展部署。<br /><br /> 您所設定的向外延展可能不會回應導向虛擬伺服器 IP 的要求。 將向外延展設定為使用虛擬伺服器 IP 的作業會在您設定檢視狀態驗證之後的步驟進行。|[設定原生模式報表伺服器向外延展部署 &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/configure-a-native-mode-report-server-scale-out-deployment.md)|  
|5|設定檢視狀態驗證<br /><br /> 為了獲得最佳結果，請在您設定向外延展部署之後，而在將報表伺服器執行個體設定為使用虛擬伺服器 IP 之前，執行這個步驟。 先設定檢視狀態驗證，就可以在使用者嘗試存取互動式報表時，避免發生有關狀態驗證失敗的例外狀況。|本主題中的[如何設定檢視狀態驗證](#ViewState) 。|  
|6|將 **Hostname** 和 **UrlRoot** 設定為使用 NLB 叢集的虛擬伺服器 IP。|本主題中的[如何設定 Hostname 和 UrlRoot](#SpecifyingVirtualServerName) 。|  
|7|確認伺服器可透過您指定的主機名稱存取。|本主題中的[確認報表伺服器存取](#Verify) 。|  
  
## <a name="ViewState"></a> 如何設定檢視狀態驗證

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
若要在 NLB 叢集上執行向外延展部署，您必須設定檢視狀態驗證，好讓使用者可以檢視互動式 HTML 報表。  您必須針對報表伺服器 Web 服務執行這項工作。
::: moniker-end

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
若要在 NLB 叢集上執行向外延展部署，您必須設定檢視狀態驗證，好讓使用者可以檢視互動式 HTML 報表。
::: moniker-end
  
 檢視狀態驗證是由 ASP.NET 所控制。 依預設會啟用檢視狀態驗證，並使用 Web 服務的識別來執行驗證。 但是在 NLB 叢集案例中，會有多個服務執行個體和 Web 服務識別在不同的電腦上執行。 因為此服務識別會因每個節點而異，所以您不能依賴單一處理序識別來執行驗證。  
  
 為了解決此問題，您可以產生任意驗證金鑰來支援檢視狀態驗證，然後手動將每個報表伺服器節點設定為使用相同的金鑰。 您可以使用任何隨機產生的十六進位序列。 驗證演算法 (例如 SHA1) 會決定十六進位序列必須包含的長度。  

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"

1. 使用 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]提供的自動產生功能來產生驗證金鑰和解密金鑰。 最後，您必須擁有單一 <`MachineKey`> 項目，以針對向外延展部署中的每個報表伺服器執行個體貼入 Web.config 檔案中。  
  
    下列範例說明您必須取得的值。 請不要將此範例複製至設定檔，因為這些金鑰值無效。  
  
    ```xml
    <machineKey validationKey="123455555" decryptionKey="678999999" validation="SHA1" decryption="AES"/>  
    ```  
  
2. 開啟 Reportserver 的 Web.config 檔案，並在 <`system.web`> 區段中貼上您產生的 <`machineKey`> 項目。 根據預設，報表管理員的 Web.config 檔案位於 \Program Files\Microsoft SQL Server\MSRS13.MSSQLSERVER\Reporting Services\Reportserver\Web.config。  
  
3. 儲存檔案。  
  
4. 針對向外延展部署中的每個報表伺服器重複以上步驟。  
  
5. 確認 \Reporting Services\Reportserver 資料夾中的所有 Web.Config 檔案在 <`system.web`> 區段中包含相同的 <`machineKey`> 項目。  

::: moniker-end

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"

1. 使用 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]提供的自動產生功能來產生驗證金鑰和解密金鑰。 最後，您必須擁有單一 \<**MachineKey**> 項目，以便針對向外延展部署中的每個報表伺服器執行個體張貼到 RSReportServer.config 檔案中。

    下列範例說明您必須取得的值。 請勿將此範例複製到組態檔中，因為這些金鑰值是無效的。 報表伺服器需要正確的大小寫。

    ```xml
    <machineKey validationKey="123455555" decryptionKey="678999999" validation="SHA1" decryption="AES"/>
    ```

2. 儲存檔案。

3. 針對向外延展部署中的每個報表伺服器重複以上步驟。  

4. 請驗證 \Reporting Services\Report Server 資料夾中的所有 RSReportServer.config 檔案均包含相同的 \<**MachineKey**> 元素。

::: moniker-end

## <a name="SpecifyingVirtualServerName"></a> 如何設定 Hostname 和 UrlRoot

 若要在 NLB 叢集上設定報表伺服器向外延展部署，您必須定義單一虛擬伺服器名稱，以便提供伺服器叢集的單一存取點。 然後向您所在環境中的網域名稱伺服器 (DNS) 註冊這個虛擬伺服器名稱。  
  
 定義虛擬伺服器名稱之後，您必須在 RSReportServer.config 檔案中設定 **Hostname** 和 **UrlRoot** 屬性，以便將虛擬伺服器名稱包含在報表伺服器 URL 中。  
  
 當您在報表環境中使用萬用字元 URL 保留項目時，請設定 **Hostname** 屬性。 當您指定 **Hostname** 屬性作為 NLB 伺服器的虛擬伺服器名稱時，報表環境的網路流量會導向 NLB 伺服器。 然後 NLB 會將要求散發到報表伺服器節點。  
  
 另外，請設定 **UrlRoot** 屬性，好讓報表連結可以在已匯出到靜態報表的報表中工作 (例如 Excel 或 PDF 格式) 或是在訂閱所產生的報表中工作 (例如電子郵件訂閱)。  
  
 如果您將 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 與 [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] 3.0 或 [!INCLUDE[offSPServ](../../includes/offspserv-md.md)] 2007 整合，或是您在自訂 Web 應用程式中主控報表，您可能只需要設定 **UrlRoot** 屬性。 在此範例中，將 **UrlRoot** 屬性設定為 SharePoint 網站或 Web 應用程式的 URL。 這樣會將報表環境的網路流量導向可處理報表的應用程式，而不是報表伺服器或 NLB 叢集。  
  
 請不要修改 **ReportServerUrl**。 如果您修改這個 URL，就會在每次處理內部要求時增加虛擬伺服器之間的額外往返。 如需詳細資訊，請參閱[設定檔中的 URL &#40;SSRS 設定管理員&#41;](../../reporting-services/install-windows/urls-in-configuration-files-ssrs-configuration-manager.md)。 如需編輯設定檔的詳細資訊，請參閱《[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》中的[修改 Reporting Services 設定檔 &#40;RSreportserver.config&#41;](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)。  
  
1. 在文字編輯器中開啟 RSReportServer.config。  
  
2. 請尋找 **\<Service** 區段、將以下資訊新增至設定檔中，並以 NLB 伺服器的虛擬伺服器名稱取代 **Hostname** 值：  
  
    ```xml
    <Hostname>virtual_server</Hostname>  
    ```  
  
3. 尋找 **UrlRoot**。 雖然設定檔沒有指定這個項目，但是所使用預設值是採用下列格式的 URL： https:// 或 `https://<computername>/<reportserver>`，其中 \<*reportserver*> 是報表伺服器 Web 服務的虛擬目錄名稱。  
  
4. 鍵入 **UrlRoot** 的值，其中包括採用下列格式的叢集虛擬名稱： https:// 或 `https://<virtual_server>/<reportserver>`。  
  
5. 儲存檔案。  
  
6. 針對向外延展部署中的每個報表伺服器，在每個 RSReportServer.config 檔案中重複這些步驟。  
  
## <a name="Verify"></a> 確認報表伺服器存取

 確認您可以透過虛擬伺服器名稱存取向外延展部署 (例如，`https://MyVirtualServerName/reportserver` 和 `https://MyVirtualServerName/reports`)。  
  
 您可以查看報表伺服器記錄檔，或檢查 RS 執行記錄 (執行記錄資料表包含稱為 **InstanceName** 的資料行，它會顯示哪一個執行個體處理特定要求)，藉以檢查實際上是哪一個節點在處理報表。 如需詳細資訊，請參閱《 [線上叢書》中的](../../reporting-services/report-server/reporting-services-log-files-and-sources.md) Reporting Services 記錄檔和來源 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
 如果您無法連接到報表伺服器，請檢查 NLB 來確定要求有傳送到報表伺服器，並檢視報表伺服器 HTTP 記錄來確認伺服器正在接收要求。  
  
### <a name="troubleshooting-failed-requests"></a>疑難排解失敗的要求

 如果要求沒有送達報表伺服器執行個體，請檢查 RSReportServer.config 檔案來確認虛擬伺服器名稱是否指定為報表伺服器 URL 的主機名稱：  
  
1. 在文字編輯器中開啟 RSReportServer.config 檔。  
  
2. 尋找 \<**Hostname**>、\<**ReportServerUrl**> 和 \<**UrlRoot**>，並檢查每個設定的主機名稱。 如果此值不是您所預期的主機名稱，請將它取代成正確的主機名稱。  
  
 如果您於變更後再啟動 Reporting Services 設定工具，則該工具可能會將 \<**ReportServerUrl**> 設定變更成預設值。 一律保存組態檔的備份副本，以防您需要將它們取代成內含欲使用之設定的版本。  
  
## <a name="see-also"></a>另請參閱

 [Reporting Services 組態管理員 &#40;原生模式&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)   
 [設定 URL &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)   
 [設定原生模式報表伺服器向外延展部署 &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/configure-a-native-mode-report-server-scale-out-deployment.md)   
 [管理 Reporting Services 原生模式報表伺服器](../../reporting-services/report-server/manage-a-reporting-services-native-mode-report-server.md)