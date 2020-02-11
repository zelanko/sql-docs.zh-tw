---
title: MSReportServer_ConfigurationSetting 屬性 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
api_name:
- MSReportServer_ConfigurationSetting Properties
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- WMI provider [Reporting Services], MSReportServer_ConfigurationSetting class
- MSReportServer_ConfigurationSetting class
ms.assetid: e75fe1e5-197b-4c65-859b-370821cad003
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 9c3937d888089f06435fece25e791b10ebbab785
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66097333"
---
# <a name="msreportserver_configurationsetting-properties"></a>MSReportServer_ConfigurationSetting 屬性
  MSReportServer_ConfigurationSetting 類別代表報表伺服器執行個體的安裝與執行階段參數。 這些設定儲存在 RSReportServer.config 組態檔中。  
  
## <a name="public-properties"></a>公用屬性  
  
|||  
|-|-|  
|[ConnectionPoolSize](configurationsetting-property-connectionpoolsize.md)|傳回報表伺服器用來與[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)]主控報表伺服器資料庫之實例進行通訊的連接集區大小。 唯讀。|  
|[DatabaseLogonAccount](configurationsetting-property-databaselogonaccount.md)|指定報表伺服器用來連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)]主控報表伺服器資料庫之實例的登入帳戶。 唯讀。|  
|[DatabaseLogonTimeout](configurationsetting-property-databaselogontimeout.md)|指定嘗試登入報表伺服器資料庫失敗之前等候的秒數。 唯讀。|  
|[DatabaseLogonType](configurationsetting-property-databaselogontype.md)|指定報表伺服器會使用 Windows 服務帳戶、Windows 使用者帳戶或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入來存取報表伺服器資料庫。 唯讀。|  
|[DatabaseName](configurationsetting-property-databasename.md)|指定主控報表伺服器資料庫之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的名稱。|  
|[DatabaseQueryTimeout](configurationsetting-property-databasequerytimeout.md)|指定命令失敗或超時之前必須經過的秒數。報表伺服器會針對 SQL Server 目錄進行處理，而非報表的資料來源。|  
|[DatabaseServerName](configurationsetting-property-databaseservername.md)|指定安裝報表伺服器資料庫之伺服器的名稱。|  
|[InstallationID 屬性](configurationsetting-property-installationid.md)|傳回特定報表伺服器執行個體的唯一識別碼。|  
|[InstanceName](configurationsetting-property-instancename.md)|指定特定電腦上報表伺服器執行個體的名稱。|  
|[IsInitialized](configurationsetting-property-isinitialized.md)|指出報表伺服器執行個體是否已初始化。  唯讀。|  
|[IsSharePointIntegrated](configurationsetting-property-issharepointintegrated.md)|指出報表伺服器是否設定為 SharePoint 整合模式。|  
|[IsWebServiceEnabled](configurationsetting-property-iswebserviceenabled.md)|指出報表伺服器 Web 服務是否已啟用。 唯讀。|  
|[IsWindowsServiceEnabled](configurationsetting-property-iswindowsserviceenabled.md)|指出是否已啟用報表伺服器 Windows 服務。 唯讀。|  
|[&#40;WMI&#41;的 MachineAccountIdentity 屬性](configurationsetting-property-machineaccountidentity.md)|取得安裝報表伺服器的電腦帳戶識別。|  
|[PathName](configurationsetting-property-pathname.md)|指定報表伺服器執行個體的安裝路徑。|  
|[SecureConnectionLevel](configurationsetting-property-secureconnectionlevel.md)|傳回 RSReportServer.config 檔案中指定的安全連接層級。|  
|[SenderEmailAddress](configurationsetting-property-senderemailaddress.md)|取得用以從報表伺服器傳送電子郵件的位址。 唯讀。|  
|[SendUsingSMTPServer](configurationsetting-property-sendusingsmtpserver.md)|指定電子郵件組態中的 SendUsing 屬性是否設定為 TRUE。|  
|[SMTPServer](configurationsetting-property-smtpserver.md)|從 RSReportServer.config 檔案中取得 SMTP 伺服器屬性。 唯讀。|  
|[UnattendedExecutionAccount](configurationsetting-property-unattendedexecutionaccount.md)|指定自動執行報表時報表伺服器所模擬的登入使用者帳戶。 唯讀。|  
|[版本](configurationsetting-property-version.md)|傳回報表伺服器的版本。|  
|[VirtualDirectoryReportManager 屬性 &#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-property-virtualdirectoryreportmanager.md)|傳回報表管理員應用程式的虛擬目錄。|  
|[VirtualDirectoryReportServer 屬性 &#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-property-virtualdirectoryreportserver.md)|傳回報表伺服器 Web 服務應用程式的虛擬目錄。|  
|[WindowsServiceIdentityActual](configurationsetting-property-windowsserviceidentityactual.md)|傳回實際執行報表伺服器 Windows 服務所使用的識別。 唯讀。|  
|[WindowsServiceIdentityConfigured](windowsserviceidentityconfigured-property.md)|傳回上次設定報表伺服器 Windows 服務執行時所使用的識別。 唯讀。|  
  
## <a name="see-also"></a>另請參閱  
 [MSReportServer_ConfigurationSetting 成員](msreportserver-configurationsetting-members.md)  
  
  
