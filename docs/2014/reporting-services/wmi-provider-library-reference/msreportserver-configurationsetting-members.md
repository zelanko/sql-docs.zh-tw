---
title: MSReportServer_ConfigurationSetting 成員 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
api_name:
- MSReportServer_ConfigurationSetting Members
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- WMI provider [Reporting Services], MSReportServer_ConfigurationSetting class
- MSReportServer_ConfigurationSetting class
ms.assetid: 5e21a53a-a2f8-4b35-a8d9-5483519e3857
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 981db90ba9114b26b0581f9b1e3d62561c8b6939
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48180618"
---
# <a name="msreportserverconfigurationsetting-members"></a>MSReportServer_ConfigurationSetting 成員
  MSReportServer_ConfigurationSetting 類別包含下列屬性和方法。  
  
## <a name="public-properties"></a>公用屬性  
  
|||  
|-|-|  
|[ConnectionPoolSize](configurationsetting-property-connectionpoolsize.md)|傳回報表伺服器用來與主控報表伺服器資料庫之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體進行通訊的連接集區大小。 唯讀。|  
|[DatabaseLogonAccount](configurationsetting-property-databaselogonaccount.md)|指定報表伺服器用來連接至主控報表伺服器資料庫之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體的登入帳戶。 唯讀。|  
|[DatabaseLogonTimeout](configurationsetting-property-databaselogontimeout.md)|指定嘗試登入報表伺服器資料庫失敗之前等候的秒數。 唯讀。|  
|[DatabaseLogonType](configurationsetting-property-databaselogontype.md)|指定報表伺服器會使用 Windows 服務帳戶、Windows 使用者帳戶或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入來存取報表伺服器資料庫。 唯讀。|  
|[DatabaseName](configurationsetting-property-databasename.md)|指定主控報表伺服器資料庫之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的名稱。|  
|[DatabaseQueryTimeout](configurationsetting-property-databasequerytimeout.md)|指定此命令失敗或逾時之前必須經過的秒數。報表伺服器會針對報表伺服器資料庫 (而非報表的資料來源) 進行處理序計時。|  
|[DatabaseServerName](configurationsetting-property-databaseservername.md)|指定安裝報表伺服器資料庫之伺服器的名稱。|  
|[InstallationID 屬性](configurationsetting-property-installationid.md)|傳回特定報表伺服器執行個體的唯一識別碼。|  
|[InstanceName](configurationsetting-property-instancename.md)|指定特定電腦上報表伺服器執行個體的名稱。|  
|[IsInitialized](configurationsetting-property-isinitialized.md)|指出報表伺服器執行個體是否已初始化。 唯讀。|  
|[IsSharePointIntegrated](configurationsetting-property-issharepointintegrated.md)|指出報表伺服器是否設定為 SharePoint 整合模式。|  
|[IsWebServiceEnabled](configurationsetting-property-iswebserviceenabled.md)|指出報表伺服器 Web 服務是否已啟用。 唯讀。|  
|[IsWindowsServiceEnabled](configurationsetting-property-iswindowsserviceenabled.md)|指出是否已啟用報表伺服器 Windows 服務。 唯讀。|  
|[MachineAccountIdentity 屬性&#40;WMI&#41;](configurationsetting-property-machineaccountidentity.md)|取得安裝報表伺服器的電腦帳戶識別。|  
|[PathName](configurationsetting-property-pathname.md)|指定報表伺服器執行個體的安裝路徑。|  
|[SecureConnectionLevel](configurationsetting-property-secureconnectionlevel.md)|傳回 RSReportServer.config 檔案中指定的安全連接層級。|  
|[SenderEmailAddress](configurationsetting-property-senderemailaddress.md)|取得用以從報表伺服器傳送電子郵件的位址。 唯讀。|  
|[SendUsingSMTPServer](configurationsetting-property-sendusingsmtpserver.md)|指定電子郵件組態中的 SendUsing 屬性是否設定為 TRUE。|  
|[SMTPServer](configurationsetting-property-smtpserver.md)|從 RSReportServer.config 檔案中取得 SMTP 伺服器屬性。 唯讀。|  
|[UnattendedExecutionAccount](configurationsetting-property-unattendedexecutionaccount.md)|指定自動執行報表時報表伺服器所模擬的登入使用者帳戶。 唯讀。|  
|[版本](configurationsetting-property-version.md)|傳回報表伺服器的版本。|  
|[VirtualDirectoryReportManager 屬性&#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-property-virtualdirectoryreportmanager.md)|傳回報表管理員應用程式的虛擬目錄。|  
|[VirtualDirectoryReportServer 屬性&#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-property-virtualdirectoryreportserver.md)|傳回報表伺服器 Web 服務應用程式的虛擬目錄。|  
|[WindowsServiceIdentityActual](configurationsetting-property-windowsserviceidentityactual.md)|傳回實際執行報表伺服器 Windows 服務所使用的識別。 唯讀。|  
|[WindowsServiceIdentityConfigured](windowsserviceidentityconfigured-property.md)|傳回上次設定報表伺服器 Windows 服務執行時所使用的識別。 唯讀。|  
  
## <a name="public-methods"></a>公用方法  
  
|||  
|-|-|  
|[BackupEncryptionKey](configurationsetting-method-backupencryptionkey.md)|備份執行個體的加密金鑰。 此加密金鑰會以密碼加密的方式儲存。|  
|[CreateSSLCertificateBinding 方法&#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-method-createsslcertificatebinding.md)|建立 SSL 憑證繫結。|  
|[DeleteEncryptedInformation](configurationsetting-method-deleteencryptedinformation.md)|從報表伺服器資料庫中刪除加密的資訊。|  
|[DeleteEncryptionKey](configurationsetting-method-deleteencryptionkey.md)|從報表伺服器資料庫中刪除加密金鑰。|  
|[GenerateDatabaseCreationScript](configurationsetting-method-generatedatabasecreationscript.md)|產生可用來建立報表伺服器資料庫的 SQL 指令碼。|  
|[GenerateDatabaseRightsScript](configurationsetting-method-generatedatabaserightsscript.md)|產生可用來將報表伺服器資料庫之權限授與使用者的 SQL 指令碼。|  
|[GenerateDatabaseUpgradeScript](configurationsetting-method-generatedatabaseupgradescript.md)|產生可用來升級報表伺服器資料庫的 SQL 指令碼。|  
|[GetAdminSiteUrl 方法&#40;WMI&#41;](configurationsetting-method-getadminsiteurl.md)|取得管理中心網站的絕對 URL。|  
|[GetDatabaseVersionDisplayName](configurationsetting-method-getdatabaseversiondisplayname.md)|取得給定報表伺服器資料庫版本字串的顯示名稱。|  
|[InitializeReportServer](configurationsetting-method-initializereportserver.md)|初始化指定的報表伺服器執行個體。|  
|[ListInstalledSharePointVersions 方法&#40;WMI&#41;](configurationsetting-method-listinstalledsharepointversions.md)|傳回一組 Token，這些 Token 代表與報表伺服器安裝在同一部電腦上的 [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] [!INCLUDE[offSPServ](../../includes/offspserv-md.md)], [!INCLUDE[SPF2010](../../includes/spf2010-md.md)]或 [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] 版本。|  
|[ListIPAddresses 方法&#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-method-listipaddresses.md)|列出電腦的 IP 位址。|  
|[ListReportServersInDatabase](configurationsetting-method-listreportserversindatabase.md)|傳回存在報表伺服器資料庫中之報表伺服器安裝的清單，不論這些安裝是否具有安全資訊的存取權都一樣。|  
|[ListReservedURLs 方法&#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-method-listreservedurls.md)|列出針對報表伺服器上所有應用程式保留的 URL。|  
|[ListSSLCertificateBindings 方法&#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-method-listsslcertificatebindings.md)|列出存在 HTTP.SYS 中的 SSL 憑證繫結以及預期來自 rsreportserver.config 的 SSL 憑證繫結。|  
|[ListSSLCertificates 方法&#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-method-listsslcertificates.md)|列出電腦上的已安裝 SSL 憑證。|  
|[ReencryptSecureInformation](configurationsetting-method-reencryptsecureinformation.md)|產生新的加密金鑰，並且使用這個新的金鑰來重新加密報表伺服器資料庫中的所有安全資訊。|  
|[RemoveSSLCertificateBindings 方法&#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-method-removesslcertificatebinding.md)|移除 SSL 憑證繫結。|  
|[RemoveUnattendedExecutionAccount](configurationsetting-method-removeunattendedexecutionaccount.md)|從報表伺服器組態中移除自動執行帳戶項目。|  
|[RemoveURL 方法&#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-method-removeurl.md)|移除針對報表伺服器所保留的 URL。|  
|[ReserveURL 方法&#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-method-reserveurl.md)|加入給定應用程式的 URL 保留項目。|  
|[RestoreEncryptionKey](configurationsetting-method-restoreencryptionkey.md)|將指定的加密金鑰重新套用至報表伺服器資料庫。|  
|[SetDatabaseConnection](configurationsetting-method-setdatabaseconnection.md)|設定特定報表伺服器資料庫的報表伺服器資料庫連接。|  
|[SetDatabaseLogonTimeout](configurationsetting-method-setdatabaselogontimeout.md)|指定報表伺服器資料庫登入嘗試的預設逾時值。|  
|[SetDatabaseQueryTimeout](configurationsetting-method-setdatabasequerytimeout.md)|指定報表伺服器資料庫連接的預設逾時值。|  
|[SetEmailConfiguration](configurationsetting-method-setemailconfiguration.md)|設定報表伺服器用來傳送電子郵件的電子郵件傳遞延伸模組。|  
|[SetSecureConnectionLevel](configurationsetting-method-setsecureconnectionlevel.md)|設定報表伺服器的安全連接層級。|  
|[SetServiceState](configurationsetting-method-setservicestate.md)|開啟和關閉報表伺服器 Windows 與 Web 服務。|  
|[SetUnattendedExecutionAccount](configurationsetting-method-setunattendedexecutionaccount.md)|指定用來自動執行報表的帳戶。|  
|[SetVirtualDirectory 方法&#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-method-setvirtualdirectory.md)|設定應用程式的虛擬目錄。|  
|[SetWindowsServiceIdentity](configurationsetting-method-setwindowsserviceidentity.md)|讓報表伺服器 Windows 服務以指定之 Windows 使用者的身分執行，並且授與此帳戶足夠的檔案系統權限，以便允許報表伺服器運作。|  
  
## <a name="see-also"></a>另請參閱  
 [MSReportServer_ConfigurationSetting 類別](msreportserver-configurationsetting-class.md)  
  
  
