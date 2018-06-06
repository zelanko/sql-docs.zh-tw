---
title: 儲存報表 (報表產生器) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-builder
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 59ddc4b8-9517-4d3f-9c88-a07e9907cecb
caps.latest.revision: 9
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: fbf40f6911d3d8a77bfc37a749a12864b775ebd1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="saving-reports-report-builder"></a>儲存報表 (報表產生器)
  在報表產生器中，您可以將分頁報表儲存至 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 報表伺服器、SharePoint 文件庫、您具有寫入權限的檔案共用或您的電腦。 
  
當您儲存報表時，您實際上儲存的是報表定義，報表定義會描述報表配置。 您不會儲存資料。 每當您執行報表時，便會重新整理報表資料，而且報表資料可能會與您上次執行報表時的資料不同。  
  
 如果您想要將報表儲存到另一個格式或是儲存具有資料的報表定義，請使用下列其中一個 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 功能：  
  
-   將轉譯的報表匯出成另一個檔案格式，如逗號分隔的檔案 (CSV) 或 Excel 活頁簿，然後使用該格式儲存報表。 您也可以從報表產生資料摘要，並儲存報表資料。  
  
-   建立要傳遞的報表訂閱，並將報表儲存到檔案共用位置。  
  
-   使用報表記錄，將轉譯的報表版本儲存為歷程記錄複本。  
  
 若要深入了解如何直接在報表伺服器上檢視及管理報表，請參閱[尋找、檢視和管理報表 &#40;報表產生器及 SSRS &#41;](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md) 和 [Reporting Services 報表伺服器 &#40;原生模式&#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)。  
  
##  <a name="SavingReportDefinitions"></a> 將報表儲存到報表伺服器  
  將報表儲存到報表伺服器也稱為發行報表。 雖然您可以將報表儲存到電腦，但是將報表儲存到報表伺服器會提供許多優點：  
  
-   報表會提供給有權存取報表儲存所在之資料夾的其他人使用。  
  
-   您可以在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 入口網站上管理及檢視報表。  
  
-   類似資料來源、影像和子報表的報表資源會儲存在一個地方，讓使用者方便存取。  
  
-   報表可以透過訂閱傳遞給其他人。  
  
-   報表會安全地儲存在報表伺服器資料庫中。  
  
-   報表執行可以記錄下來，並提供效能和稽核資訊。  
  
##  <a name="ExportingAndSavingReports"></a> 匯出與儲存報表  
 若您要封存的報表數量很少，請考慮將報表匯出，並將它儲存成檔案。 在您將報表匯出至應用程式 (例如 PDF 或 Excel) 後，可以將它另存新檔，並放在網路上一個受保護的共用目錄下。 或者，如果您想要在報表伺服器資料庫中，保留報表的所有複本 (不論何種格式)，您可以將已經儲存的 PDF 或 Excel 檔案，做為資源項目進行上傳。 如需匯出報表的詳細資訊，請參閱 [匯出報表 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md) 和 [上傳檔案或報表](../../reporting-services/reports/upload-a-file-or-report-report-manager.md)。  
  
##  <a name="UsingFileShareDelivery"></a> 使用檔案共用傳遞  
 如果您要封存的報表數量很多，請建立訂閱，將報表直接傳遞到檔案系統。 若要使用此方式，您必須對每一個報表建立訂閱、選擇共用資料夾來儲存報表，並且定義排程以決定何時建立檔案。 一旦完成訂閱的定義，報表伺服器就可以使用您所提供的排程，自動執行報表並將報表檔案加入封存。 如果只是偶爾要封存報表，就可以建立僅使用一次的排程。 如需訂閱和檔案共用傳遞的詳細資訊，請參閱 [Reporting Services 中的檔案共用傳遞](../../reporting-services/subscriptions/file-share-delivery-in-reporting-services.md)。  
  
##  <a name="UsingReportHistory"></a> 使用報表記錄  
 您也可以使用報表記錄功能來建立歷程記錄複本。 然後就可以備份報表伺服器資料庫，並將備份儲存於安全的位置以供未來使用。 所有的報表記錄 (連同報表、共用資料來源項目、資料夾、訂閱和共用排程) 都會儲存在報表伺服器資料庫中。 您可以建立備份，以永久保留一份報表記錄和中繼資料的副本 (例如指出報表收件者的訂閱資訊)。 如需詳細資訊，請參閱 [建立、修改及刪除報表記錄中的快照集](../../reporting-services/report-server/create-modify-and-delete-snapshots-in-report-history.md)。  
 
##  <a name="HowTo"></a> 如何主題  
  
-   [將報表儲存到報表伺服器 &#40;報表產生器&#41;](../../reporting-services/report-builder/save-reports-to-a-report-server-report-builder.md)  
  
-   [將報表儲存至 SharePoint 文件庫 &#40;報表產生器&#41;](../../reporting-services/report-builder/save-a-report-to-a-sharepoint-library-report-builder.md)  
   
## <a name="see-also"></a>另請參閱  
 [報表、報表組件和報表定義 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/reports-report-parts-and-report-definitions-report-builder-and-ssrs.md)   
 [安裝和解除安裝報表產生器](http://msdn.microsoft.com/library/2c9a5814-17bf-4947-8fb3-6269e7caa416)   
 [尋找、檢視和管理報表 &#40;報表產生器及 SSRS &#41;](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [匯出報表 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md)   
 [列印報表 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-builder/print-reports-report-builder-and-ssrs.md)  
  
  
