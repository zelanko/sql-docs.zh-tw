---
title: RsReportServer.config 組態檔 | Microsoft Docs
ms.date: 06/12/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-server
ms.topic: conceptual
ms.assetid: 60e0a0b2-8a47-4eda-a5df-3e5e403dbdbc
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 4edaecf62a1f78c90954b60ff0c08ce462993dd3
ms.sourcegitcommit: 3daacc4198918d33179f595ba7cd4ccb2a13b3c0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/25/2018
ms.locfileid: "50020342"
---
# <a name="rsreportserverconfig-configuration-file"></a>RsReportServer.config 組態檔
[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]**RsReportServer.config** 檔案會儲存報表伺服器 Web 服務和背景處理所使用的設定。 所有 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 應用程式都是在讀取 RSReportServer.config 檔中儲存之組態設定的單一處理序中執行。 原生模式和 SharePoint 模式的報表伺服器都使用 RSReportServer.config，不過，這兩個模式不會使用組態檔中的所有相同設定。 SharePoint 模式版本的檔案較小，因為 SharePoint 模式的許多設定是儲存在 SharePoint 組態資料庫中，而不是檔案中。 本主題描述針對原生模式和 SharePoint 模式所安裝的預設組態檔，以及由組態檔控制的部分重要設定和行為。  

在 SharePoint 模式中，組態檔包含套用至該電腦上執行之所有服務應用程式執行個體的設定。 SharePoint 組態資料庫包含套用至特定服務應用程式的組態設定。 儲存在組態資料庫中且透過 SharePoint 管理頁面管理的設定，可能因每個 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務應用程式而有所不同。  
  
 設定在下列內容中出現的順序，是依據預設安裝的組態檔中出現的順序而定。 如需如何編輯此檔案的指示，請參閱 [修改 Reporting Services 組態檔 &#40;RSreportserver.config&#41;](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)。  
  
 
##  <a name="bkmk_file_location"></a> 檔案位置  

RSReportServer.config 位於下列資料夾，端視報表伺服器模式而定：  


  
### <a name="native-mode-report-server"></a>原生模式報表伺服器  

 
**[!INCLUDE[applies](../../includes/applies-md.md)]**  SQL Server 2016
```  
C:\Program Files\Microsoft SQL Server\MSRS13.MSSQLSERVER\Reporting Services\ReportServer  
```

**[!INCLUDE[applies](../../includes/applies-md.md)]** SQL Server Reporting Services 中的 Power BI 報表 2017 年 1 月技術預覽
```  
C:\Program Files\Microsoft SQL Server Reporting Services\RSServer\ReportServer
```  
  
### <a name="sharepoint-mode-report-server"></a>SharePoint 模式報表伺服器

> [!NOTE]
> SQL Server Reporting Services 中的 Power BI 報表 2017 年 1 月技術預覽未提供 SharePoint 整合模式。
  
```  
C:\Program Files\Common Files\Microsoft Shared\Web Server Extensions\15\WebServices\Reporting  
```  
 
如需編輯此檔案的詳細資訊，請參閱 [修改 Reporting Services 組態檔 &#40;RSreportserver.config&#41;](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)。  
  
##  <a name="bkmk_generalconfiguration"></a> 一般組態設定 (rsreportserver.config)  
 下表提供有關檔案第一個部分中顯示之一般組態設定的資訊。 設定會依其出現在組態檔的順序顯示。 資料表的最後一個資料行會指出此設定適用於原生模式的報表伺服器 **(N)** 、SharePoint 模式的報表伺服器 **(S)** ，還是兩者。  
  
> [!NOTE]  
>  在本主題中，「最大整數」是指 2147483647 的 INT_MAX 值。  如需詳細資訊，請參閱[整數限制](https://msdn.microsoft.com/library/296az74e\(v=vs.110\).aspx) (https://msdn.microsoft.com/library/296az74e(v=vs.110).aspx)。  
  
|設定|Description|[模式]|  
|-------------|-----------------|----------|  
|**Dsn**|將連接字串指定給主控報表伺服器資料庫的資料庫伺服器。 當您建立報表伺服器資料庫時，這個值會加密並加入至組態檔。 如果是 SharePoint，資料庫連接資訊會取自 SharePoint 組態資料庫。|N、S|  
|**ConnectionType**|指定報表伺服器用於連接到報表伺服器資料庫的認證類型。 有效值為 **Default** 和 **Impersonate**。 如果將報表伺服器設定為使用**登入或服務帳戶連接到報表伺服器資料庫，則會指定** Default [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 如果報表伺服器是使用 Windows 帳戶連接到報表伺服器資料庫，則會指定**Impersonate** 。|N|  
|**LogonUser, LogonDomain, LogonCred**|儲存報表伺服器用於連接至報表伺服器資料庫所使用之網域帳戶的網域、使用者名稱和密碼。 當報表伺服器連接設定使用網域帳戶時，會建立 **LogonUser**、 **LogonDomain**和 **LogonCred** 的值。 如需報表伺服器資料庫連接的詳細資訊，請參閱[設定報表伺服器資料庫連接 &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md)。|N|  
|**InstanceID**|報表伺服器執行個體的識別碼。 報表伺服器執行個體名稱以 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體名稱為基礎。 此值會指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體名稱。 根據預設，這個值為 **MSRS12***\<執行個體名稱>*。 請勿修改此設定。 以下為完整值的範例： `<InstanceId>MSRS13.MSSQLSERVER</InstanceId>`<br /><br /> 以下是 SharePoint 模式的範例：<br /><br /> `<InstanceId>MSRS12.@Sharepoint</InstanceId>`|N、S|  
|**InstallationID**|安裝程式建立之報表伺服器安裝的識別碼。 此值會設定為 GUID。 請勿修改此設定。|N|  
|**SecureConnectionLevel**|指定 Web 服務呼叫必須使用安全通訊端層 (SSL) 的程度。 這項設定同時用於報表伺服器 Web 服務和入口網站。 當您在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具中設定使用 HTTP 或 HTTPS 的 URL 時，就會設定這個值。 在 SQL Server 2008 R2 中，SecureConnectionLevel 會變成 on/off 開關。 對於 SQL Server 2008 R2 之前的版本，有效值範圍是從 0 到 3，其中 0 是最不安全的值。 如需詳細資訊，請參閱 [ConfigurationSetting 方法 - SetSecureConnectionLevel](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setsecureconnectionlevel.md)、[使用安全的 Web 服務方法](../../reporting-services/report-server-web-service/net-framework/using-secure-web-service-methods.md)和[在原生模式報表伺服器上設定 SSL 連線](../../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md)。|N、S|
|**DisableSecureFormsAuthenticationCookie**|預設值為 False。<br /><br /> 指定是否停用強制將表單和自訂驗證所使用的 Cookie 標記為安全。 從 SQL Server 2012 開始， [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 會自動將搭配自訂驗證延伸模組所使用的表單驗證 Cookie (在傳送給用戶端時) 標示為安全 Cookie。 藉由變更這個屬性，報表伺服器管理員和自訂安全性延伸模組作者可以還原成之前的行為，該行為可讓自訂安全性延伸模組作者判斷是否將 Cookie 標示為安全 Cookie。 建議針對表單驗證使用安全 Cookie，以防止網路探查和重新執行攻擊。|N|  
|**CleanupCycleMinutes**|指定一個時限 (分鐘)，超過此時限後，舊有的工作階段和過期的快照集，便會從報表伺服器資料庫中移除。 有效值範圍是從 0 到最大整數。 預設值是 10。 將值設定為 0，則會停用資料庫清除處理序。|N、S|  
|**MaxActiveReqForOneUser**|指定一個使用者同時可以處理的報表最大數目。 一旦達到限制，系統就會拒絕進一步的報表處理要求。 有效值為 1 到最大整數。 預設值是 20。<br /><br /> 請注意，大部分要求的處理速度很快，因此單一使用者不太可能同時擁有 20 個以上的開啟連接。 如果使用者同時開啟超過 15 個密集處理的報表，您可能需要增加此值。<br /><br /> 以 SharePoint 整合模式執行的報表伺服器會忽略這項設定。|N、S|  
|**MaxActiveReqForAnonymous**|指定可同時處理的匿名要求數目上限。 達到限制之後，系統就會拒絕進一步的處理要求。 有效值為 1 到最大整數。 預設值是 200。
|**DatabaseQueryTimeout**|指定一個時限 (秒)，超過此時限後，與報表伺服器資料庫的連接便會逾時。此值傳遞至 System.Data.SQLClient.SQLCommand.CommandTimeout 屬性。 有效值的範圍為 0 到 2147483647。 預設值是 120。 值為 0 會指定無限等候時間，因此不建議您這樣做。|N|  
|**AlertingCleanupCycleMinutes**|預設值是 20。<br /><br /> 判斷清除在警示資料庫中儲存之暫存資料的頻率。|S|  
|**AlertingDataCleanupMinutes**|預設值是 360。<br /><br /> 判斷用於建立或編輯警示定義的工作階段資料會在警示資料庫內保留多久。 預設為 6 小時。|S|  
|**AlertingExecutionLogCleanup**Minutes|預設值是 10080。<br /><br /> 判斷要保留警示執行記錄值多久。 預設值為 7 天。|S|  
|**AlertingMaxDataRetentionDays**|預設值是 180。<br /><br /> 判斷在警示的資料尚未變更時，要保留必要的警示資料多久來避免重複的警示訊息。|S|  
|**RunningRequestsScavengerCycle**|指定取消遺棄與過期要求的頻率。 此指定值的單位是秒。 有效值範圍是從 0 到最大整數。 預設值是 60。|N、S|  
|**RunningRequestsDbCycle**|指定報表伺服器評估執行中作業，以檢查作業是否超過報表執行逾時的頻率，以及何時在入口網站的 [管理作業] 頁面中，顯示執行中作業的資訊。 此指定值的單位是秒。 有效值的範圍為 0 到 2147483647。 預設值是 60。|N、S|  
|**RunningRequestsAge**|指定間隔秒數，超過此秒數後，執行中作業的狀態便會從新作業變更成執行中作業。 有效值的範圍為 0 到 2147483647。 預設值是 30。|N、S|  
|**MaxScheduleWait**|指定要求 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [下次執行時間] **時，報表伺服器 Windows 服務等候** Agent 服務更新排程的秒數。 有效值的範圍從 1 到 60。<br /><br /> 在預設組態檔中，MaxScheduleWait 會設為 **5**。<br /><br /> 如果報表伺服器找不到或無法讀取組態檔，則伺服器會將 MaxScheduleWait 預設為 1。|N、S|  
|**DisplayErrorLink**|指出錯誤發生時，是否顯示「 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 說明及支援」網站的連結。 此連結出現在錯誤訊息中。 使用者可以按一下此連結，以便開啟網站上的更新錯誤訊息內容。 有效值包括 **True** (預設值) 和 **False**。|N、S|  
|**WebServiceuseFileShareStorage**|指定是否將快取報表與暫存快照集 (報表伺服器 Web 服務為使用者工作階段持續時間所建立的)，儲存在檔案系統上。 有效值為 **True** 和 **False** (預設值)。 如果此值設定為 false，暫存資料會儲存在 reportservertempdb 資料庫中。|N、S|  
|**WatsonFlags**|指定針對向 [!INCLUDE[msCoName](../../includes/msconame-md.md)]報告的錯誤狀況要記錄多少資訊。<br /><br /> 0x0430 = 完整傾印<br /><br /> 0x0428 = 迷你傾印<br /><br /> 0x0002 = 無傾印|N、S|  
|**WatsonDumpOnExceptions**|指定您想要在錯誤記錄檔中報告的例外狀況清單。 這在您有重複發生的問題，而且想要利用傳送到 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 進行分析的資訊建立傾印時相當實用。 建立傾印會影響效能，因此只有在診斷問題時，才能變更這個設定。|N、S|  
|**WatsonDumpExcludeIfContainsExceptions**|指定您不想要在錯誤記錄檔中報告的例外狀況清單。 這在您要診斷問題，而且不想讓伺服器建立特定例外的傾印時相當實用。|N、S|  
  
##  <a name="bkmk_URLReservations"></a> URLReservations (RSReportServer.config 檔)  
 **URLReservations** 會針對目前的執行個體，定義報表伺服器 Web 服務及入口網站的 HTTP 存取。 當您設定報表伺服器時，URL 會保留並儲存在 HTTP.SYS 中。  
  
> [!WARNING]  
>  如果是 SharePoint 模式，便會在 SharePoint 管理中心設定 URL 保留項目。 如需詳細資訊，請參閱[設定備用存取對應(https://technet.microsoft.com/library/cc263208(office.12).aspx)](https://technet.microsoft.com/library/cc263208\(office.12\).aspx)。  
  
 請勿直接修改組態檔中的 URL 保留項目。 請務必使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員或報表伺服器 WMI 提供者建立或修改原生模式報表伺服器的 URL 保留項目。 如果您修改組態檔中的值，可能會損毀保留項目，因而導致執行階段發生伺服器錯誤，或將解除安裝本軟體時不會移除的遺棄保留項目留在 HTTP.SYS 中。 如需詳細資訊，請參閱[設定報表伺服器 URL &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md) 和[組態檔中的 URL &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/urls-in-configuration-files-ssrs-configuration-manager.md)。  
  
 **URLReservations** 是選擇性項目。 如果它不存在 RSReportServer.config 檔中，表示伺服器可能尚未設定。 如果您指定了此項目，就需要 **AccountName** 以外的所有子項目。  
  
 資料表的最後一個資料行會指出此設定適用於原生模式的報表伺服器 (N)、SharePoint 模式的報表伺服器 (S)，還是兩者。  
  
|設定|Description|[模式]|  
|-------------|-----------------|----------|  
|**應用程式**|包含 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 應用程式的設定。|N|  
|**名稱**|指定 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 應用程式。 有效值為 ReportServerWebService 或 ReportManager。|N|  
|**VirtualDirectory**|指定應用程式的虛擬目錄名稱。|N|  
|**URL**|包含應用程式的一或多個 URL 保留項目。|N|  
|**UrlString**|指定適用於 HTTP.SYS 的 URL 語法。 如需語法的詳細資訊，請參閱 [URL 保留項目語法 &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/url-reservation-syntax-ssrs-configuration-manager.md)。|N|  
|**AccountSid**|指定建立保留的 URL 時使用之帳戶的安全性識別碼 (SID)。 這應該是報表伺服器服務執行時使用的帳戶。 如果 SID 與服務帳戶不符，報表伺服器可能就無法接聽該 URL 的要求。|N|  
|**AccountName**|指定對應至 **AccountSid**的可讀取帳戶名稱。 雖然系統不會使用此設定，但是它會顯示在檔案中，讓您可以輕易地判斷用於 URL 保留項目的帳戶。|N|  
  
##  <a name="bkmk_Authentication"></a> Authentication (RSReportServer.config 檔)  
 **Authentication** 會指定報表伺服器所接受的一個或多個驗證類型。 預設設定和預設值是這個區段可用之設定和值的子集。 只有預設設定會自動加入。 若要加入其他設定，您必須使用文字編輯器，將元素結構加入至 RSReportServer.config 檔，然後設定其值。  
  
 預設值包括 **RSWindowsNegotiate** 和 **EnableAuthPersistance** 設為 **True** 的 **RSWindowsNTLM**：  
  
```  
   <Authentication>  
      <AuthenticationTypes>  
         <RSWindowsNegotiate/>  
         <RSWindowsNTLM/>  
      </AuthenticationTypes>  
      <EnableAuthPersistence>true</EnableAuthPersistence>  
   </Authentication>  
```  
  
 所有其他值都必須手動加入。 如需詳細資訊和範例，請參閱 [使用報表伺服器驗證](../../reporting-services/security/authentication-with-the-report-server.md)。  
  
 下表的最後一個資料行會指出此設定適用於原生模式的報表伺服器 (N)、SharePoint 模式的報表伺服器 (S)，還是兩者。  
  
|設定|Description|[模式]|  
|-------------|-----------------|----------|  
|**AuthenticationTypes**|指定一或多種驗證類型。 有效值為： **RSWindowsNegotiate**、 **RSWindowsKerberos**、 **RSWindowsNTLM**、 **RSWindowsBasic**和 **Custom**。<br /><br /> **RSWindows** 類型和 **Custom** 互斥。<br /><br /> **RSWindowsNegotiate**、 **RSWindowsKerberos**、 **RSWindowsNTLM**和 **RSWindowsBasic** 是累計的，而且可以一起使用，如本節前面的預設值範例所示。<br /><br /> 如果您預期會收到來自各種使用不同驗證類型之用戶端應用程式或瀏覽器的要求，指定多種驗證類型就是必要的做法。<br /><br /> 請勿移除 **RSWindowsNTLM**，否則瀏覽器支援會限制在部分支援的瀏覽器類型。 如需詳細資訊，請參閱 [Reporting Services 和 Power View 的瀏覽器支援](../../reporting-services/browser-support-for-reporting-services-and-power-view.md)。|N|  
|**RSWindowsNegotiate**|報表伺服器接受 Kerberos 或 NTLM 安全性 Token。 當報表伺服器在原生模式下執行，而且服務帳戶為網路服務時，此為預設值。 當報表伺服器在原生模式下執行，而且服務帳戶設定成網域使用者帳戶時，會省略此設定。<br /><br /> 如果網域帳戶設定成報表伺服器服務帳戶，而且服務主要名稱 (SPN) 未設定成報表伺服器，此設定可能會防止使用者登入伺服器。|N|  
|**EnableAuthPersistance**|伺服器接受 NTLM 安全性 Token。<br /><br /> 如果您移除此設定，瀏覽器支援會受到某些支援之瀏覽器類型的限制。 如需詳細資訊，請參閱 [Reporting Services 和 Power View 的瀏覽器支援](../../reporting-services/browser-support-for-reporting-services-and-power-view.md)。|N、S|  
|**RSWindowsKerberos**|伺服器接受 Kerberos 安全性 Token。<br /><br /> 當您在限制委派驗證配置中使用 Kerberos 驗證時，請使用此設定或 RSWindowsNegotiate。|N|  
|**RSWindowsBasic**|不使用認證建立連線時，伺服器會接受基本認證並發出挑戰/回應。<br /><br /> 基本驗證會以清楚的文字，將認證傳入 HTTP 要求中。 如果您使用基本驗證，請使用 SSL 加密進出報表伺服器的網路流量。 若要檢視 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]中基本驗證的範例組態語法，請參閱 [使用報表伺服器驗證](../../reporting-services/security/authentication-with-the-report-server.md)。|N|  
|**Custom**|如果您在報表伺服器電腦上部署了自訂安全性延伸模組，請指定這個值。 如需詳細資訊，請參閱＜ [Implementing a Security Extension](../../reporting-services/extensions/security-extension/implementing-a-security-extension.md)＞。|N|  
|**LogonMethod**|這個值會指定 **RSWindowsBasic**的登入類型。 如果您指定了 **RSWindowsBasic**，這個值就是必要項目。 有效值為 2 或 3，其中每個值代表下列項目：<br /><br /> **2** = 網路登入，用於驗證純文字密碼的高效能伺服器<br /><br /> **3** = 純文字登入，可將登入認證保存在隨著每個 HTTP 要求傳送的驗證封裝中，以便在連接至網路中的其他伺服器時，允許伺服器模擬使用者。<br /><br /> <br /><br /> 注意： [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)]中不支援值 0 (用於互動式登入) 和 1 (用於批次登入)。|N|  
|**Realm**|這個值是用於 **RSWindowsBasic**。 它會指定資源分割區，其中包含用於控制組織中受保護資源之存取權的授權和驗證功能。|N|  
|**DefaultDomain**|這個值是用於 **RSWindowsBasic**。 它可用於決定伺服器用以驗證使用者的網域。 雖然這個值是選擇性的，但是如果您省略它，報表伺服器將使用電腦名稱當做網域。 如果您在網域控制站上安裝了報表伺服器，則使用的網域就是電腦所控制的網域。|N|  
|**RSWindowsExtendedProtectionLevel**|預設值是 **off**。 如需詳細資訊，請參閱＜ [Extended Protection for Authentication with Reporting Services](../../reporting-services/security/extended-protection-for-authentication-with-reporting-services.md)＞|N|  
|**RSWindowsExtendedProtectionScenario**|The default value is <bpt id="p1">**</bpt>Proxy<ept id="p1">**</ept>|N|  
|**EnableAuthPersistence**|決定要在連接時或針對每個要求執行驗證。<br /><br /> 有效值為 **True** (預設值) 或 **False**。 如果設定為 **True**，來自相同連接的後續要求就會採用第一個要求的模擬內容。<br /><br /> 如果您正使用 Proxy 伺服器軟體 (例如 ISA Server) 來存取報表伺服器，這個值就必須設定為 **False** 。 使用 Proxy 伺服器可讓多位使用者使用 Proxy 伺服器的單一連接。 在這個狀況中，您應該停用驗證持續性機制，以便個別驗證每個使用者要求。 如果您沒有將 **EnableAuthPersistence** 設定為 **False**，則所有使用者都將使用第一個要求的模擬內容來進行連接。|N、S|  
  
##  <a name="bkmk_service"></a> Service (RSReportServer.config 檔)  
 **Service** 會指定以整體方式套用至服務的應用程式設定。  
  
 下表的最後一個資料行會指出此設定適用於原生模式的報表伺服器 (N)、SharePoint 模式的報表伺服器 (S)，還是兩者。  
  
|設定|Description|[模式]|  
|-------------|-----------------|----------|  
|**IsSchedulingService**|指定報表伺服器是否要維護一組對應到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用者所建立之排程與訂閱的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Agent 作業。 有效值包括 **True** (預設值) 和 **False**。<br /><br /> 當您使用原則式管理的 [Reporting Services 的介面區組態] Facet 來啟用或停用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 功能時，這個設定會受到影響。 如需詳細資訊，請參閱 [啟動與停止報表伺服器服務](../../reporting-services/report-server/start-and-stop-the-report-server-service.md)。|N、S|  
|**IsNotificationService**|指定報表伺服器是否處理通知和傳遞。 有效值包括 **True** (預設值) 和 **False**。 當值為 **False**時，不會傳遞訂閱。<br /><br /> 當您使用原則式管理的 [Reporting Services 的介面區組態] Facet 來啟用或停用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 功能時，這個設定會受到影響。 如需詳細資訊，請參閱 [啟動與停止報表伺服器服務](../../reporting-services/report-server/start-and-stop-the-report-server-service.md)。|N、S|  
|**IsEventService**|指定服務處理序事件是否位於事件佇列中。 有效值包括 **True** (預設值) 和 **False**。 當值為 **False**時，報表伺服器不會執行排程或訂閱的作業。<br /><br /> 當您使用原則式管理的 [Reporting Services 的介面區組態] Facet 來啟用或停用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 功能時，這個設定會受到影響。 如需詳細資訊，請參閱 [啟動與停止報表伺服器服務](../../reporting-services/report-server/start-and-stop-the-report-server-service.md)。|N、S|  
|**IsAlertingService**|預設值為 **True**|S|  
|**PollingInterval**|指定報表伺服器之事件資料表輪詢的間隔 (以秒計)。 有效值範圍是從 0 到最大整數。 預設值是 10。|N、S|  
|**WindowsServiceUseFileShareStorage**|指定是否將快取報表與暫存快照集 (報表伺服器服務為使用者工作階段持續時間所建立) 儲存在檔案系統上。 有效值為 **True** 和 **False** (預設值)。|N、S|  
|**MemorySafetyMargin**|指定 **WorkingSetMaximum** 的百分比，以便定義中度與低度壓力狀況之間的界限。 預設值是 80。 如需 **WorkingSetMaximum** 和設定可用記憶體的詳細資訊，請參閱 [設定報表伺服器應用程式的可用記憶體](../../reporting-services/report-server/configure-available-memory-for-report-server-applications.md)。|N、S|  
|**MemoryThreshold**|指定 **WorkingSetMaximum** 的百分比，以便定義高度與中度壓力狀況之間的界限。 預設值是 **90**。 此值應該大於針對 **MemorySafetyMargin**所設定的值。 如需詳細資訊，請參閱 [設定報表伺服器應用程式的可用記憶體](../../reporting-services/report-server/configure-available-memory-for-report-server-applications.md)。|N、S|  
|**RecycleTime**|指定應用程式網域的回收時間，以分鐘測量。 有效值範圍是從 0 到最大整數。 預設值是 720。|N、S|  
|**MaxAppDomainUnloadTime**|指定在回收作業過程中，允許應用程式網域卸載的時間間隔。 如果回收未在此時間週期內完成，應用程式網域中的所有處理都會停止。 如需詳細資訊，請參閱＜ [Application Domains for Report Server Applications](../../reporting-services/report-server/application-domains-for-report-server-applications.md)＞。<br /><br /> 此值的單位是分鐘。 有效值範圍是從 0 到最大整數。 預設值是 **30**。|N、S|  
|**MaxQueueThreads**|指定報表伺服器 Windows 服務用於同時處理訂閱和通知的執行緒數目。 有效值範圍是從 0 到最大整數。 預設值是 0。 如果您選擇 0，則報表伺服器會決定最大的執行緒數目。 如果您指定整數，您所指定的值會設定一次可以建立的執行緒數目上限。 如需報表伺服器 Windows 服務如何管理記憶體來執行處理的詳細資訊，請參閱 [設定報表伺服器應用程式的可用記憶體](../../reporting-services/report-server/configure-available-memory-for-report-server-applications.md)。|N、S|  
|**UrlRoot**|報表伺服器傳遞延伸模組所使用，用於撰寫以電子郵件和檔案共用訂閱傳遞之報表所使用的 URL。 此值必須是可從中存取已發行報表之報表伺服器的有效 URL 位址。 報表伺服器所使用，用於產生離線或自動存取的 URL。 這些 URL 會在匯出的報表中，由傳遞延伸模組所使用，用於撰寫包含在傳遞訊息中的 URL，例如電子郵件中的連結。 報表伺服器會根據下列行為，決定報表中的 URL：<br /><br /> 當 **UrlRoot** 是空的 (預設值)，而且有 URL 保留項目時，報表伺服器會自動以針對 ListReportServerUrls 方法產生 URL 的相同方式決定 URL。 系統會使用 ListReportServerUrls 方法所傳回第一個 URL。 或者，如果 SecureConnectionLevel 大於零 (0)，則會使用第一個 SSL URL。<br /><br /> 當 **UrlRoot** 設定為特定的值時，系統會使用明確值。<br /><br /> 當 **UrlRoot** 是空的，而且沒有設定任何 URL 保留項目時，轉譯報表與電子郵件連結中的 URL 會不正確。|N、S|  
|**UnattendedExecutionAccount**|指定報表伺服器為執行報表所使用的使用者名稱、密碼和網域。 這些值經過加密。 使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具或 **rsconfig** 公用程式即可設定這些值。 如需詳細資訊，請參閱[設定自動執行帳戶 &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)。<br /><br /> SharePoint 模式中，您集合執行帳戶的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務應用程式使用 SharePoint 集中管理。 如需詳細資訊，請參閱 [管理 Reporting Services SharePoint 服務應用程式](../../reporting-services/report-server-sharepoint/manage-a-reporting-services-sharepoint-service-application.md)|N|  
|**PolicyLevel**|指定安全性原則組態檔。 有效的值為 Rssrvrpolicy.config。如需詳細資訊，請參閱＜ [Using Reporting Services Security Policy Files](../../reporting-services/extensions/secure-development/using-reporting-services-security-policy-files.md)＞。|N、S|  
|**IsWebServiceEnabled**|指定報表伺服器 Web 服務是否回應 SOAP 與 URL 存取要求。 當您使用原則型式管理的 [Reporting Services 的介面區組態] Facet 來啟用或停用服務時，將會設定這個值。|N、S|  
|**IsReportManagerEnabled**|此設定已在 SQL Server 2016 Reporting Services 累積更新 2 之後淘汰。 入口網站會一律啟用。|N|  
|**FileShareStorageLocation**|指定檔案系統上儲存暫存快照集的單一資料夾。 雖然您可以將資料夾路徑指定為 UNC 路徑，但是不建議您這麼做。 預設值為空白。<br /><br /> `<FileShareStorageLocation>`<br /><br /> `<Path>`<br /><br /> `</Path>`<br /><br /> `</FileShareStorageLocation>`|N、S|  
|**IsRdceEnabled**|指定是否啟用報表定義自訂延伸模組 (RDCE)。 有效值為 **True** 和 **False**。|N、S|  
  
##  <a name="bkmk_UI"></a> UI (RSReportServer.config 檔)  
 **UI** 會指定套用至入口網站應用程式的組態設定。  
  
 下表的最後一個資料行會指出此設定適用於原生模式的報表伺服器 (N)、SharePoint 模式的報表伺服器 (S)，還是兩者。  
  
|設定|Description|[模式]|  
|-------------|-----------------|----------|  
|**ReportServerUrl**|指定入口網站對其建立連線的報表伺服器 URL。 只有當您要將入口網站設定成連接線另一個執行個體或遠端電腦中的報表伺服器時，才應該修改這個值。|N、S|  
|**ReportBuilderTrustLevel**|請勿修改這個值，因為它是無法設定的。 在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 和更新版本中，報表產生器只能以 **FullTrust**執行。 如需停用部分信任模式的詳細資訊，請參閱 [SQL Server 2016 中 SQL Server Reporting Services 已停止的功能](../../reporting-services/discontinued-functionality-to-sql-server-reporting-services-in-sql-server.md)。|N、S|  
|**PageCountMode**|(僅適用於入口網站) 這項設定會指定報表伺服器要在轉譯報表之前或檢視報表時計算頁面計數值。 有效值為 **Estimate** (預設值) 和 **Actual**。 在使用者檢視報表時，請使用 **Estimate** 來計算頁面計數資訊。 起初，頁面計數設定為 2 (代表目前的頁面加上一個額外頁面)，但是會隨著使用者在報表中逐次翻頁而向上調整。 如果您想要在顯示報表之前預先計算頁面計數，請使用 **Actual** 。 提供**Actual** 的目的，是為了與舊版相容。 請注意，如果您將 **PageCountMode** 設定為 **Actual**，則系統必須處理整份報表才能取得有效的頁面計數，因而增加顯示報表之前的等候時間。|N、S|  
  
##  <a name="bkmk_extensions"></a> 延伸模組 (RSReportServer.config 檔) 原生模式  
 ＜延伸模組＞一節會出現在 **僅適用於原生模式** 報表伺服器的 rsreportserver.config 檔案中。 SharePoint 模式報表伺服器的延伸模組資訊儲存在 SharePoint 組態資料庫中，而且會針對每個 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務應用程式設定。  
  
 **Extensions** 會針對 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安裝的下列可延伸模組指定組態設定：  
  
-   傳遞延伸模組  
  
-   DeliveryUI 延伸模組  
  
-   轉譯延伸模組  
  
-   資料處理延伸模組  
  
-   語意查詢延伸模組 (僅供內部使用)  
  
-   模型產生延伸模組 (僅供內部使用)  
  
-   安全性延伸模組  
  
-   驗證延伸模組  
  
-   事件處理延伸模組 (僅供內部使用)  
  
-   報表定義自訂延伸模組  
  
 其中某些延伸模組僅供報表伺服器內部使用。 僅供內部使用之延伸模組的組態設定沒有記載。 下列各節描述預設延伸模組的組態設定。 如果您要使用具有自訂延伸模組的報表伺服器，組態檔可能會包含此處未描述的設定。 本節將依據顯示的順序列出這些延伸模組。 針對相同延伸模組類型之多個執行個體重複出現的設定只會描述一次。  
  
###  <a name="bkmk_extensionsgeneral"></a> 傳遞延伸模組一般組態  
 指定透過訂閱傳遞報表所使用的預設 (也可能是自訂的) 傳遞延伸模組。 RSReportServer.config 檔案包含四個傳遞延伸模組的應用程式設定：  
  
1.  報表伺服器電子郵件  
  
2.  檔案共用傳遞。  
  
3.  報表伺服器文件庫用於在 SharePoint 整合模式下執行的報表伺服器。  
  
4.  Null 傳遞提供者用於預先載入報表快取。  
  
 如需傳遞延伸模組的詳細資訊，請參閱[訂閱與傳遞 &#40;Reporting Services&#41;](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)  
  
 所有傳遞延伸模組都具有 **Extension Name**、 **MaxRetries**、 **SecondsBeforeRetry**和 **Configuration**。 這些共用設定會優先記載。 延伸模組特有設定的描述接著列於第二個表格中。  
  
|設定|Description|  
|-------------|-----------------|  
|**Extension Name**|指定傳遞延伸模組的易記名稱和組件。 請勿修改此值。|  
|**MaxRetries**|指定報表伺服器將重試傳遞的次數 (如果第一次嘗試不成功的話)。 預設值是 3。|  
|**SecondsBeforeRetry**|指定每次重試嘗試之間的時間間隔 (以秒為單位)。 預設值是 900。|  
|**Configuration**|包含每個傳遞延伸模組專用的組態設定。|  
  
####  <a name="bkmk_fileshare_extension"></a> 檔案共用傳遞延伸模組組態設定  
 檔案共用傳遞會將已經匯出成應用程式檔案格式的報表傳送至網路上的共用資料夾。 如需詳細資訊，請參閱＜ [File Share Delivery in Reporting Services](../../reporting-services/subscriptions/file-share-delivery-in-reporting-services.md)＞。  
  
|設定|Description|  
|-------------|-----------------|  
|**ExcludedRenderFormats**、 **RenderingExtension**|這些設定是用於刻意排除無法搭配檔案共用傳遞使用的匯出格式。 這些格式通常用於互動式報表、預覽或預先載入報表快取。 它們不會產生可輕易地從桌上型電腦應用程式中檢視的應用程式檔案。<br /><br /> HTMLOWC<br /><br /> RGDI<br /><br /> [Null]|  
  
####  <a name="bkmk_email_extension"></a> 報表伺服器電子郵件延伸模組組態設定  
 報表伺服器電子郵件會使用 SMTP 網路裝置，將報表傳送至電子郵件地址。 您必須先設定這個傳遞延伸模組，然後才能使用它。 如需詳細資訊，請參閱 [為電子郵件傳遞設定報表伺服器 (SSRS 組態管理員)](https://msdn.microsoft.com/b838f970-d11a-4239-b164-8d11f4581d83) 和 [Reporting Services 中的電子郵件傳遞](../../reporting-services/subscriptions/e-mail-delivery-in-reporting-services.md)。  
  
|設定|Description|  
|-------------|-----------------|  
|**SMTPServer**|指定表示遠端 SMTP 伺服器或轉送器位址的字串值。 遠端 SMTP 服務需要此值。 這可以是 IP 位址、您公司內部網路上電腦的 UNC 名稱，或者完整網域名稱。|  
|**SMTPServerPort**|指定一個整數值，表示 SMTP 服務用於傳送外寄郵件的通訊埠。 通常使用通訊埠 25 來傳送電子郵件。|  
|**SMTPAccountName**|包含指派 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Outlook Express 帳戶名稱的字串值。 如果您的 SMTP 伺服器設定來做某些用途，您可以設定此值；否則可以將它保留空白。 使用 [寄件者]，以指定用於傳送報表的電子郵件帳戶。|  
|**SMTPConnectionTimeout**|指定表示有效通訊端在連接到 SMTP 服務逾時前，所等待之秒數的整數值。預設值是 30 秒，但是如果 **SendUsing** 設定為 2，就會忽略此值。|  
|**SMTPServerPickupDirectory**|指定表示本機 SMTP 服務收取目錄的字串值。 此值必須是完整本機資料夾路徑 (例如，d:\rs-emails)。|  
|**SMTPUseSSL**|指定可以設定在透過網路傳送 SMTP 訊息時，使用安全通訊端層 (SSL) 的布林值。 預設值是 0 (或 False)。 當 **[SendUsing]** 元素設定為 2 時，可使用此設定。|  
|**SendUsing**|指定用於傳送訊息的方法。 有效值為：<br /><br /> 1=從本機 SMTP 服務收取目錄傳送訊息。<br /><br /> 2=從網路 SMTP 服務傳送訊息。|  
|**SMTPAuthenticate**|指定表示在透過 TCP/IP 連接傳送訊息到 SMTP 服務時，要使用之驗證種類的整數值。 有效值為：<br /><br /> 0=無驗證。<br /><br /> 1= (不支援)。<br /><br /> 2= NTLM (NT LanMan) 驗證。 使用報表伺服器 Windows 服務的安全性內容，連接到網路 SMTP 伺服器。|  
|**來源**|以 *abc@host.xyz*。 地址會在外寄電子郵件訊息的 [寄件者] 行上出現。 如果您使用的是遠端 SMTP 伺服器，則此值是必要的。 它應該是擁有傳送郵件之權限的有效電子郵件帳戶。|  
|**EmbeddedRenderFormats、RenderingExtension**|指定用於將報表封裝在電子郵件訊息之主體中的轉譯格式。 報表中的影像會後續內嵌在報表中。 有效值為 MHTML 和 HTML4.0。|  
|**PrivilegedUserRenderFormats**|指定透過「管理所有訂閱」工作啟用訂閱時，使用者可以從報表訂閱選取的轉譯格式。 如果未設定此值，就可以使用所有未刻意排除的轉譯格式。|  
|**ExcludedRenderFormats、RenderingExtension**|刻意排除與給定傳遞延伸模組配合不良的格式。 您無法排除同一個轉譯延伸模組的多個執行個體， 如果您排除多個執行個體，就會在報表伺服器讀取組態檔時產生錯誤。 預設會排除用於電子郵件傳遞的下列延伸模組：<br /><br /> HTMLOWC<br /><br /> [Null]<br /><br /> RGDI|  
|**SendEmailToUserAlias**|此值使用 **DefaultHostName**。<br /><br /> 如果 **SendEmailToUserAlias** 設定為 **True**，就會自動將定義個別訂閱的使用者指定為報表的收件者。 **[收件者]** 欄位是隱藏的。 如果值為 **False**，則看得到 [收件者]  欄位。 如果您希望充分控制報表散發，請將此值設定為 **True** 。 有效值包括下列各項：<br /><br /> **True**=使用建立訂閱之使用者的電子郵件地址。 這是預設值。<br /><br /> **False**=可以指定任何電子郵件地址。|  
|**DefaultHostName**|此值使用 **SendEmailToUserAlias**。<br /><br /> 指定當 **SendEmailToUserAlias** 設定為 true 時，表示附加到使用者別名之主機名稱的字串值。 此值可以是網域名稱系統 (DNS) 名稱或 IP 位址。|  
|**PermittedHosts**|藉由明確地指定哪些主機可以接收電子郵件傳遞，來限制報表散發。 **PermittedHosts**中，將每個主機指定為一個 **HostName** 元素，其值為 IP 位址或 DNS 名稱。<br /><br /> 只有主機所定義的電子郵件帳戶為有效收件者。 如果您指定 **DefaultHostName**，務必要將該主機包含為 **PermittedHosts** 的 **HostName**元素。 此值必須是一或多個 DNS 名稱或 IP 位址。 依預設，未設定此值。 如果未設定此值，便不限制誰可以接收電子郵件報表。|  
  
####  <a name="bkmk_documentlibrary_extension"></a> 報表伺服器 SharePoint 文件庫延伸模組組態  
 報表伺服器文件庫會將已經匯出成應用程式檔案格式的報表傳送至文件庫。 只有設定為在 SharePoint 整合模式中執行的報表伺服器可以使用這個傳遞延伸模組。 如需詳細資訊，請參閱＜ [SharePoint Library Delivery in Reporting Services](../../reporting-services/subscriptions/sharepoint-library-delivery-in-reporting-services.md)＞。  
  
|設定|Description|  
|-------------|-----------------|  
|**ExcludedRenderFormats、RenderingExtension**|這些設定是用於刻意排除無法搭配文件庫傳遞使用的匯出格式。 系統會排除 HTMLOWC、RGDI 和 Null 傳遞延伸模組。 這些格式通常用於互動式報表、預覽或預先載入報表快取。 它們不會產生可輕易地從桌上型電腦應用程式中檢視的應用程式檔案。|  
  
####  <a name="bkmk_null_extension"></a> NULL 傳遞延伸模組組態  
 NULL 傳遞提供者是用於預先載入含有個別使用者之預先產生報表的快取。 這個傳遞延伸模組沒有任何組態設定。 如需詳細資訊，請參閱 [快取報表 &#40;SSRS&#41;](../../reporting-services/report-server/caching-reports-ssrs.md)的版本中預先載入快取的唯一方法。  
  
###  <a name="bkmk_ui"></a> 傳遞 UI 延伸模組一般組態  
 指定包含使用者介面元件的傳遞延伸模組，而該元件會顯示於在入口網站中定義個別訂閱時使用的訂閱定義頁面中。 如果您建立並部署具有使用者定義選項的自訂傳遞延伸模組，而且您想要使用入口網站，就必須在這個區段中註冊該傳遞延伸模組。 根據預設，報表伺服器電子郵件和報表伺服器檔案共用都具有組態設定。 只在資料驅動訂閱或 SharePoint 應用程式頁面中使用的傳遞延伸模組沒有此區段的設定。  
  
|設定|Description|  
|-------------|-----------------|  
|**DefaultDeliveryExtension**|此設定會決定會先顯示在訂閱定義頁面之傳遞類型清單中的傳遞延伸模組。 只有一個傳遞延伸模組可以包含這項設定。 有效值包括 **True** 或 **False**。 當此值設定為 **True**時，表示該延伸模組為預設選取項目。|  
|**Configuration**|指定傳遞延伸模組的組態選項。 您可以針對每一個傳遞延伸模組設定預設轉譯格式。 有效值是在 rsreportserver.config 檔案的轉譯區段中，所註明的轉譯延伸模組名稱。|  
|**DefaultRenderingExtension**|指定傳遞延伸模組是否為預設值。 報表伺服器電子郵件是預設的傳遞延伸模組。 有效值包括 **True** 或 **False**。 如果有多個延伸模組包含 **True**值，就會將第一個延伸模組視為預設的延伸模組。|  
  
###  <a name="bkmk_rendering"></a> 轉譯延伸模組一般組態  
 指定用於報表呈現的預設 (而且可能是自訂的) 轉譯延伸模組。  
  
 除非您要部署自訂轉譯延伸模組，否則請勿修改此區段。 如需詳細資訊，請參閱＜ [Implementing a Rendering Extension](../../reporting-services/extensions/rendering-extension/implementing-a-rendering-extension.md)＞。  
  
 預設轉譯延伸模組包含以下內容：  
  
-   XML  
  
-   Null  
  
-   CSV  
  
-   PDF  
  
-   RGDI  
  
-   HTML4.0  
  
-   MHTML  
  
-   EXCEL  
  
-   RPL  
  
-   IMAGE  
  
 從 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 版開始，MHTML 和 HTML 4.0 轉譯程式預設包含下列裝置資訊設定，以控制調整資料視覺效果大小的行為。  
  
```  
<DeviceInfo><DataVisualizationFitSizing>Approximate</DataVisualizationFitSizing></DeviceInfo>  
```  
  
 如需有關 DeviceInfo 設定的詳細資訊，請參閱：  
  
-   [MHTML 裝置資訊設定](../../reporting-services/mhtml-device-information-settings.md)  
  
-   [HTML 裝置資訊設定](../../reporting-services/html-device-information-settings.md)  
  
-   [轉譯延伸模組的裝置資訊設定 &#40;Reporting Services&#41;](../../reporting-services/device-information-settings-for-rendering-extensions-reporting-services.md)  
  
 如需 **\<Render>** 底下子 **\<Extension>** 元素屬性的資訊，請參閱下列文章：  
  
-   [在 RSReportServer.Config 中自訂轉譯延伸模組參數](../../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)  
  
-   [部署轉譯延伸模組](../../reporting-services/extensions/rendering-extension/deploying-a-rendering-extension.md)  
  
 除非您要部署自訂轉譯延伸模組，否則請勿修改此區段。 如需詳細資訊，請參閱＜ [Implementing a Rendering Extension](../../reporting-services/extensions/rendering-extension/implementing-a-rendering-extension.md)＞。  
  
###  <a name="bkmk_data"></a> 資料延伸模組一般組態  
 指定用於處理查詢的預設 (而且可能是自訂的) 資料處理延伸模組。 預設資料處理延伸模組包含以下內容：  
  
-   SQL  
  
-   SQLAZURE  
  
-   SQLPDW  
  
-   OLEDB  
  
-   OLEDB-MD  
  
-   ORACLE  
  
-   ODBC  
  
-   XML  
  
-   SHAREPOINTLIST  
  
-   SAPBW  
  
-   ESSBASE  
  
-   TERADATA  
  
 除非您要加入自訂資料處理延伸模組，否則請勿修改此區段。 如需詳細資訊，請參閱＜ [Implementing a Data Processing Extension](../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)＞。  
  
###  <a name="bkmk_semantic"></a> 語意查詢延伸模組一般組態  
 指定用於處理報表模型的語意查詢處理延伸模組。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 隨附的語意查詢處理延伸模組會提供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 關聯式資料、Oracle 和 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 多維度資料的支援。 請勿修改此區段。 查詢處理不可延伸。  
  
###  <a name="bkmk_model"></a> 模型產生組態  
 指定模型產生延伸模組，它是用於根據已經在報表伺服器上發行的共用資料來源建立報表模型。 您可以針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 關聯式資料、Oracle 和 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 多維度資料來源產生模型。 請勿修改此區段。 模型產生是無法延伸的。  
  
###  <a name="bkmk_security"></a> 安全性延伸模組組態  
 指定 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]所使用的授權元件。 這個元件是由 RSReportServer.config 檔之 **Authentication** 項目中註冊的驗證延伸模組所使用。 除非您要實作自訂驗證延伸模組，否則請勿修改此區段。 如需有關加入自訂安全性功能的詳細資訊，請參閱＜ [Implementing a Security Extension](../../reporting-services/extensions/security-extension/implementing-a-security-extension.md)＞。 如需有關授權的詳細資訊，請參閱＜ [Authorization in Reporting Services](../../reporting-services/extensions/security-extension/authorization-in-reporting-services.md)＞。  
  
###  <a name="bkmk_authentication"></a> 驗證延伸模組組態  
 指定報表伺服器所使用的預設和自訂驗證延伸模組。 預設的延伸模組是以 Windows 驗證為基礎。 除非您要實作自訂驗證延伸模組，否則請勿修改此區段。 如需 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]中驗證的詳細資訊，請參閱 [Reporting Services 中的驗證](../../reporting-services/extensions/security-extension/authentication-in-reporting-services.md) 和 [使用報表伺服器驗證](../../reporting-services/security/authentication-with-the-report-server.md)。 如需有關加入自訂安全性功能的詳細資訊，請參閱＜ [Implementing a Security Extension](../../reporting-services/extensions/security-extension/implementing-a-security-extension.md)＞。  
  
###  <a name="bkmk_eventprocessing"></a> 事件處理  
 指定預設事件處理常式。 請勿修改此區段。 這個區段無法延伸。  
  
###  <a name="bkmk_reportdefinition"></a> Report Definition Customization  
 指定可修改報表定義之自訂延伸模組的名稱和類型。  
  
###  <a name="bkmk_rdlsandboxing"></a> RDLSandboxing  
 指定報表定義語言 (RDL) 模式，可在多個租用戶共用報表伺服器的單一 Web 伺服陣列的案例中，協助您偵測及限制個別租用戶所使用的特定報表資源類型。 如需詳細資訊，請參閱 [啟用與停用 RDL 沙箱](../../reporting-services/report-server-sharepoint/enable-and-disable-rdl-sandboxing.md)。  
  
##  <a name="bkmk_MapTileServer"></a> MapTileServerConfiguration (RSReportServer.config 檔案)  
 **MapTileServerConfiguration** 會定義 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Bing Maps Web 服務的組態設定，以便針對在報表伺服器上發行之報表中的地圖報表項目提供影像分割背景。 所有子元素都是必要的。  
  
|設定|Description|  
|-------------|-----------------|  
|**MaxConnections**|指定 Bing Maps Web 服務的連接數目上限。|  
|**逾時**|指定等候 Bing Maps Web 服務回應的逾時 (以秒為單位)。|  
|**AppID**|指定要用於 Bing Maps Web 服務的應用程式識別碼 (AppID)。 **(預設值)** 會指定 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 預設 AppID。<br /><br /> 如需有關在報表中使用 Bing 地圖底圖的詳細資訊，請參閱 [其他使用規定](https://go.microsoft.com/fwlink/?LinkId=151371)。<br /><br /> 除非您必須針對自己的 Bing Maps 授權合約指定自訂 AppID，否則請勿變更此值。 變更 AppID 時，您不需要重新啟動 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ，即可讓變更生效。|  
|**CacheLevel**|根據 System.Net.Cache 的 HttpRequestCacheLevel 列舉型別指定值。 預設值為 **Default**。 如需詳細資訊，請參閱 [HttpRequestCacheLevel 列舉型別](https://go.microsoft.com/fwlink/?LinkId=153353)。|  
  
##  <a name="bkmk_nativedefaultfile"></a> 原生模式報表伺服器的預設組態檔  
 預設情況下，rsreportserver.config 檔案會安裝到以下位置：  
  
 **C:\Program Files\Microsoft SQL Server\MSRS13.MSSQLSERVER\Reporting Services\ReportServer**  
  
```  
<Configuration>
    <Dsn>AQAAANCMnd8BFdERjHoAwE/Cl+sBAAAAR58DMGebHUeMvyR6HR04kQQAAAAiAAAAUgBlAHAAbwBy
AHQAaQBuAGcAIABTAGUAcgB2AGUAcgAAAANmAADAAAAAEAAAADczfLRgZ4GF44iBHkLrKY4AAAAA
BIAAAKAAAAAQAAAAJ9wQOmDNauH+LS30rboJ2OAAAAAp0kiFFBrc3r3ypKaldZJtjCORX9LTZRzt
0/JCSVIZc4GXx0peGKqd+f85UyrY/KOyUSHogOC/XoBp9Ppxv6ITbdunsS/LXEcMUBVqEdQD4ylh
x6K1NTC/u8hl9v0MgK+xMQKaiV7BuNYbgGgkaViABcNH0xVzcc5rMTHUkrABbGDFGKyAFniGQ1qu
/rqHibNNyvYbP/2uiqvgC0tQl6u8VkVbXpWrkvO+bFCqxlaJlCoDc2f3rIO321SZEvoFbsYNgPLd
+mIAkSCnH3Z3gm/bI8bqVkFaHblKyQuSfFsi6RQAAACb87b26dV0GjHmMJnE0Tk8CzNmhg==</Dsn>
    <ConnectionType>Default</ConnectionType>
    <LogonUser></LogonUser>
    <LogonDomain></LogonDomain>
    <LogonCred></LogonCred>
    <InstanceId>MSRS13.MSSQLSERVER</InstanceId>
    <InstallationID>{cd920604-a5c7-4554-b2a0-aadc04312fe5}</InstallationID>
    <Add Key="SecureConnectionLevel" Value="0"/>
    <Add Key="DisableSecureFormsAuthenticationCookie" Value="false"/>
    <Add Key="CleanupCycleMinutes" Value="10"/>
    <Add Key="MaxActiveReqForOneUser" Value="20"/>
    <Add Key="DatabaseQueryTimeout" Value="120"/>
    <Add Key="RunningRequestsScavengerCycle" Value="60"/>
    <Add Key="RunningRequestsDbCycle" Value="60"/>
    <Add Key="RunningRequestsAge" Value="30"/>
    <Add Key="MaxScheduleWait" Value="5"/>
    <Add Key="DisplayErrorLink" Value="true"/>
    <Add Key="WebServiceUseFileShareStorage" Value="false"/>
    <!--  <Add Key="ProcessTimeout" Value="150" /> -->
    <!--  <Add Key="ProcessTimeoutGcExtension" Value="30" /> -->
    <!--  <Add Key="WatsonFlags" Value="0x0430" /> full dump-->
    <!--  <Add Key="WatsonFlags" Value="0x0428" /> minidump -->
    <!--  <Add Key="WatsonFlags" Value="0x0002" /> no dump-->
    <Add Key="WatsonFlags" Value="0x0428"/>
    <Add Key="WatsonDumpOnExceptions" Value="Microsoft.ReportingServices.Diagnostics.Utilities.InternalCatalogException,Microsoft.ReportingServices.Modeling.InternalModelingException,Microsoft.ReportingServices.ReportProcessing.UnhandledReportRenderingException"/>
    <Add Key="WatsonDumpExcludeIfContainsExceptions" Value="System.Threading.ThreadAbortException,System.Web.UI.ViewStateException,System.OutOfMemoryException,System.Web.HttpException,System.IO.IOException,System.IO.FileLoadException,Microsoft.SharePoint.SPException,Microsoft.ReportingServices.WmiProvider.WMIProviderException,System.AppDomainUnloadedException"/>
    <URLReservations>
        <Application>
            <Name>ReportServerWebService</Name>
            <VirtualDirectory>ReportServer</VirtualDirectory>
            <URLs>
                <URL>
                    <UrlString>http://+:80</UrlString>
                    <AccountSid>S-1-5-80-2885764129-887777008-271615777-1616004480-2722851051</AccountSid>
                    <AccountName>NT SERVICE\ReportServer</AccountName>
                </URL>
            </URLs>
        </Application>
        <Application>
            <Name>ReportServerWebApp</Name>
            <VirtualDirectory>Reports</VirtualDirectory>
            <URLs>
                <URL>
                    <UrlString>http://+:80</UrlString>
                    <AccountSid>S-1-5-80-2885764129-887777008-271615777-1616004480-2722851051</AccountSid>
                    <AccountName>NT SERVICE\ReportServer</AccountName>
                </URL>
            </URLs>
        </Application>
    </URLReservations>
    <Authentication>
        <AuthenticationTypes>
            <RSWindowsNTLM/>
        </AuthenticationTypes>
        <RSWindowsExtendedProtectionLevel>Off</RSWindowsExtendedProtectionLevel>
        <RSWindowsExtendedProtectionScenario>Proxy</RSWindowsExtendedProtectionScenario>
        <EnableAuthPersistence>true</EnableAuthPersistence>
    </Authentication>
    <Service>
        <IsSchedulingService>True</IsSchedulingService>
        <IsNotificationService>True</IsNotificationService>
        <IsEventService>True</IsEventService>
        <PollingInterval>10</PollingInterval>
        <WindowsServiceUseFileShareStorage>False</WindowsServiceUseFileShareStorage>
        <MemorySafetyMargin>80</MemorySafetyMargin>
        <MemoryThreshold>90</MemoryThreshold>
        <RecycleTime>720</RecycleTime>
        <MaxAppDomainUnloadTime>30</MaxAppDomainUnloadTime>
        <MaxQueueThreads>0</MaxQueueThreads>
        <UrlRoot>
        </UrlRoot>
        <UnattendedExecutionAccount>
            <UserName></UserName>
            <Password></Password>
            <Domain></Domain>
        </UnattendedExecutionAccount>
        <PolicyLevel>rssrvpolicy.config</PolicyLevel>
        <IsWebServiceEnabled>True</IsWebServiceEnabled>
        <IsReportManagerEnabled>True</IsReportManagerEnabled>
        <FileShareStorageLocation>
            <Path>
            </Path>
        </FileShareStorageLocation>
        <DefaultFileShareAccount>
            <Domain></Domain>
            <UserName></UserName>
            <Password></Password>
        </DefaultFileShareAccount>
    </Service>
    <UI>
        <ReportServerUrl>
        </ReportServerUrl>
        <PageCountMode>Estimate</PageCountMode>
    </UI>
    <Extensions>
        <Delivery>
            <Extension Name="Report Server FileShare" Type="Microsoft.ReportingServices.FileShareDeliveryProvider.FileShareProvider,ReportingServicesFileShareDeliveryProvider">
                <MaxRetries>3</MaxRetries>
                <SecondsBeforeRetry>900</SecondsBeforeRetry>
                <Configuration>
                    <FileShareConfiguration>
                        <ExcludedRenderFormats>
                            <RenderingExtension>HTMLOWC</RenderingExtension>
                            <RenderingExtension>NULL</RenderingExtension>
                            <RenderingExtension>RGDI</RenderingExtension>
                        </ExcludedRenderFormats>
                    </FileShareConfiguration>
                </Configuration>
            </Extension>
            <Extension Name="Report Server Email" Type="Microsoft.ReportingServices.EmailDeliveryProvider.EmailProvider,ReportingServicesEmailDeliveryProvider">
                <MaxRetries>3</MaxRetries>
                <SecondsBeforeRetry>900</SecondsBeforeRetry>
                <Configuration>
                    <RSEmailDPConfiguration>
                        <SMTPServer></SMTPServer>
                        <SMTPServerPort>
                        </SMTPServerPort>
                        <SMTPAccountName>
                        </SMTPAccountName>
                        <SMTPConnectionTimeout>
                        </SMTPConnectionTimeout>
                        <SMTPServerPickupDirectory>
                        </SMTPServerPickupDirectory>
                        <SMTPUseSSL>False</SMTPUseSSL>
                        <SendUsing>2</SendUsing>
                        <SMTPAuthenticate>0</SMTPAuthenticate>
                        <SendUserName></SendUserName>
                        <SendPassword></SendPassword>
                        <From></From>
                        <EmbeddedRenderFormats>
                            <RenderingExtension>MHTML</RenderingExtension>
                        </EmbeddedRenderFormats>
                        <PrivilegedUserRenderFormats>
                        </PrivilegedUserRenderFormats>
                        <ExcludedRenderFormats>
                            <RenderingExtension>HTMLOWC</RenderingExtension>
                            <RenderingExtension>NULL</RenderingExtension>
                            <RenderingExtension>RGDI</RenderingExtension>
                        </ExcludedRenderFormats>
                        <SendEmailToUserAlias>True</SendEmailToUserAlias>
                        <DefaultHostName>
                        </DefaultHostName>
                        <PermittedHosts>
                        </PermittedHosts>
                    </RSEmailDPConfiguration>
                </Configuration>
            </Extension>
            <Extension Name="Report Server DocumentLibrary" Type="Microsoft.ReportingServices.SharePoint.SharePointDeliveryExtension.DocumentLibraryProvider,ReportingServicesSharePointDeliveryExtension">
                <MaxRetries>3</MaxRetries>
                <SecondsBeforeRetry>900</SecondsBeforeRetry>
                <Configuration>
                    <DocumentLibraryConfiguration>
                        <ExcludedRenderFormats>
                            <RenderingExtension>HTMLOWC</RenderingExtension>
                            <RenderingExtension>NULL</RenderingExtension>
                            <RenderingExtension>RGDI</RenderingExtension>
                        </ExcludedRenderFormats>
                    </DocumentLibraryConfiguration>
                </Configuration>
            </Extension>
            <Extension Name="NULL" Type="Microsoft.ReportingServices.NullDeliveryProvider.NullProvider,ReportingServicesNullDeliveryProvider"/>
            <Extension Name="Report Server PowerBI" Type="Microsoft.ReportingServices.PowerBIDeliveryProvider.PowerBIDeliveryProvider,ReportingServicesPowerBIDeliveryProvider">
                <MaxRetries>3</MaxRetries>
                <SecondsBeforeRetry>900</SecondsBeforeRetry>
                <Configuration>
                    <PowerBIDeliveryConfiguration>
                    </PowerBIDeliveryConfiguration>
                </Configuration>
            </Extension>
        </Delivery>
        <DeliveryUI>
            <Extension Name="Report Server Email" Type="Microsoft.ReportingServices.EmailDeliveryProvider.EmailDeliveryProviderControl,ReportingServicesEmailDeliveryProvider">
                <DefaultDeliveryExtension>True</DefaultDeliveryExtension>
                <Configuration>
                    <RSEmailDPConfiguration>
                        <DefaultRenderingExtension>MHTML</DefaultRenderingExtension>
                    </RSEmailDPConfiguration>
                </Configuration>
            </Extension>
            <Extension Name="Report Server FileShare" Type="Microsoft.ReportingServices.FileShareDeliveryProvider.FileShareUIControl,ReportingServicesFileShareDeliveryProvider"/>
            <Extension Name="Report Server PowerBI" Type="Microsoft.ReportingServices.PowerBIDeliveryProvider.PowerBIDeliveryUIControl,ReportingServicesPowerBIDeliveryProvider"/>
        </DeliveryUI>
        <Render>
            <Extension Name="WORDOPENXML" Type="Microsoft.ReportingServices.Rendering.WordRenderer.WordOpenXmlRenderer.WordOpenXmlDocumentRenderer,Microsoft.ReportingServices.WordRendering"/>
            <Extension Name="WORD" Type="Microsoft.ReportingServices.Rendering.WordRenderer.WordDocumentRenderer,Microsoft.ReportingServices.WordRendering" Visible="false"/>
            <Extension Name="EXCELOPENXML" Type="Microsoft.ReportingServices.Rendering.ExcelOpenXmlRenderer.ExcelOpenXmlRenderer,Microsoft.ReportingServices.ExcelRendering"/>
            <Extension Name="EXCEL" Type="Microsoft.ReportingServices.Rendering.ExcelRenderer.ExcelRenderer,Microsoft.ReportingServices.ExcelRendering" Visible="false"/>
            <Extension Name="PPTX" Type="Microsoft.ReportingServices.Rendering.PowerPointRendering.PptxRenderingExtension,Microsoft.ReportingServices.PowerPointRendering"/>
            <Extension Name="PDF" Type="Microsoft.ReportingServices.Rendering.ImageRenderer.PDFRenderer,Microsoft.ReportingServices.ImageRendering"/>
            <Extension Name="IMAGE" Type="Microsoft.ReportingServices.Rendering.ImageRenderer.ImageRenderer,Microsoft.ReportingServices.ImageRendering"/>
            <Extension Name="MHTML" Type="Microsoft.ReportingServices.Rendering.HtmlRenderer.MHtmlRenderingExtension,Microsoft.ReportingServices.HtmlRendering">
                <Configuration>
                    <DeviceInfo>
                        <DataVisualizationFitSizing>Approximate</DataVisualizationFitSizing>
                    </DeviceInfo>
                </Configuration>
            </Extension>
            <Extension Name="CSV" Type="Microsoft.ReportingServices.Rendering.DataRenderer.CsvReport,Microsoft.ReportingServices.DataRendering"/>
            <Extension Name="XML" Type="Microsoft.ReportingServices.Rendering.DataRenderer.XmlDataReport,Microsoft.ReportingServices.DataRendering"/>
            <Extension Name="ATOM" Type="Microsoft.ReportingServices.Rendering.DataRenderer.AtomDataReport,Microsoft.ReportingServices.DataRendering"/>
            <Extension Name="NULL" Type="Microsoft.ReportingServices.Rendering.NullRenderer.NullReport,Microsoft.ReportingServices.NullRendering" Visible="false"/>
            <Extension Name="RGDI" Type="Microsoft.ReportingServices.Rendering.ImageRenderer.RGDIRenderer,Microsoft.ReportingServices.ImageRendering" Visible="false"/>
            <Extension Name="HTML4.0" Type="Microsoft.ReportingServices.Rendering.HtmlRenderer.Html40RenderingExtension,Microsoft.ReportingServices.HtmlRendering" Visible="false">
                <Configuration>
                    <DeviceInfo>
                        <DataVisualizationFitSizing>Approximate</DataVisualizationFitSizing>
                    </DeviceInfo>
                </Configuration>
            </Extension>
            <Extension Name="HTML5" Type="Microsoft.ReportingServices.Rendering.HtmlRenderer.Html5RenderingExtension,Microsoft.ReportingServices.HtmlRendering" Visible="false">
                <Configuration>
                    <DeviceInfo>
                        <DataVisualizationFitSizing>Approximate</DataVisualizationFitSizing>
                    </DeviceInfo>
                </Configuration>
            </Extension>
            <Extension Name="RPL" Type="Microsoft.ReportingServices.Rendering.RPLRendering.RPLRenderer,Microsoft.ReportingServices.RPLRendering" Visible="false" LogAllExecutionRequests="false"/>
        </Render>
        <!--
        For the SQLPDW extension to work, install the SQL Server PDW Client Tools on the report server.
        NOTE: The SQLPDW extension is deprecated. It supports old versions of SQL Server Parallel Data Warehouse (PDW).        
        To connect to Analytics Platform System, use the SQL (SQL Server) extension.        
        For the ORACLE extension to work, install the Oracle Data Provider for NET (ODP.NET) on the report server.
        For TERADATA extension to work, install the .NET Provider for Teradata on the report server.
      -->
        <Data>
            <Extension Name="SQL" Type="Microsoft.ReportingServices.DataExtensions.SqlConnectionWrapper,Microsoft.ReportingServices.DataExtensions"/>
            <Extension Name="SQLAZURE" Type="Microsoft.ReportingServices.DataExtensions.SqlAzureConnectionWrapper,Microsoft.ReportingServices.DataExtensions"/>
            <Extension Name="SQLPDW" Type="Microsoft.ReportingServices.DataExtensions.SqlDwConnectionWrapper,Microsoft.ReportingServices.DataExtensions"/>
            <Extension Name="OLEDB-MD" Type="Microsoft.ReportingServices.DataExtensions.AdoMdConnection,Microsoft.ReportingServices.DataExtensions"/>
            <Extension Name="SHAREPOINTLIST" Type="Microsoft.ReportingServices.DataExtensions.SharePointList.SPListConnection,Microsoft.ReportingServices.DataExtensions"/>
            <Extension Name="ORACLE" Type="Microsoft.ReportingServices.DataExtensions.OracleClientConnectionWrapper,Microsoft.ReportingServices.DataExtensions"/>
            <Extension Name="ESSBASE" Type="Microsoft.ReportingServices.DataExtensions.Essbase.EssbaseConnection,Microsoft.ReportingServices.DataExtensions.Essbase"/>
            <Extension Name="SAPBW" Type="Microsoft.ReportingServices.DataExtensions.SapBw.SapBwConnection,Microsoft.ReportingServices.DataExtensions.SapBw"/>
            <Extension Name="TERADATA" Type="Microsoft.ReportingServices.DataExtensions.TeradataConnectionWrapper,Microsoft.ReportingServices.DataExtensions"/>
            <Extension Name="OLEDB" Type="Microsoft.ReportingServices.DataExtensions.OleDbConnectionWrapper,Microsoft.ReportingServices.DataExtensions"/>
            <Extension Name="ODBC" Type="Microsoft.ReportingServices.DataExtensions.OdbcConnectionWrapper,Microsoft.ReportingServices.DataExtensions"/>
            <Extension Name="XML" Type="Microsoft.ReportingServices.DataExtensions.XmlDPConnection,Microsoft.ReportingServices.DataExtensions"/>
        </Data>
        <SemanticQuery>
            <Extension Name="SQL" Type="Microsoft.ReportingServices.SemanticQueryEngine.Sql.MSSQL.MSSqlSQCommand,Microsoft.ReportingServices.SemanticQueryEngine">
                <Configuration>
                    <EnableMathOpCasting>False</EnableMathOpCasting>
                </Configuration>
            </Extension>
            <Extension Name="SQLAZURE" Type="Microsoft.ReportingServices.SemanticQueryEngine.Sql.MSSQL.MSSqlSQCommand,Microsoft.ReportingServices.SemanticQueryEngine">
                <Configuration>
                    <EnableMathOpCasting>False</EnableMathOpCasting>
                </Configuration>
            </Extension>
            <Extension Name="SQLPDW" Type="Microsoft.ReportingServices.SemanticQueryEngine.Sql.MSSQLADW.MSSqlAdwSQCommand,Microsoft.ReportingServices.SemanticQueryEngine">
                <Configuration>
                    <EnableMathOpCasting>False</EnableMathOpCasting>
                </Configuration>
            </Extension>
            <Extension Name="ORACLE" Type="Microsoft.ReportingServices.SemanticQueryEngine.Sql.Oracle.OraSqlSQCommand,Microsoft.ReportingServices.SemanticQueryEngine">
                <Configuration>
                    <EnableMathOpCasting>True</EnableMathOpCasting>
                    <DisableNO_MERGEInLeftOuters>False</DisableNO_MERGEInLeftOuters>
                    <EnableUnistr>False</EnableUnistr>
                    <DisableTSTruncation>False</DisableTSTruncation>
                </Configuration>
            </Extension>
            <Extension Name="TERADATA" Type="Microsoft.ReportingServices.SemanticQueryEngine.Sql.Teradata.TdSqlSQCommand,Microsoft.ReportingServices.SemanticQueryEngine">
                <Configuration>
                    <EnableMathOpCasting>True</EnableMathOpCasting>
                    <ReplaceFunctionName>oREPLACE</ReplaceFunctionName>
                </Configuration>
            </Extension>
            <Extension Name="OLEDB-MD" Type="Microsoft.AnalysisServices.Modeling.QueryExecution.ASSemanticQueryCommand,Microsoft.AnalysisServices.Modeling"/>
        </SemanticQuery>
        <ModelGeneration>
            <Extension Name="SQL" Type="Microsoft.ReportingServices.SemanticQueryEngine.Sql.MSSQL.MsSqlModelGenerator,Microsoft.ReportingServices.SemanticQueryEngine"/>
            <Extension Name="SQLAZURE" Type="Microsoft.ReportingServices.SemanticQueryEngine.Sql.MSSQL.MsSqlModelGenerator,Microsoft.ReportingServices.SemanticQueryEngine"/>
            <Extension Name="ORACLE" Type="Microsoft.ReportingServices.SemanticQueryEngine.Sql.Oracle.OraSqlModelGenerator,Microsoft.ReportingServices.SemanticQueryEngine"/>
            <Extension Name="TERADATA" Type="Microsoft.ReportingServices.SemanticQueryEngine.Sql.Teradata.TdSqlModelGenerator,Microsoft.ReportingServices.SemanticQueryEngine"/>
            <Extension Name="OLEDB-MD" Type="Microsoft.AnalysisServices.Modeling.Generation.ModelGeneratorExtention,Microsoft.AnalysisServices.Modeling"/>
        </ModelGeneration>
        <Security>
            <Extension Name="Windows" Type="Microsoft.ReportingServices.Authorization.WindowsAuthorization, Microsoft.ReportingServices.Authorization"/>
        </Security>
        <Authentication>
            <Extension Name="Windows" Type="Microsoft.ReportingServices.Authentication.WindowsAuthentication, Microsoft.ReportingServices.Authorization"/>
        </Authentication>
        <EventProcessing>
            <Extension Name="SnapShot Extension" Type="Microsoft.ReportingServices.Library.HistorySnapShotCreatedHandler,ReportingServicesLibrary">
                <Event>
                    <Type>ReportHistorySnapshotCreated</Type>
                </Event>
            </Extension>
            <Extension Name="Timed Subscription Extension" Type="Microsoft.ReportingServices.Library.TimedSubscriptionHandler,ReportingServicesLibrary">
                <Event>
                    <Type>TimedSubscription</Type>
                </Event>
            </Extension>
            <Extension Name="Cache Refresh Plan Extension" Type="Microsoft.ReportingServices.Library.CacheRefreshPlanHandler,ReportingServicesLibrary">
                <Event>
                    <Type>RefreshCache</Type>
                </Event>
            </Extension>
            <Extension Name="Shared Dataset Cache Update Extension" Type="Microsoft.ReportingServices.Library.SharedDatasetCacheUpdatePlanHandler,ReportingServicesLibrary">
                <Event>
                    <Type>SharedDatasetCacheUpdate</Type>
                </Event>
            </Extension>
            <Extension Name="Cache Update Extension" Type="Microsoft.ReportingServices.Library.ReportExecutionSnapshotUpdateEventHandler,ReportingServicesLibrary">
                <Event>
                    <Type>SnapshotUpdated</Type>
                </Event>
            </Extension>
        </EventProcessing>
    </Extensions>
    <MapTileServerConfiguration>
        <MaxConnections>2</MaxConnections>
        <Timeout>10</Timeout>
        <AppID>(Default)</AppID>
        <CacheLevel>Default</CacheLevel>
    </MapTileServerConfiguration>
</Configuration> 
```  
  
##  <a name="bkmk_sharepointdefaultfile"></a> SharePoint 模式報表伺服器的預設組態檔  
 預設情況下，rsreportserver.config 檔案會安裝到以下位置：  
  
 **C:\Program Files\Common Files\Microsoft Shared\Web Server Extensions\15\WebServices\Reporting**  
  
```  
<Configuration>  
  <Dsn />  
  <ConnectionType>Default</ConnectionType>  
  <LogonUser>  
  </LogonUser>  
  <LogonDomain>  
  </LogonDomain>  
  <LogonCred>  
  </LogonCred>  
  <InstanceId>MSRS12.@Sharepoint</InstanceId>  
  <Add Key="SecureConnectionLevel" Value="0" />  
  <Add Key="CleanupCycleMinutes" Value="10" />  
  <Add Key="MaxActiveReqForOneUser" Value="20" />  
  <Add Key="AlertingCleanupCycleMinutes" Value="20" />  
  <Add Key="AlertingDataCleanupMinutes" Value="360" />  
  <Add Key="AlertingExecutionLogCleanupMinutes" Value="10080" />  
  <Add Key="AlertingMaxDataRetentionDays" Value="180" />  
  <Add Key="RunningRequestsScavengerCycle" Value="60" />  
  <Add Key="RunningRequestsDbCycle" Value="60" />  
  <Add Key="RunningRequestsAge" Value="30" />  
  <Add Key="MaxScheduleWait" Value="5" />  
  <Add Key="DisplayErrorLink" Value="true" />  
  <Add Key="WebServiceUseFileShareStorage" Value="false" />  
  <!--  <Add Key="ProcessTimeout" Value="150" /> -->  
  <!--  <Add Key="ProcessTimeoutGcExtension" Value="30" /> -->  
  <!--  <Add Key="WatsonFlags" Value="0x0430" /> full dump-->  
  <!--  <Add Key="WatsonFlags" Value="0x0428" /> minidump -->  
  <!--  <Add Key="WatsonFlags" Value="0x0002" /> no dump-->  
  <Add Key="WatsonFlags" Value="0x0428" />  
  <Add Key="WatsonDumpOnExceptions" Value="Microsoft.ReportingServices.Diagnostics.Utilities.InternalCatalogException,Microsoft.ReportingServices.Modeling.InternalModelingException,Microsoft.ReportingServices.ReportProcessing.UnhandledReportRenderingException" />  
  <Add Key="WatsonDumpExcludeIfContainsExceptions" Value="System.Threading.ThreadAbortException,System.Web.UI.ViewStateException,System.OutOfMemoryException,System.Web.HttpException,System.IO.IOException,System.IO.FileLoadException,Microsoft.SharePoint.SPException,Microsoft.ReportingServices.WmiProvider.WMIProviderException" />  
  <RStrace>  
    <add name="FileName" value="ReportServerService" />  
    <add name="FileSizeLimitMb" value="32" />  
    <add name="KeepFilesForDays" value="14" />  
    <add name="Prefix" value="tid, time" />  
    <add name="TraceListeners" value="file" />  
    <add name="TraceFileMode" value="unique" />  
    <add name="Components" value="all:3" />  
  </RStrace>  
  <URLReservations>  
    <Application>  
      <Name>ReportServerWebService</Name>  
      <VirtualDirectory>ReportServer</VirtualDirectory>  
      <URLs>  
        <URL>  
          <UrlString>http://+:80</UrlString>  
          <AccountSid>  
          </AccountSid>  
          <AccountName>  
          </AccountName>  
        </URL>  
      </URLs>  
    </Application>  
    <Application>  
      <Name>ReportManager</Name>  
      <VirtualDirectory>Reports</VirtualDirectory>  
      <URLs>  
        <URL>  
          <UrlString>http://+:80</UrlString>  
          <AccountSid>  
          </AccountSid>  
          <AccountName>  
          </AccountName>  
        </URL>  
      </URLs>  
    </Application>  
  </URLReservations>  
  <Authentication>  
    <AuthenticationTypes>  
      <RSWindowsNTLM />  
    </AuthenticationTypes>  
    <EnableAuthPersistence>true</EnableAuthPersistence>  
  </Authentication>  
  <Service>  
    <IsSchedulingService>True</IsSchedulingService>  
    <IsNotificationService>True</IsNotificationService>  
    <IsEventService>True</IsEventService>  
    <IsAlertingService>True</IsAlertingService>  
    <PollingInterval>10</PollingInterval>  
    <WindowsServiceUseFileShareStorage>False</WindowsServiceUseFileShareStorage>  
    <MemorySafetyMargin>80</MemorySafetyMargin>  
    <MemoryThreshold>90</MemoryThreshold>  
    <RecycleTime>720</RecycleTime>  
    <MaxAppDomainUnloadTime>30</MaxAppDomainUnloadTime>  
    <MaxQueueThreads>0</MaxQueueThreads>  
    <UrlRoot>  
    </UrlRoot>  
    <PolicyLevel>rssrvpolicy.config</PolicyLevel>  
    <IsWebServiceEnabled>True</IsWebServiceEnabled>    
    <FileShareStorageLocation>  
      <Path>  
      </Path>  
    </FileShareStorageLocation>  
  </Service>  
  <UI>  
    <ReportServerUrl>  
    </ReportServerUrl>  
    <PageCountMode>Estimate</PageCountMode>  
  </UI>  
  <MapTileServerConfiguration>  
    <MaxConnections>2</MaxConnections>  
    <Timeout>10</Timeout>  
    <AppID>(Default)</AppID>  
    <CacheLevel>Default</CacheLevel>  
  </MapTileServerConfiguration>  
</Configuration>  
```  
  
## <a name="see-also"></a>另請參閱  
 [修改 Reporting Services 組態檔 &#40;RSreportserver.config&#41;](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)   
 [設定報表伺服器應用程式的可用記憶體](../../reporting-services/report-server/configure-available-memory-for-report-server-applications.md)   
 [Reporting Services 組態檔](../../reporting-services/report-server/reporting-services-configuration-files.md)   
 [將報表伺服器初始化 &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md)   
 [儲存加密的報表伺服器資料 &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)   
 [Reporting Services 組態管理員 &#40;原生模式&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)  
 更多問題嗎？ [試試 Reporting Services 論壇](https://go.microsoft.com/fwlink/?LinkId=620231)
  
  
