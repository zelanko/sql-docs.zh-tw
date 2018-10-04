---
title: MSReportServer_ConfigurationSetting 方法 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
api_name:
- MSReportServer_ConfigurationSetting Methods
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- WMI provider [Reporting Services], MSReportServer_ConfigurationSetting class
- MSReportServer_ConfigurationSetting class
ms.assetid: a08c2476-5b8e-4792-94da-1360fe231c6e
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 0bfe72762875d2c92b78a985a5b8239eefd9256a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48182698"
---
# <a name="msreportserverconfigurationsetting-methods"></a>MSReportServer_ConfigurationSetting 方法
  報表伺服器 WMI 提供者的 MSReportServer_ConfigurationSetting 類別會提供下列公用方法。  
  
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
|[ListInstalledSharePointVersions 方法&#40;WMI&#41;](configurationsetting-method-listinstalledsharepointversions.md)|傳回一組 Token，這些 Token 代表與報表伺服器安裝在同一部電腦上的 Microsoft [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] [!INCLUDE[offSPServ](../../includes/offspserv-md.md)], [!INCLUDE[SPF2010](../../includes/spf2010-md.md)]或 [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] 版本。|  
|[ListIPAddresses 方法&#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-method-listipaddresses.md)|列出電腦的 IP 位址。|  
|[ListReportServersInDatabase](configurationsetting-method-listreportserversindatabase.md)|傳回存在報表伺服器資料庫中之報表伺服器安裝的清單，不論這些安裝是否具有安全資訊的存取權都一樣。|  
|[ListReservedURLs 方法&#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-method-listreservedurls.md)|列出針對報表伺服器上所有應用程式保留的 URL。|  
|[ListSSLCertificateBindings 方法&#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-method-listsslcertificatebindings.md)|列出存在 HTTP.SYS 中的 SSL 憑證繫結以及預期來自 RSReportServer.config 的 SSL 憑證繫結。|  
|[ListSSLCertificates 方法&#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-method-listsslcertificates.md)|列出電腦上的已安裝 SSL 憑證。|  
|[ReencryptSecureInformation](configurationsetting-method-reencryptsecureinformation.md)|產生新的加密金鑰，並且使用這個新的金鑰來重新加密報表伺服器資料庫中的所有安全資訊。|  
|[RemoveSSLCertificateBindings 方法&#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-method-removesslcertificatebinding.md)|移除 SSL 憑證繫結。|  
|[RemoveUnattendedExecutionAccount](configurationsetting-method-removeunattendedexecutionaccount.md)|從報表伺服器組態中移除自動執行帳戶項目。|  
|[RemoveURL 方法&#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-method-removeurl.md)|移除針對報表伺服器所保留的 URL。|  
|[ReserveURL 方法&#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-method-reserveurl.md)|加入給定應用程式的 URL 保留項目。|  
|[RestoreEncryptionKey](configurationsetting-method-restoreencryptionkey.md)|將指定的加密金鑰重新套用至報表伺服器資料庫。|  
|[SetDatabaseConnection](configurationsetting-method-setdatabaseconnection.md)|設定特定報表伺服器資料庫的報表伺服器資料庫連接。|  
|[SetDatabaseLogonTimeout](configurationsetting-method-setdatabaselogontimeout.md)|指定報表伺服器資料庫登入嘗試的預設逾時值。|  
|[SetDatabaseQueryTimeout](configurationsetting-method-setdatabasequerytimeout.md)|指定報表伺服器資料庫查詢的預設逾時值。|  
|[SetEmailConfiguration](configurationsetting-method-setemailconfiguration.md)|設定報表伺服器用來傳送電子郵件的電子郵件傳遞延伸模組。|  
|[SetSecureConnectionLevel](configurationsetting-method-setsecureconnectionlevel.md)|設定報表伺服器的安全連接層級。|  
|[SetServiceState](configurationsetting-method-setservicestate.md)|開啟和關閉報表伺服器服務。|  
|[SetUnattendedExecutionAccount](configurationsetting-method-setunattendedexecutionaccount.md)|指定用來自動執行報表的帳戶。|  
|[SetVirtualDirectory 方法&#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-method-setvirtualdirectory.md)|設定應用程式的虛擬目錄。|  
|[SetWindowsServiceIdentity](configurationsetting-method-setwindowsserviceidentity.md)|讓報表伺服器服務以指定之 Windows 使用者的身分執行，並且授與此帳戶足夠的檔案系統權限，以便允許報表伺服器運作。|  
  
## <a name="see-also"></a>另請參閱  
 [MSReportServer_ConfigurationSetting 類別](msreportserver-configurationsetting-class.md)  
  
  
