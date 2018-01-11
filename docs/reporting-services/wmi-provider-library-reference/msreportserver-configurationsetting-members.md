---
title: "MSReportServer_ConfigurationSetting 成員 | Microsoft Docs"
ms.custom: 
ms.date: 03/20/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: wmi-provider-library-reference
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
apiname: MSReportServer_ConfigurationSetting Members
apilocation: reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- WMI provider [Reporting Services], MSReportServer_ConfigurationSetting class
- MSReportServer_ConfigurationSetting class
ms.assetid: 5e21a53a-a2f8-4b35-a8d9-5483519e3857
caps.latest.revision: "46"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 8c3ea3dfb366325d64469b1cda9f6b25b6460b5d
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/09/2018
---
# <a name="msreportserverconfigurationsetting-members"></a>MSReportServer_ConfigurationSetting 成員
  MSReportServer_ConfigurationSetting 類別包含下列屬性和方法。  
  
## <a name="public-properties"></a>公用屬性  
  
|||  
|-|-|  
|[ConnectionPoolSize](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-connectionpoolsize.md)|傳回報表伺服器用來與主控報表伺服器資料庫之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體進行通訊的連接集區大小。 唯讀。|  
|[DatabaseLogonAccount](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databaselogonaccount.md)|指定報表伺服器用來連接至主控報表伺服器資料庫之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體的登入帳戶。 唯讀。|  
|[DatabaseLogonTimeout](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databaselogontimeout.md)|指定嘗試登入報表伺服器資料庫失敗之前等候的秒數。 唯讀。|  
|[DatabaseLogonType](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databaselogontype.md)|指定報表伺服器會使用 Windows 服務帳戶、Windows 使用者帳戶或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入來存取報表伺服器資料庫。 唯讀。|  
|[DatabaseName](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databasename.md)|指定主控報表伺服器資料庫之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的名稱。|  
|[DatabaseQueryTimeout](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databasequerytimeout.md)|指定此命令失敗或逾時之前必須經過的秒數。報表伺服器會針對報表伺服器資料庫 (而非報表的資料來源) 進行處理序計時。|  
|[DatabaseServerName](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databaseservername.md)|指定安裝報表伺服器資料庫之伺服器的名稱。|  
|[InstallationID 屬性](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-installationid.md)|傳回特定報表伺服器執行個體的唯一識別碼。|  
|[InstanceName](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-instancename.md)|指定特定電腦上報表伺服器執行個體的名稱。|  
|[IsInitialized](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-isinitialized.md)|指出報表伺服器執行個體是否已初始化。 唯讀。|  
|[IsSharePointIntegrated](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-issharepointintegrated.md)|指出報表伺服器是否設定為 SharePoint 整合模式。|  
|[IsWebServiceEnabled](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-iswebserviceenabled.md)|指出報表伺服器 Web 服務是否已啟用。 唯讀。|  
|[IsWindowsServiceEnabled](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-iswindowsserviceenabled.md)|指出是否已啟用報表伺服器 Windows 服務。 唯讀。|  
|[MachineAccountIdentity 屬性 &#40;WMI&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-machineaccountidentity.md)|取得安裝報表伺服器的電腦帳戶識別。|  
|[PathName](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-pathname.md)|指定報表伺服器執行個體的安裝路徑。|  
|[SecureConnectionLevel](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-secureconnectionlevel.md)|傳回 RSReportServer.config 檔案中指定的安全連接層級。|  
|[SenderEmailAddress](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-senderemailaddress.md)|取得用以從報表伺服器傳送電子郵件的位址。 唯讀。|  
|[SendUsingSMTPServer](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-sendusingsmtpserver.md)|指定電子郵件組態中的 SendUsing 屬性是否設定為 TRUE。|  
|[SMTPServer](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-smtpserver.md)|從 RSReportServer.config 檔案中取得 SMTP 伺服器屬性。 唯讀。|  
|[UnattendedExecutionAccount](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-unattendedexecutionaccount.md)|指定自動執行報表時報表伺服器所模擬的登入使用者帳戶。 唯讀。|  
|[版本](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-version.md)|傳回報表伺服器的版本。|  
|[VirtualDirectoryReportManager 屬性 &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-virtualdirectoryreportmanager.md)|傳回報表管理員應用程式的虛擬目錄。|  
|[VirtualDirectoryReportServer 屬性 &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-virtualdirectoryreportserver.md)|傳回報表伺服器 Web 服務應用程式的虛擬目錄。|  
|[WindowsServiceIdentityActual](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-windowsserviceidentityactual.md)|傳回實際執行報表伺服器 Windows 服務所使用的識別。 唯讀。|  
|[WindowsServiceIdentityConfigured](../../reporting-services/wmi-provider-library-reference/windowsserviceidentityconfigured-property.md)|傳回上次設定報表伺服器 Windows 服務執行時所使用的識別。 唯讀。|  
  
## <a name="public-methods"></a>公用方法  
  
|||  
|-|-|  
|[BackupEncryptionKey](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-backupencryptionkey.md)|備份執行個體的加密金鑰。 此加密金鑰會以密碼加密的方式儲存。|  
|[CreateSSLCertificateBinding 方法 &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-createsslcertificatebinding.md)|建立 SSL 憑證繫結。|  
|[DeleteEncryptedInformation](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-deleteencryptedinformation.md)|從報表伺服器資料庫中刪除加密的資訊。|  
|[DeleteEncryptionKey](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-deleteencryptionkey.md)|從報表伺服器資料庫中刪除加密金鑰。|  
|[GenerateDatabaseCreationScript](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-generatedatabasecreationscript.md)|產生可用來建立報表伺服器資料庫的 SQL 指令碼。|  
|[GenerateDatabaseRightsScript](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-generatedatabaserightsscript.md)|產生可用來將報表伺服器資料庫之權限授與使用者的 SQL 指令碼。|  
|[GenerateDatabaseUpgradeScript](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-generatedatabaseupgradescript.md)|產生可用來升級報表伺服器資料庫的 SQL 指令碼。|  
|[GetAdminSiteUrl 方法 &#40;WMI&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-getadminsiteurl.md)|取得管理中心網站的絕對 URL。|  
|[GetDatabaseVersionDisplayName](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-getdatabaseversiondisplayname.md)|取得給定報表伺服器資料庫版本字串的顯示名稱。|  
|[InitializeReportServer](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-initializereportserver.md)|初始化指定的報表伺服器執行個體。|  
|[ListInstalledSharePointVersions 方法 &#40;WMI&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-listinstalledsharepointversions.md)|傳回一組 Token，這些 Token 代表與報表伺服器安裝在同一部電腦上的 [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] [!INCLUDE[offSPServ](../../includes/offspserv-md.md)], [!INCLUDE[SPF2010](../../includes/spf2010-md.md)]或 [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] 版本。|  
|[ListIPAddresses 方法 &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-listipaddresses.md)|列出電腦的 IP 位址。|  
|[ListReportServersInDatabase](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-listreportserversindatabase.md)|傳回存在報表伺服器資料庫中之報表伺服器安裝的清單，不論這些安裝是否具有安全資訊的存取權都一樣。|  
|[ListReservedURLs 方法 &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-listreservedurls.md)|列出針對報表伺服器上所有應用程式保留的 URL。|  
|[ListSSLCertificateBindings 方法 &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-listsslcertificatebindings.md)|列出存在 HTTP.SYS 中的 SSL 憑證繫結以及預期來自 rsreportserver.config 的 SSL 憑證繫結。|  
|[ListSSLCertificates 方法 &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-listsslcertificates.md)|列出電腦上的已安裝 SSL 憑證。|  
|[ReencryptSecureInformation](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-reencryptsecureinformation.md)|產生新的加密金鑰，並且使用這個新的金鑰來重新加密報表伺服器資料庫中的所有安全資訊。|  
|[RemoveSSLCertificateBindings 方法 &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-removesslcertificatebinding.md)|移除 SSL 憑證繫結。|  
|[RemoveUnattendedExecutionAccount](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-removeunattendedexecutionaccount.md)|從報表伺服器組態中移除自動執行帳戶項目。|  
|[RemoveURL 方法 &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-removeurl.md)|移除針對報表伺服器所保留的 URL。|  
|[ReserveURL 方法 &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-reserveurl.md)|加入給定應用程式的 URL 保留項目。|  
|[RestoreEncryptionKey](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-restoreencryptionkey.md)|將指定的加密金鑰重新套用至報表伺服器資料庫。|  
|[SetDatabaseConnection](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setdatabaseconnection.md)|設定特定報表伺服器資料庫的報表伺服器資料庫連接。|  
|[SetDatabaseLogonTimeout](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setdatabaselogontimeout.md)|指定報表伺服器資料庫登入嘗試的預設逾時值。|  
|[SetDatabaseQueryTimeout](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setdatabasequerytimeout.md)|指定報表伺服器資料庫連接的預設逾時值。|  
|[SetEmailConfiguration](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setemailconfiguration.md)|設定報表伺服器用來傳送電子郵件的電子郵件傳遞延伸模組。|  
|[SetSecureConnectionLevel](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setsecureconnectionlevel.md)|設定報表伺服器的安全連接層級。|  
|[SetServiceState](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setservicestate.md)|開啟和關閉報表伺服器 Windows 與 Web 服務。|  
|[SetUnattendedExecutionAccount](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setunattendedexecutionaccount.md)|指定用來自動執行報表的帳戶。|  
|[SetVirtualDirectory 方法 &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setvirtualdirectory.md)|設定應用程式的虛擬目錄。|  
|[SetWindowsServiceIdentity](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setwindowsserviceidentity.md)|讓報表伺服器 Windows 服務以指定之 Windows 使用者的身分執行，並且授與此帳戶足夠的檔案系統權限，以便允許報表伺服器運作。|  
  
## <a name="see-also"></a>另請參閱  
 [MSReportServer_ConfigurationSetting Class](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
  
