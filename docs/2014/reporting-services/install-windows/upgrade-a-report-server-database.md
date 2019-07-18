---
title: 升級報表伺服器資料庫 | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- upgrading databases
- report server database
- upgrading Reporting Services
ms.assetid: 4091cf87-9d97-4048-a393-67f1f9207401
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e3ba4d9ee2e0b92617c2d2bcadae3bf87c8b5414
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66108643"
---
# <a name="upgrade-a-report-server-database"></a>升級報表伺服器資料庫
  報表伺服器資料庫為一個或多個報表伺服器執行個體提供了儲存裝置。 由於報表伺服器資料庫結構描述可隨著每個新的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]版本一起變更，所以此資料庫版本必須符合您所使用的報表伺服器執行個體版本。 在大多數情況下，報表伺服器資料庫可以自動升級，而不需要您採取特定的動作。  
  
 **原生模式：** 在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]原生模式，報表伺服器資料庫實際上由組成的兩個具有預設名稱為"ReportServer 和 ReportServerTempDB"的資料庫。  
  
 **SharePoint 模式：** 在  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式報表伺服器資料庫是實際的資料庫集合是針對每個執行個體建立[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]服務應用程式。  
  
## <a name="ways-to-upgrade-a-native-mode-report-server-database"></a>升級原生模式報表伺服器資料庫的方法  
 下列清單會識別升級報表伺服器資料庫的狀況：  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式會升級報表伺服器的單一執行個體。 報表伺服器資料庫結構描述會在服務啟動之後自動升級，而且報表伺服器會判斷此資料庫結構描述是否與伺服器版本不符。  
  
     當服務啟動時，報表伺服器會檢查資料庫結構描述版本，以便確認它是否符合伺服器版本。 如果資料庫結構描述版本是較舊的版本，它就會自動升級為報表伺服器所需的結構描述版本。 如果您還原或附加舊版的報表伺服器資料庫，自動升級會特別實用。 報表伺服器追蹤記錄檔中會輸入一則訊息，表示資料庫結構描述版本已升級。  
  
-   當您選取要搭配新的報表伺服器執行個體使用的舊版時， [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員會升級本機或遠端報表伺服器資料庫。 若為上述情況，您就必須在升級動作發生之前先進行確認。  
  
     [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員不再提供個別的 [升級] 按鈕或升級指令碼。 這些功能從 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 開始已過時，因為報表伺服器服務有自動升級功能。  
  
 在更新結構描述之後，便無法將此項升級回復成先前的版本。 一定要備份報表伺服器資料庫，以防之後需要重新建立先前的安裝。  
  
## <a name="how-the-schema-metadata-and-report-server-content-is-updated"></a>如何升級結構描述、中繼資料和報表伺服器內容  
 報表伺服器資料庫的升級作業共分三個階段：  
  
1.  在安裝和服務啟動之後，或是當您在舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員中選取 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 原生模式報表伺服器資料庫時，結構描述會自動升級。 此外，報表伺服器服務會在啟動時檢查資料庫版本。 如果報表伺服器連接到舊版的資料庫，報表伺服器將會在啟動時更新此資料庫。  
  
2.  安全性描述項會在更新結構描述之後第一次使用報表伺服器資料庫時升級。  
  
3.  已發行的報表和已編譯的報表快照集都在第一次使用時升級。 如需詳細資訊，請參閱 [Upgrade Reports](upgrade-reports.md)。  
  
 除了報表伺服器資料庫之外，報表伺服器也使用暫存資料庫。 當您升級報表伺服器資料庫時，會自動升級暫存資料庫。  
  
## <a name="permissions-required-to-upgrade-a-report-server-database"></a>升級報表伺服器資料庫所需的權限  
 如果您正在升級的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安裝包含報表伺服器資料庫，則當執行資料庫升級時具備的權限不足時，您可能會看到錯誤訊息。 依預設，安裝程式會使用執行安裝程式之使用者的安全性 Token，以連接到遠端 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體並更新結構描述。 如果您在主控報表伺服器資料庫的資料庫伺服器上擁有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **系統管理員** 權限，資料庫升級將會成功。 同樣地，如果您從命令提示字元執行安裝程式，並為具有修改遠端電腦結構描述之 **系統管理員** 權限的帳戶指定 RSUPGRADEDATABASEACCOUNT 和 RSUPGRADEPASSWORD 引數，資料庫升級將會成功。  
  
 然而，如果您沒有遠端電腦之資料庫的 **系統管理員** 權限，則連線會遭到拒絕，並傳回下列錯誤：  
  
 `"Setup was not able to upgrade the report server database schema. You must update the database schema manually after setup is finished. To update the schema, run the Reporting Services Configuration Manager, open the Database Setup page, re-select the database, and click Apply. The database will be upgraded automatically."`  
  
 在此時，報表伺服器程式檔案將會升級，但報表伺服器資料庫則為舊版格式。 在您手動升級資料庫來完成升級程序之前，將無法使用此報表伺服器。  
  
#### <a name="to-upgrade-a-native-mode-database-with-scripts"></a>若要使用指令碼升級原生模式資料庫  
 您可以使用 WMI 指令碼來升級報表伺服器資料庫。 如需詳細資訊，請參閱 [GenerateDatabaseUpgradeScript 方法 &#40;WMI MSReportServer_ConfigurationSetting&#41;](../wmi-provider-library-reference/configurationsetting-method-generatedatabaseupgradescript.md)  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 組態管理員 &#40;原生模式&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)   
 [建立報表伺服器資料庫 &#40;SSRS 組態管理員&#41;](../../sql-server/install/create-a-report-server-database-ssrs-configuration-manager.md)   
 [變更資料庫精靈 &#40;SSRS 原生模式&#41;](../../sql-server/install/change-database-wizard-ssrs-native-mode.md)   
 [升級和移轉 Reporting Services](upgrade-and-migrate-reporting-services.md)   
 [移轉 Reporting Services 安裝 &#40;原生模式&#41;](migrate-a-reporting-services-installation-native-mode.md)  
  
  
