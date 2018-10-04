---
title: 教學課程的必要條件 (報表產生器) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 9b8346a6-f4f4-4ad3-bc98-8f2be342ef2d
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 2d1807caf5b5ef2687121dd465e87eb55b9fd2df
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48056208"
---
# <a name="prerequisites-for-tutorials-report-builder"></a>教學課程的必要條件 (報表產生器)
  報表產生器教學課程希望您能夠在報表伺服器或與報表伺服器整合的 SharePoint 網站上檢視和儲存報表。 針對資料，所有教學課程都使用必須由 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]處理的常值查詢。  
  
 如果您沒有報表伺服器或網站或是資料來源的存取權，可以透過建立離線報表來了解報表產生器。 請參閱[教學課程：離線建立快速圖表報表 &#40;報表產生器&#41;](report-builder/tutorial-create-a-quick-chart-report-offline-report-builder.md)。  
  
## <a name="requirements"></a>需求  
 您必須擁有下列必要元件，才能完成報表產生器教學課程：  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 報表產生器的存取權。 您可以使用獨立版的報表產生器，或者報表管理員或 SharePoint 網站提供的 ClickOnce 版本來執行報表產生器。 只有第一個步驟「如何開啟報表產生器」與 ClickOnce 版本不同。  
  
     若要使用報表管理員中，開啟報表管理員，然後按一下**報表產生器**。 根據預設，報表管理員 URL 是 http://\<*servername*> / 報告。  
  
     若要使用 SharePoint 網站，請巡覽至網站，依序按一下 [文件] 索引標籤和 [新增文件]，然後從下拉式清單按一下 [報表產生器報表]。 例如 http://\<伺服器名稱 >/網站/mySite/報表。 SharePoint 管理員必須啟用每一個文件庫的 [報表產生器報表] 功能。  
  
-   至 URL [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)]報表伺服器或 SharePoint 網站整合[!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)]報表伺服器。 您必須具有權限，才能儲存和檢視報表、共用資料來源、共用資料集、報表組件和模型。 根據預設，報表伺服器的 URL 為 http://\<伺服器名稱 > / reportserver。 根據預設，SharePoint 網站的 URL 為 http://\<站台名稱 > 或 http://\<伺服器 > / 站台。  
  
-   名稱[!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]執行個體和能夠以唯讀方式存取任何資料庫的認證。 教學課程中的資料集查詢會使用常值資料，但是每一個查詢都必須經過 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 執行個體處理，才能傳回報表資料集所需的中繼資料。 例如，下列連接字串僅指定伺服器：`data source=<servername>`。 您必須由授與您存取此伺服器之權限的系統管理員，指派具有預設資料庫的讀取存取權。 您也可以指定資料庫，如下列連接字串所示： `data source=<servername>;initial catalog=<database>`。  
  
-   至於包含地圖的教學課程，報表伺服器必須設定為支援 Bing Maps 做為背景。 如需詳細資訊，請參閱 <<c0> [ 對應報表支援規劃](plan-for-map-report-support.md)中[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]中的文件[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][線上叢書 》](http://go.microsoft.com/fwlink/?LinkId=154888) msdn.microsoft.com 上。  
  
-   教學課程中，[教學課程： 建立鑽研及主報表&#40;報表產生器&#41;](tutorial-creating-drillthrough-and-main-reports-report-builder.md)，會使用 Contoso 商業智慧示範資料集。 此資料集是由 ContosoDW 資料倉儲與 Contoso_Retail 線上分析處理 (OLAP) 資料庫所組成。 您將在此教學課程中建立的報表會從 Contoso Sales Cube 擷取報表資料。 Contoso_Retail OLAP 資料庫可以從 [Microsoft 下載中心](http://go.microsoft.com/fwlink/?LinkID=191575)下載。 您只需要下載 ContosoBIdemoABF.exe 檔。 它包含 OLAP 資料庫。  
  
     另一個檔案 ContosoBIdemoBAK.exe 則是供 ContosoDW 資料倉儲使用，在此教學課程中不會使用這個檔案。  
  
     此網站包含解壓縮 ContosoRetail.abf 備份檔案，並將其還原至 Contoso_Retail OLAP 資料庫的指示。  
  
     您必須能夠存取要在其上安裝 OLAP 資料庫的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體。  
  
 報表伺服器管理員必須授必要的權限，在報表伺服器上，與您設定[!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)]資料夾位置，以及設定報表產生器的預設選項。 如需詳細資訊，請參閱 <<c0> [ 安裝、 解除安裝，以及報表產生器支援](install-uninstall-and-report-builder-support.md)。  
  
## <a name="see-also"></a>另請參閱  
 [教學課程&#40;報表產生器&#41;](report-builder-tutorials.md)  
  
  
