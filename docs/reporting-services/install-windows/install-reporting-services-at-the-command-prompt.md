---
title: "安裝 Reporting Services，在命令提示字元 |Microsoft 文件"
ms.custom:
- SQL2016_New_Updated
ms.date: 09/25/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- command line
ms.assetid: 048169b3-512c-41e4-895a-0416eff41268
caps.latest.revision: 11
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: f2c8586ba26169bdd236f825b9f9688106788fff
ms.contentlocale: zh-tw
ms.lasthandoff: 08/09/2017

---
# <a name="install-reporting-services-at-the-command-prompt"></a>在命令提示字元安裝 Reporting Services

[!INCLUDE[ssrs-appliesto-sql2016-xpreview](../../includes/ssrs-appliesto-sql2016-xpreview.md)]

[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 支援從 SQL Server 安裝程式進行命令列安裝。 本主題包含數個 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]特有的命令列安裝範例。 如需所有 SQL Server 元件之可用命令列選項的完整說明，請參閱 [從命令提示字元安裝 SQL Server 2016](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)。 本主題不會就 SharePoint 產品之 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 增益集的命令列選項進行說明。 如需增益集的命令安裝相關資訊，請參閱 [使用安裝檔 rsSharePoint.msi 安裝增益集](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md#bkmk_install_rssharepoint)。

##  <a name="bkmk_native_mode"></a> 原生模式 Reporting Services

### <a name="rsinstallmode-native-mode"></a>RSINSTALLMODE (原生模式)
 安裝 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 的主要輸入設定為 **/RSINSTALLMODE** 輸入設定。 此設定包含兩個選項： **DefaultNativeMode** 和 **FilesOnlyMode**  
  
 如果安裝包含 SQL Server Database Engine，預設 RSINSTALLMODE 為 DefaultNativeMode。如果安裝不包含 SQL Server Database Engine，預設 RSINSTALLMODE 為 FilesOnlyMode。如果選擇 DefaultNativeMode 但安裝不包含 SQL Server Database Engine，安裝會自動將 RSINSTALLMODE 變更為 FilesOnlyMode。 如需輸入設定的詳細資訊，請參閱 [從命令提示字元安裝 SQL Server 2016](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)。

### <a name="examples-of-native-mode-installation"></a>原生模式安裝範例

 下例會安裝下列項目並設定帳戶︰  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 。  
  
-   [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]。  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 訂閱功能需要的 SQL Server Agent。  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]特有的命令列安裝範例。  
  
```  
Setup.exe /q /IACCEPTSQLSERVERLICENSETERMS /ACTION="install" /ERRORREPORTING=1 /UPDATEENABLED="False" /INSTANCENAME="MSSQLSERVER" /FEATURES="SQLEngine,Adv_SSMS,RS" /RSINSTALLMODE="DefaultNativeMode" /SQLSVCACCOUNT="[DOMAIN\ACCOUNT]" /SQLSVCPASSWORD="[PASSWORD]" /AGTSVCACCOUNT="[DOMAIN\ACCOUNT]" /AGTSVCPASSWORD="[PASSWORD]" /SQLSYSADMINACCOUNTS="[DOMAIN\ACCOUNT]"  
```  
  
##  <a name="bkmk_sharepoint_mode"></a> SharePoint 模式 Reporting Services  
  
### <a name="rsshpinstallmode-sharepoint-mode"></a>RSSHPINSTALLMODE (SharePoint 模式)  
 在 SharePoint 模式中安裝 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 的輸入設定是 **/RSSHPINSTALLMODE**。 此輸入設定包含一個選項：SharePointFilesOnlyMode。 這個選項會安裝 SharePoint 模式所需的所有檔案，但是安裝之後需要進行設定。 額外設定步驟是使用 SharePoint 管理中心完成。 如需詳細資訊，請參閱 [在 SharePoint 模式中安裝第一部報表伺服器](http://msdn.microsoft.com/en-us/b29d0f45-0068-4c84-bd7e-5b8a9cd1b538)。  
  
### <a name="examples-of-sharepoint-mode-installation"></a>SharePoint 模式安裝範例  
 以下範例將安裝 SQL Server 資料庫引擎服務和 SharePoint 模式的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ，以及適用於 SharePoint 的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 增益集 (RS_SHPWFE)。  
  
```  
setup /q /ACTION=install /FEATURES=SQL, RS_SHP, RS_SHPWFE,TOOLS /INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="BUILTIN\ADMINISTRATORS" /RSSVCACCOUNT="NT AUTHORITY\NETWORK SERVICE" /SQLSVCACCOUNT="NT AUTHORITY\NETWORK SERVICE" /AGTSVCACCOUNT="NT AUTHORITY\NETWORK SERVICE"  
```  
  
 以下範例只會安裝 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式。  
  
```  
Setup.exe /q /ACTION="Install" /IACCEPTSQLSERVERLICENSETERMS /FEATURES="RS_SHP" /INSTANCEDIR="C:\Program Files\Microsoft SQL Server" /INSTALLSHAREDDIR="C:\Program Files\Microsoft SQL Server" /INSTALLSHAREDWOWDIR="C:\Program Files (x86)\Microsoft SQL Server" /INSTALLSQLDATADIR="C:\Program Files\Microsoft SQL Server" /SECURITYMODE="SQL" /SAPWD="[PASSWORD]" /PID="[Your PID Value]" /SQLSYSADMINACCOUNTS="[Account Name]" "AutoSql Admin Group" /ASSYSADMINACCOUNTS="[Account Name]" /UPDATEENABLED="False"  
  
```  
  
### <a name="examples-of-sharepoint-mode-upgrade"></a>SharePoint 模式升級範例  
 下列範例會升級 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式。 **RSUPGRADEPASSWORD** 是現有報表伺服器服務帳戶的密碼。 除非 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務帳戶是內建帳戶，否則在升級案例中，RSUPGRADEPASSWORD 是必填欄位。  
  
```  
Setup.exe /q /ACTION="Upgrade" /INSTANCENAME="MSSQLSERVER" /PID="[PID value]" /FTSVCACCOUNT="[DOMAIN\ACCOUNT]" /FTSVCPASSWORD="[PASSWORD]" /UPDATEENABLED="False" /IACCEPTSQLSERVERLICENSETERMS /RSUPGRADEPASSWORD="[PASSWORD]"  
```  
  
 下列範例可用於升級使用 SharePoint 共用服務架構為基礎的 SharePoint 模式安裝。 此範例會使用切換參數 ALLOWUPGRADEFORSSRSSHAREPOINTMODE。 若要升級不是以共用服務架構為基礎的舊版本，不需要此參數：  
  
-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  
  
-   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]  
  
```  
Setup.exe /q /ACTION="Upgrade" /INSTANCENAME="MSSQLSERVER" /PID="[Your PID Value]" /FTSVCACCOUNT="[ACCOUNT Name]" /FTSVCPASSWORD="[PASSWORD]" /UPDATEENABLED="False" /IACCEPTSQLSERVERLICENSETERMS /ALLOWUPGRADEFORSSRSSHAREPOINTMODE="True"  
```

## <a name="next-steps"></a>後續的步驟

[從命令提示字元安裝 SQL Server 2016](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)   
[SysPrep 參數](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md#SysPrep)   
[從命令提示字元安裝 Power Pivot](http://msdn.microsoft.com/en-us/7f1f2b28-c9f5-49ad-934b-02f2fa6b9328)  

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](http://go.microsoft.com/fwlink/?LinkId=620231)
