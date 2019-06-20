---
title: 編寫部署和管理工作的指令碼 | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- scripts [Reporting Services]
- moving reports
- report servers [Reporting Services], duplicating settings
- deploying [Reporting Services], scripts
- copying report server settings
- administrative tasks [Reporting Services]
- duplicating report server environment
- migrating reports [Reporting Services]
- scripts [Reporting Services], deployments
- transferrng reports
- reports [Reporting Services], migrating
ms.assetid: d0416c9e-e3f9-456d-9870-2cfd2c49039b
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d37a00e0a4fb71672f3bedcfc0e1651a7c42ce71
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66099707"
---
# <a name="script-deployment-and-administrative-tasks"></a>編寫部署和管理工作的指令碼
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 支援使用指令碼，以自動執行例行安裝、部署和管理工作。 部署報表伺服器是一個多步驟的程序， 您必須使用數個工具和程序來設定部署；並沒有單一程式或方法可用來自動化處理所有工作。  
  
 不是每一個步驟都應該自動化； 在某些情況下，手動執行步驟或是透過圖形工具是最簡單且最有效的方法。 例如，如果您想要部署大量的報表和模型，則複製報表伺服器資料庫要比撰寫程式碼來重新建立報表伺服器環境更為理想。  
  
 某些步驟需要自訂程式碼； 例如，只有當您撰寫自訂程式碼來呼叫報表伺服器 Windows Management Instrumentation (WMI) 提供者時，才可以讓 Web 服務和報表管理員的 URL 設定自動化。 如果您不想要撰寫程式碼，必須使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具來執行此步驟。  
  
 若要執行設定報表伺服器的指令碼，您必須是設定電腦上的本機管理員。 如需詳細資訊，請參閱 [設定報表伺服器來進行遠端管理](../report-server/configure-a-report-server-for-remote-administration.md)。  
  
 此主題描述自動化特定步驟的建議方法。 其中會提及數個程式和程式設計介面，此主題稍後會描述各程式和程式設計介面。  
  
## <a name="deployment-tasks-and-how-to-automate-them"></a>部署工作及自動化這些工作的方式  
 下表摘要列出部署報表伺服器所需的安裝和組態工作。 您可以使用這個表，比對特定的工作以及讓您自動化或自主 (Unattended) 執行工作的方法。  
  
|工作|方法|  
|----------|--------------|  
|安裝 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]。|您可以從命令列執行安裝程式，以執行自動安裝。<br /><br /> 只有當您指定預設組態選項，而且系統符合該安裝類型的所有需求時，才可以使用安裝程式來安裝及設定報表伺服器。 如果您無法安裝預設組態，必須執行僅限檔案的安裝。|  
|設定服務帳戶。|服務帳戶一開始是透過安裝程式設定的。 若要讓服務帳戶的變更當做安裝後工作自動化，您必須撰寫呼叫報表伺服器 WMI 提供者的自訂程式碼。 並沒有任何命令提示公用程式或指令碼範本可以使用程式設計方式設定服務帳戶。<br /><br /> 如果編碼需求讓您無法自動化這個步驟，您可以藉由執行 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具，以手動方式輕鬆地設定帳戶。 如需詳細資訊，請參閱[設定服務帳戶 &#40;SSRS 設定管理員&#41;](../../sql-server/install/configure-a-service-account-ssrs-configuration-manager.md)。|  
|設定報表伺服器 Web 服務與報表管理員 URL。|您必須撰寫自訂程式碼來呼叫報表伺服器 WMI 提供者。 並沒有任何命令列公用程式或指令碼範本可以用來設定 URL。<br /><br /> 如果您想要避免撰寫程式碼，您可以執行 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具手動設定 URL。 如需詳細資訊，請參閱[設定 URL &#40;SSRS 組態管理員&#41;](../install-windows/configure-a-url-ssrs-configuration-manager.md)。|  
|建立報表伺服器資料庫。|您必須撰寫自訂程式碼來呼叫報表伺服器 WMI 提供者。 並沒有任何命令提示公用程式或指令碼範本可以用來建立報表伺服器資料庫和 RSExecRole。<br /><br /> 如果您想要避免撰寫程式碼，您可以執行 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具手動建立資料庫。 如需詳細資訊，請參閱[建立原生模式報表伺服器資料庫 &#40;SSRS 設定管理員&#41;](../install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md)。|  
|設定報表伺服器資料庫連接。|如果您要變更連接字串、帳戶或密碼，或驗證類型，請執行 **rsconfig** 公用程式來設定連接。 如需詳細資訊，請參閱[設定報表伺服器資料庫連線 &#40;SSRS 設定管理員&#41;](../../sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md) 和 [rsconfig 公用程式 &#40;SSRS&#41;](rsconfig-utility-ssrs.md)。<br /><br /> 但是不能使用 rsconfig.exe 來建立或升級資料庫。 資料庫和 RSExecRole 必須已經存在。|  
|設定向外延展部署。|請從下列自動化向外延展部署的方法中進行選擇：<br /><br /> 執行 rskeymgmt.exe 公用程式，將報表伺服器執行個體聯結到現有的安裝。 如需詳細資訊，請參閱[新增和移除向外延展部署的加密金鑰 &#40;SSRS 設定管理員&#41;](../install-windows/add-and-remove-encryption-keys-for-scale-out-deployment.md)。<br /><br /> 撰寫可對報表伺服器 WMI 提供者執行的自訂程式碼。|  
|備份加密金鑰。|請從下列自動化加密金鑰備份的方法中進行選擇：<br /><br /> 執行 rskeymgmt.exe 公用程式來備份這些金鑰。 如需詳細資訊，請參閱 [備份與還原 Reporting Services 加密金鑰](../install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)。<br /><br /> 撰寫可對報表伺服器 WMI 提供者執行的自訂程式碼。|  
|設定報表伺服器電子郵件。|撰寫可對 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] WMI 提供者執行的自訂程式碼。 提供者支援電子郵件組態設定的子集。<br /><br /> 雖然 RSReportServer.config 檔案包含所有設定，但請不要以自動方式使用檔案。 亦即，請不要使用批次檔複製檔案到其他報表伺服器。 每個組態檔都包含適用於目前執行個體的值。 這些值對其他報表伺服器執行個體無效。<br /><br /> 如需有關設定的詳細資訊，請參閱[電子郵件傳遞設定報表伺服器&#40;SSRS 組態管理員&#41;](../../sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md)。|  
|設定自動執行帳戶。|請從下列讓自動處理帳戶組態自動化的方法中進行選擇：<br /><br /> 執行 rsconfig.exe 公用程式來設定此帳戶。 如需詳細資訊，請參閱[設定自動執行帳戶 &#40;SSRS 組態管理員&#41;](../install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)。<br /><br /> 撰寫可呼叫報表伺服器 WMI 提供者的自訂程式碼。|  
|在另一部報表伺服器上部署現有的內容，包括資料夾階層、角色指派、報表、訂閱、排程、資料來源和資源。|重新建立現有報表伺服器環境的最佳方式，就是將報表伺服器資料庫複製到新的報表伺服器執行個體。<br /><br /> 替代方式是撰寫以程式設計方式重新建立現有報表伺服器內容的自訂程式碼。 不過，請注意，訂閱、報表快照集和報表記錄不能以程式設計方式重新建立。<br /><br /> 某些部署會因為將這兩種技術一起使用而獲益 (也就是還原報表伺服器資料庫，然後執行會針對特定安裝而修改報表伺服器資料庫的自訂程式碼)。<br /><br /> 如需詳細的範例，請參閱＜ [在報表伺服器之間移轉內容的範例 Reporting Services rs.exe 指令碼](sample-reporting-services-rs-exe-script-to-copy-content-between-report-servers.md)＞。<br /><br /> 如需重新放置報表伺服器資料庫的詳細資訊，請參閱[將報表伺服器資料庫移至其他電腦 &#40;SSRS 原生模式&#41;](../report-server/moving-the-report-server-databases-to-another-computer-ssrs-native-mode.md)。 如需有關以程式設計方式建立報表伺服器環境的詳細資訊，請參閱本主題的「使用指令碼來移轉報表伺服器內容和資料夾」一節。|  
  
## <a name="tools-and-technologies-for-automating-server-deployment"></a>自動化伺服器部署的工具和技術  
 下列清單摘要列出可用來自動化部署和維護工作的程式與介面。  
  
-   安裝程式可以在自動模式中執行，以便安裝報表伺服器元件，有時也可以進行設定。 您必須使用「僅限檔案」安裝選項，才能讓安裝程式設定報表伺服器執行個體。  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] WMI 提供者和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 命令列公用程式可用於本機和遠端伺服器組態。  
  
     [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] WMI 提供者會公開類別、屬性和方法，讓您能夠設定 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安裝的所有層面，包括指定服務帳戶、設定 URL、建立及設定報表伺服器資料庫，或是設定報表伺服器以進行電子郵件傳遞。 您必須撰寫自訂程式碼或指令碼，才能使用 WMI 提供者。 如需詳細資訊，請參閱 [存取 Reporting Services WMI 提供者](access-the-reporting-services-wmi-provider.md)。  
  
     撰寫程式碼的替代方案是使用命令列公用程式 (rsconfig.exe 和 rskeymgmt.exe)， 您可以撰寫批次檔來執行這些公用程式， 這些公用程式可用來自動化某些組態工作，而不是所有組態工作。  
  
-   報表伺服器 Script Host 工具 (rs.exe) 可以執行您可能會撰寫的自訂 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 程式碼，以便重新建立現有內容，或是在報表伺服器之間移動現有內容。 當您使用這個方式時，會使用 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]撰寫指令碼，並將其另存為 .rss 檔案，然後在目標報表伺服器上使用 rs.exe 來執行此指令碼。 您所撰寫的指令碼可以呼叫報表伺服器 Web 服務的 SOAP 介面。 部署指令碼是使用這種方法所撰寫，因為它可讓您重新建立報表伺服器資料夾命名空間與內容，以及重新建立以角色為基礎的安全性。  
  
-   [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 版引進了適用於 SharePoint 整合模式的 PowerShell 指令程式。 您可以使用 PowerShell 設定和管理 SharePoint 整合。  如需詳細資訊，請參閱 [Reporting Services SharePoint 模式適用的 PowerShell Cmdlet](../powershell-cmdlets-for-reporting-services-sharepoint-mode.md)。  
  
## <a name="use-scripts-to-migrate-report-server-content-and-folders"></a>使用指令碼來移轉報表伺服器內容和資料夾  
 您可以撰寫指令碼來複製另一個報表伺服器執行個體上的報表伺服器環境。 部署指令碼通常是以 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 撰寫，然後使用報表伺服器 Script Host 公用程式處理。  
  
 如需詳細的範例，請參閱＜ [在報表伺服器之間移轉內容的範例 Reporting Services rs.exe 指令碼](sample-reporting-services-rs-exe-script-to-copy-content-between-report-servers.md)＞。  
  
 使用指令碼，即可將資料夾、共用資料來源、資源、報表、角色指派以及設定從一部伺服器複製到另一部伺服器。 您為某個報表伺服器執行個體撰寫一個指令碼，然後在另一部伺服器上執行此指令碼，以重新建立報表伺服器命名空間。 如果您的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 部署中有多個報表伺服器，可以分別在每一個伺服器上執行指令碼，以相同方式設定所有伺服器。  
  
 下列清單描述將報表從一部伺服器移轉到另一部伺服器的步驟。  
  
1.  將您的指令碼變數設定為來源報表伺服器的 URL。  
  
2.  使用 <xref:ReportService2010.ReportingService2010.GetItemDefinition%2A> 和 <xref:ReportService2010.ReportingService2010.GetProperties%2A> 方法，即可擷取報表的報表定義與屬性。  
  
3.  將 URL 設定為指向目的地伺服器。  
  
4.  使用 <xref:ReportService2010.ReportingService2010.CreateCatalogItem%2A> 方法，傳遞從 <xref:ReportService2010.ReportingService2010.GetProperties%2A> 傳回的屬性和 <xref:ReportService2010.ReportingService2010.GetItemDefinition%2A>。  
  
 藉由使用各種 get 與 create 方法的組合，您可以執行類似的步驟來移轉設定、資料夾、共用資料來源以及資源。 如需您可以使用之方法的詳細資訊，請參閱[技術參考 &#40;SSRS&#41;](../technical-reference-ssrs.md)。  
  
> [!NOTE]  
>  除非明確設定認證，否則指令碼便會利用執行指令碼之使用者的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 認證來執行。  
  
 如需如何格式化和執行指令碼檔案的詳細資訊，請參閱 [利用 rs.exe 公用程式與 Web 服務編寫指令碼](script-with-the-rs-exe-utility-and-the-web-service.md)。  
  
## <a name="using-scripts-to-set-server-properties"></a>使用指令碼來設定伺服器屬性  
 您可以撰寫在報表伺服器上設定系統屬性的指令碼。 下列 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] .NET 指令碼會示範設定屬性的一個方式。 這個範例會停用 RSClientPrint ActiveX 控制項，但是您可以用任何有效的屬性名稱和值來取代 `EnableClientPrinting` 和 `False`。 若要檢視完整的伺服器屬性清單，請參閱 [報表伺服器系統屬性](../report-server-web-service/net-framework/reporting-services-properties-report-server-system-properties.md)。  
  
 若要使用此指令碼，請將它儲存為 .rss 副檔名的檔案，然後使用 rs.exe 命令提示字元公用程式，在報表伺服器上執行這個檔案。 系統不會編譯此指令碼，所以不需要安裝 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]。 這個範例假設您具有主控報表伺服器之本機電腦的權限。 如果您不是在具有權限的帳戶之下登入，您必須透過其他命令列引數來指定帳戶資訊。 如需詳細資訊，請參閱 [RS.exe 公用程式 &#40;SSRS&#41;](rs-exe-utility-ssrs.md)。  
  
> [!TIP]  
>  如需詳細的範例，請參閱＜ [在報表伺服器之間移轉內容的範例 Reporting Services rs.exe 指令碼](sample-reporting-services-rs-exe-script-to-copy-content-between-report-servers.md)＞。  
  
```  
Public Sub Main()  
        Dim props(0) As [Property]  
        Dim setProp As New [Property]  
        setProp.Name = "EnableClientPrinting"  
        setProp.Value = "False"   
        props(0) = setProp  
        Try  
            rs.SetSystemProperties(props)  
        Catch ex As System.Web.Services.Protocols.SoapException  
            Console.Write(ex.Detail.InnerXml)  
        Catch e as Exception  
            Console.Write(e.Message)  
        End Try  
End Sub  
```  
  
## <a name="see-also"></a>另請參閱  
 [GenerateDatabaseCreationScript 方法 &#40;WMI MSReportServer_ConfigurationSetting&#41;](../wmi-provider-library-reference/configurationsetting-method-generatedatabasecreationscript.md)   
 [GenerateDatabaseRightsScript 方法 &#40;WMI MSReportServer_ConfigurationSetting&#41;](../wmi-provider-library-reference/configurationsetting-method-generatedatabaserightsscript.md)   
 [GenerateDatabaseUpgradeScript 方法 &#40;WMI MSReportServer_ConfigurationSetting&#41;](../wmi-provider-library-reference/configurationsetting-method-generatedatabaseupgradescript.md)   
 [從命令提示字元安裝 SQL Server 2014](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)   
 [安裝 Reporting Services 原生模式報表伺服器](../install-windows/install-reporting-services-native-mode-report-server.md)   
 [Reporting Services 報表伺服器 &#40;原生模式&#41;](../report-server/reporting-services-report-server-native-mode.md)   
 [報表伺服器命令提示字元公用程式 &#40;SSRS&#41;](report-server-command-prompt-utilities-ssrs.md)   
 [規劃 Reporting Services 和 Power View 瀏覽器支援&#40;Reporting Services 2014&#41;](../browser-support-for-reporting-services-and-power-view.md)   
 [Reporting Services 工具](reporting-services-tools.md)  
  
  
