---
title: Reporting Services 的備份與還原作業 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- databases [Reporting Services], backing up
- databases [Reporting Services], restoring
- databases [Reporting Services], moving
- backing up databases [Reporting Services]
- moving databases
- restoring databases [Reporting Services]
- files [Reporting Services], restoring
- files [Reporting Services], backing up
ms.assetid: 157bc376-ab72-4c99-8bde-7b12db70843a
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 8c992148017f6a3ecb383e85ad5bbfcc3a3ec3c8
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66108913"
---
# <a name="backup-and-restore-operations-for-reporting-services"></a>Reporting Services 的備份與還原作業
  此主題提供所有用於 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安裝中資料檔案的概觀，並說明備份這些檔案的時機與方法。 復原策略中最重要的部分，就是訂定報表伺服器資料庫檔案的備份與還原計劃。 但是，更加完整的復原策略應該要包括加密金鑰、自訂組件或延伸模組、組態檔以及報表和模型之來源檔案的備份。  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 原生模式 | [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式  
  
 備份和還原作業常用於移動 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安裝的全部或一部分：  
  
-   如果僅移動報表伺服器資料庫，您可以透過備份與還原或是附加與卸離作業，將資料庫重新放置到不同的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上。 如需詳細資訊，請參閱 [將報表伺服器資料庫移至其他電腦 &#40;SSRS 原生模式&#41;](../report-server/moving-the-report-server-databases-to-another-computer-ssrs-native-mode.md)。  
  
-   將 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安裝移動到新的電腦上，稱為移轉。 您移轉安裝時，會執行安裝程式以安裝新的報表伺服器執行個體，然後將執行個體資料複製到新的電腦上。 如需有關移轉 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安裝的詳細資訊，請參閱下列主題：  
  
    -   [升級和移轉 Reporting Services](upgrade-and-migrate-reporting-services.md)  
  
    -   [遷移 Reporting Services 安裝 &#40;SharePoint 模式&#41;](migrate-a-reporting-services-installation-sharepoint-mode.md)  
  
    -   [遷移 Reporting Services 安裝 &#40;原生模式&#41;](migrate-a-reporting-services-installation-native-mode.md)  
  
## <a name="backing-up-the-report-server-databases"></a>備份報表伺服器資料庫  
 由於報表伺服器是無狀態伺服器，因此所有應用程式資料都會儲存在 **執行個體上執行的** reportserver **與** reportservertempdb [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 資料庫中。 您可以使用其中一種支援的 **資料庫備份方法，備份** reportserver **與** reportservertempdb [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫。 報表伺服器資料庫的特定建議事項如下：  
  
-   使用完整復原模式備份 **reportserver** 資料庫。  
  
-   使用簡易復原模式備份 **reportservertempdb** 資料庫。  
  
-   您可以針對每個資料庫使用不同的備份排程。 備份 **reportservertempdb** 的唯一理由，是避免在發生硬體故障時必須重新建立資料庫。 如果發生硬體故障，您不必復原 **reportservertempdb**中的資料，只需要資料表結構。 如果您遺失 **reportservertempdb**，要再度獲得資料庫的唯一方法是重新建立報表伺服器資料庫。 如果您重新建立 **reportservertempdb**，請務必確認此資料庫的名稱與主要報表伺服器資料庫的名稱相同。  
  
 如需備份和復原 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 關聯式資料庫的詳細資訊，請參閱 [SQL Server 資料庫的備份與還原](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)。  
  
> [!IMPORTANT]  
>  如果您的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 報表伺服器處於 SharePoint 模式，則要連接其他資料庫，包括 SharePoint 組態資料庫和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 警示資料庫。 在 SharePoint 模式下，系統會針對每個 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務應用程式建立三個資料庫。 **reportserver**、 **reportservertempdb**和 **dataalerting** 資料庫。 如需詳細資訊，請參閱 [備份與還原 Reporting Services SharePoint 服務應用程式](../backup-and-restore-reporting-services-sharepoint-service-applications.md)  
  
## <a name="backing-up-the-encryption-keys"></a>備份加密金鑰  
 當您第一次設定 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安裝時，應該要備份加密金鑰。 每次變更服務帳戶的身分或重新命名電腦時，您也應該同時備份加密金鑰。 如需詳細資訊，請參閱 [備份與還原 Reporting Services 加密金鑰](ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)。 針對 SharePoint 模式的報表伺服器，請參閱[管理 Reporting Services SharePoint 服務應用程式](../manage-a-reporting-services-sharepoint-service-application.md)的＜金鑰管理＞一節。  
  
## <a name="backing-up-the-configuration-files"></a>備份組態檔  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 會使用組態檔來儲存應用程式設定。 您應該在第一次設定伺服器時，以及部署任何自訂延伸模組之後，備份組態檔。 要備份的檔案包括：  
  
-   RSReportServer.config  
  
-   Rssvrpolicy.config  
  
-   Rsmgrpolicy.config  
  
-   Reportingservicesservice.exe.config  
  
-   報表伺服器和報表管理員 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 應用程式的 Web.config  
  
-   Machine.config [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)]  
  
## <a name="backing-up-data-files"></a>備份資料檔案  
 備份您在報表設計師和模型設計師中建立與維護的檔案。 這些包括報表定義 (.rdl) 檔案、報表模型 (.smdl) 檔案、共用資料來源 (.rds) 檔案、資料檢視 (.dv) 檔案、資料來源 (.ds) 檔案、報表伺服器專案 (.rptproj) 檔案，以及報表方案 (.sln) 檔案。  
  
 請記得備份任何為管理或部署工作所建立的指令碼檔案 (.rss)。  
  
 確認您有所使用之任何自訂延伸模組與自訂組件的備份副本。  
  
## <a name="see-also"></a>另請參閱  
 [報表伺服器資料庫 &#40;SSRS 原生模式&#41;](../report-server/report-server-database-ssrs-native-mode.md)   
 [Reporting Services 組態檔](../report-server/reporting-services-configuration-files.md)   
 [rskeymgmt 公用程式 &#40;SSRS&#41;](../tools/rskeymgmt-utility-ssrs.md)   
 [使用備份與還原複製資料庫](../../relational-databases/databases/copy-databases-with-backup-and-restore.md)   
 [管理報表伺服器資料庫 &#40;SSRS 原生模式&#41;](../report-server/administer-a-report-server-database-ssrs-native-mode.md)   
 [設定和管理加密金鑰 &#40;SSRS 組態管理員&#41;](ssrs-encryption-keys-manage-encryption-keys.md)  
  
  
