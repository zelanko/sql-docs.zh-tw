---
title: 在網路負載平衡叢集上設定報表伺服器 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- report servers [Reporting Services], network load balancing
ms.assetid: 6bfa5698-de65-43c3-b940-044f41c162d3
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: bff66ca0f644f862b7cdcfb534b55c4e8ebdd888
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66104084"
---
# <a name="configure-a-report-server-on-a-network-load-balancing-cluster"></a>在網路負載平衡叢集上設定報表伺服器
  如果您要將報表伺服器向外延展設定為在網路負載平衡 (NLB) 叢集上執行，就必須進行下列動作：  
  
-   確定此 NLB 叢集可透過對應至虛擬伺服器 IP 位址的虛擬伺服器名稱存取。 虛擬伺服器名稱是必要的項目，如此您才能夠設定 NLB 叢集的單一進入點。 當您針對每個報表伺服器執行個體設定 URL 時，就會將此虛擬伺服器名稱指定為主機。  
  
-   設定檢視狀態驗證，以便支援互動式報表檢視。 為了回應使用者動作，互動式報表通常會在單一使用者工作階段期間轉譯許多次，以便視覺化全新或不同的資料。 透過設定檢視狀態驗證，不論哪一個報表伺服器服務實際的要求，接近程度都會保留在使用者工作階段中。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 不會提供用於向外延展部署的負載平衡或是用於透過共用 URL 定義單一存取點的功能。 您必須實作個別的軟體或硬體 NLB 叢集方案，以便支援 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 向外延展部署。  
  
 您可以將 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安裝在已經屬於 NLB 叢集之一部分的節點上，也可以先設定向外延展部署，然後再安裝叢集軟體。  
  
## <a name="steps-for-report-server-deployment-on-an-nlb-cluster"></a>在 NLB 叢集上部署報表伺服器的步驟  
 您可以使用下列指導方針來安裝和設定部署：  
  
|步驟|描述|詳細資訊|  
|----------|-----------------|----------------------|  
|1|在 NLB 叢集的伺服器節點上安裝 Reporting Services 之前，請先檢查向外延展部署的需求。|[設定原生模式報表伺服器向外延展部署&#40;SSRS 組態管理員&#41;](../install-windows/configure-a-native-mode-report-server-scale-out-deployment.md) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]線上叢書 》|  
|2|設定 NLB 叢集並確認它是否正常運作。<br /><br /> 請務必將主機標頭名稱對應至 NLB 叢集的虛擬伺服器 IP。 此主機標頭名稱會用於報表伺服器 URL 中，而且比 IP 位址更容易記得和輸入。|如需詳細資訊，請參閱 Windows Server 產品文件集來了解您所執行的 Windows 作業系統版本。|  
|3|將主機標頭的 NetBIOS 和完整網域名稱 (FQDN) 加入至 Windows 登錄內儲存的 **BackConnectionHostNames** 清單。 使用中的步驟**方法 2:指定主機名稱**中[KB 896861](https://support.microsoft.com/kb/896861) (https://support.microsoft.com/kb/896861) ，進行下列調整。 KB 文章中的**步驟 7** 說「Quit Registry Editor, and then restart the IISAdmin service. (結束登錄編輯程式，然後重新啟動 IISAdmin 服務)。」 而不是將電腦重新開機以確認變更是否生效。<br /><br /> 例如，若主機標頭名稱 \<MyServer> 是 "contoso" 之 Windows 電腦名稱的虛擬名稱，您或許可以參考 FQDN 形式的 "contoso.domain.com"。 您需要將主機標頭名稱 (MyServer) 及 FQDN 名稱 (contoso.domain.com) 均加入 **BackConnectionHostNames**中的清單。|若您伺服器環境中包含本機電腦上的 NTLM 驗證，則必須執行此步驟，以建立回送連接。<br /><br /> 在此情況下，您將發現報表管理員與報表伺服器之間的要求會是失敗的 401 狀態 (未經授權)。|  
|4|在僅限檔案模式中，於已經屬於 NLB 叢集之一部分的節點上安裝 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ，並設定報表伺服器執行個體來進行向外延展部署。<br /><br /> 您所設定的向外延展可能不會回應導向虛擬伺服器 IP 的要求。 將向外延展設定為使用虛擬伺服器 IP 的作業會在您設定檢視狀態驗證之後的步驟進行。|[設定原生模式報表伺服器向外延展部署 &#40;SSRS 組態管理員&#41;](../install-windows/configure-a-native-mode-report-server-scale-out-deployment.md)|  
|5|設定檢視狀態驗證<br /><br /> 為了獲得最佳結果，請在您設定向外延展部署之後，而在將報表伺服器執行個體設定為使用虛擬伺服器 IP 之前，執行這個步驟。 先設定檢視狀態驗證，就可以在使用者嘗試存取互動式報表時，避免發生有關狀態驗證失敗的例外狀況。|本主題中的[如何設定檢視狀態驗證](#ViewState) 。|  
|6|將 `Hostname` 和 `UrlRoot` 設定為使用 NLB 叢集的虛擬伺服器 IP。|本主題中的[如何設定 Hostname 和 UrlRoot](#SpecifyingVirtualServerName) 。|  
|7|確認伺服器可透過您指定的主機名稱存取。|本主題中的[確認報表伺服器存取](#Verify) 。|  
  
##  <a name="ViewState"></a> 如何設定檢視狀態驗證  
 若要在 NLB 叢集上執行向外延展部署，您必須設定檢視狀態驗證，好讓使用者可以檢視互動式 HTML 報表。 您必須針對報表伺服器和報表管理員執行這項工作。  
  
 檢視狀態驗證是由 ASP.NET 所控制。 依預設會啟用檢視狀態驗證，並使用 Web 服務的識別來執行驗證。 但是在 NLB 叢集案例中，會有多個服務執行個體和 Web 服務識別在不同的電腦上執行。 因為此服務識別會因每個節點而異，所以您不能依賴單一處理序識別來執行驗證。  
  
 為了解決此問題，您可以產生任意驗證金鑰來支援檢視狀態驗證，然後手動將每個報表伺服器節點設定為使用相同的金鑰。 您可以使用任何隨機產生的十六進位序列。 驗證演算法 (例如 SHA1) 會決定十六進位序列必須包含的長度。  
  
1.  使用 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]提供的自動產生功能來產生驗證金鑰和解密金鑰。 最後，您必須擁有單一 <`machineKey`> 項目，您可以將它貼到向外延展部署中每個報表管理員執行個體的 Web.config 檔案。  
  
     下列範例說明您必須取得的值。 請勿將此範例複製到組態檔中，因為這些金鑰值是無效的。  
  
    ```  
    <machineKey validationKey="123455555" decryptionKey="678999999" validation="SHA1" decryption="AES"/>  
    ```  
  
2.  開啟 Web.config 檔案，報表管理員，並在 <`system.web`> 區段中貼上 <`machineKey`> 您產生的項目。 根據預設，報表管理員的 Web.config 檔案位於 \Program Files\Microsoft SQL Server\MSRS10_50.MSSQLSERVER\Reporting Services\ReportManager\Web.config。  
  
3.  儲存檔案。  
  
4.  針對向外延展部署中的每個報表伺服器重複以上步驟。  
  
5.  確認 \Reporting Services\Report Manager 資料夾中的所有 Web.Config 檔案都包含相同 <`machineKey`> 元素中的 <`system.web`> 一節。  
  
##  <a name="SpecifyingVirtualServerName"></a> 如何設定 Hostname 和 UrlRoot  
 若要在 NLB 叢集上設定報表伺服器向外延展部署，您必須定義單一虛擬伺服器名稱，以便提供伺服器叢集的單一存取點。 然後向您所在環境中的網域名稱伺服器 (DNS) 註冊這個虛擬伺服器名稱。  
  
 定義虛擬伺服器名稱之後，您必須在 RSReportServer.config 檔案中設定 `Hostname` 和 `UrlRoot` 屬性，以便將虛擬伺服器名稱包含在報表伺服器 URL 中。  
  
 當您在報表環境中使用萬用字元 URL 保留項目時，請設定 `Hostname` 屬性。 當您指定 `Hostname` 屬性做為 NLB 伺服器的虛擬伺服器名稱時，報表環境的網路流量會導向 NLB 伺服器。 然後 NLB 會將要求散發到報表伺服器節點。  
  
 另外，請設定 `UrlRoot` 屬性，好讓報表連結可以在已匯出到靜態報表的報表中工作 (例如 Excel 或 PDF 格式) 或是在訂閱所產生的報表中工作 (例如電子郵件訂閱)。  
  
 如果您整合[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]具有[!INCLUDE[winSPServ](../../includes/winspserv-md.md)]3.0 或[!INCLUDE[offSPServ](../../includes/offspserv-md.md)]2007，或裝載您自訂的 Web 應用程式中的報表，您可能只需要設定`UrlRoot`屬性。 在此範例中，將 `UrlRoot` 屬性設定為 SharePoint 網站或 Web 應用程式的 URL。 這樣會將報表環境的網路流量導向可處理報表的應用程式，而不是報表伺服器或 NLB 叢集。  
  
 請勿修改 `ReportServerUrl`。 如果您修改這個 URL，就會在每次處理內部要求時增加虛擬伺服器之間的額外往返。 如需詳細資訊，請參閱[設定檔中的 URL &#40;SSRS 設定管理員&#41;](../install-windows/urls-in-configuration-files-ssrs-configuration-manager.md)。 如需編輯設定檔的詳細資訊，請參閱《[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》中的[修改 Reporting Services 設定檔 &#40;RSreportserver.config&#41;](modify-a-reporting-services-configuration-file-rsreportserver-config.md)。  
  
1.  在文字編輯器中開啟 RSReportServer.config。  
  
2.  尋找 **\<服務 >** 區段，然後將下列資訊新增至組態檔中，取代`Hostname`NLB 伺服器的虛擬伺服器名稱的值：  
  
    ```  
    <Hostname>virtual_server</Hostname>  
    ```  
  
3.  尋找 `UrlRoot`。 組態檔中，沒有指定的項目，但是所使用的預設值是採用此格式的 URL: http:// 或 https://\<*computername*>/\<*reportserver*>，其中\< *reportserver*> 是報表伺服器 Web 服務虛擬目錄名稱。  
  
4.  輸入的值`UrlRoot`，包括叢集中的虛擬名稱採用下列格式： http:// 或 https://\<*virtual_server*>/\<*reportserver*>。  
  
5.  儲存檔案。  
  
6.  針對向外延展部署中的每個報表伺服器，在每個 RSReportServer.config 檔案中重複這些步驟。  
  
##  <a name="Verify"></a> 確認報表伺服器存取  
 確認您可以透過虛擬伺服器名稱存取向外延展部署 (例如 https://MyVirtualServerName/reportserver 和 https://MyVirtualServerName/reports) 。  
  
 您可以查看報表伺服器記錄檔，或檢查 RS 執行記錄 (執行記錄資料表包含稱為 **InstanceName** 的資料行，它會顯示哪一個執行個體處理特定要求)，藉以檢查實際上是哪一個節點在處理報表。 如需詳細資訊，請參閱《 [線上叢書》中的](../report-server/reporting-services-log-files-and-sources.md) Reporting Services 記錄檔和來源 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
 如果您無法連接到報表伺服器，請檢查 NLB 來確定要求有傳送到報表伺服器，並檢視報表伺服器 HTTP 記錄來確認伺服器正在接收要求。  
  
#### <a name="troubleshooting-failed-requests"></a>疑難排解失敗的要求  
 如果要求沒有送達報表伺服器執行個體，請檢查 RSReportServer.config 檔案來確認虛擬伺服器名稱是否指定為報表伺服器 URL 的主機名稱：  
  
1.  在文字編輯器中開啟 RSReportServer.config 檔。  
  
2.  尋找 <`Hostname`>，<`ReportServerUrl`>，並 <`UrlRoot`>，並檢查每個設定的主機名稱。 如果此值不是您所預期的主機名稱，請將它取代成正確的主機名稱。  
  
 如果您進行這些變更之後啟動 Reporting Services 組態工具，此工具可能會變更 <`ReportServerUrl`> 設定為預設值。 一律保存組態檔的備份副本，以防您需要將它們取代成內含欲使用之設定的版本。  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 組態管理員 &#40;原生模式&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)   
 [設定 URL &#40;SSRS 組態管理員&#41;](../install-windows/configure-a-url-ssrs-configuration-manager.md)   
 [設定原生模式報表伺服器向外延展部署 &#40;SSRS 組態管理員&#41;](../install-windows/configure-a-native-mode-report-server-scale-out-deployment.md)   
 [管理 Reporting Services 原生模式報表伺服器](manage-a-reporting-services-native-mode-report-server.md)  
  
  
