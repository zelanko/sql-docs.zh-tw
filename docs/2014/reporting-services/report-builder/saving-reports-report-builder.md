---
title: 儲存報表 (報表產生器) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 59ddc4b8-9517-4d3f-9c88-a07e9907cecb
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 37620b099bf07d8c38472dc211040d9efb252992
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48182038"
---
# <a name="saving-reports-report-builder"></a>儲存報表 (報表產生器)
  在報表產生器中，您可以將報表儲存到報表伺服器、SharePoint 文件庫、您具有寫入權限的檔案共用位置或是您的電腦上。 您可以將報表儲存到開啟它的相同位置，也可以儲存到另一個位置，或是以新的名稱儲存到相同或不同的位置。 根據預設，報表會重新儲存到開啟它的相同位置。 當您儲存報表時，您實際上儲存的是報表定義，報表定義會描述報表配置。 您不會儲存資料。 每當您執行報表時，便會重新整理報表資料，而且報表資料可能會與您上次執行報表時的資料不同。  
  
 如果您想要將報表儲存到另一個格式或是儲存具有資料的報表定義，請使用下列其中一個 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 功能：  
  
-   將轉譯的報表匯出成另一個檔案格式，如逗號分隔的檔案 (CSV) 或 Excel 活頁簿，然後使用該格式儲存報表。 您也可以從報表產生資料摘要，並儲存報表資料。  
  
-   建立要傳遞的報表訂閱，並將報表儲存到檔案共用位置。  
  
-   使用報表記錄，將轉譯的報表版本儲存為歷程記錄複本。  
  
 若要深入了解如何直接在報表伺服器上檢視及管理報表，請參閱[尋找、檢視和管理報表 &#40;報表產生器及 SSRS &#41;](finding-viewing-and-managing-reports-report-builder-and-ssrs.md) 和 msdn.microsoft.com 上《[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [線上叢書](http://go.microsoft.com/fwlink/?LinkId=154888)》中的 [Reporting Services 報表伺服器 &#40;原生模式&#41;](../report-server/reporting-services-report-server-native-mode.md)。  
  
##  <a name="SavingReportDefinitions"></a> 儲存報表定義  
 雖然您可以將報表儲存到電腦，但是將報表儲存到報表伺服器會提供許多優點。  
  
 將報表儲存到報表伺服器會提供下列優點：  
  
-   報表會提供給有權存取報表儲存所在之資料夾的其他人使用。  
  
-   您可以從報表管理員來管理及檢視報表。  
  
-   類似資料來源、影像和子報表的報表資源會儲存在一個地方，讓使用者方便存取。  
  
-   報表可以透過訂閱傳遞給其他人。  
  
-   報表會安全地儲存在報表伺服器資料庫中。  
  
-   報表執行可以記錄下來，並提供效能和稽核資訊。  
  
 將報表儲存到報表伺服器也稱為發行報表。 當您儲存報表時，您只會儲存報表定義。 每當您執行報表時，便會重新整理報表資料，而且報表資料可能會與您上次執行報表時的資料不同。 如果您想要儲存包含資料的報表定義，您應該使用報表記錄功能。 使用這個功能時，您就可以儲存報表的複本連同報表資料。  
  

  
##  <a name="ExportingAndSavingReports"></a> 匯出與儲存報表  
 若您要封存的報表數量很少，請考慮將報表匯出，並將它儲存成檔案。 在您將報表匯出至應用程式 (例如 PDF 或 Excel) 後，可以將它另存新檔，並放在網路上一個受保護的共用目錄下。 或者，如果您想要在報表伺服器資料庫中，保留報表的所有複本 (不論何種格式)，您可以將已經儲存的 PDF 或 Excel 檔案，做為資源項目進行上傳。 如需有關匯出報表的詳細資訊，請參閱 <<c0> [ 匯出的報表&#40;報表產生器及 SSRS&#41; ](export-reports-report-builder-and-ssrs.md)並[上傳檔案或報表&#40;報表管理員&#41;](../reports/upload-a-file-or-report-report-manager.md)。</c0>  
  

  
##  <a name="UsingFileShareDelivery"></a> 使用檔案共用傳遞  
 如果您要封存的報表數量很多，請建立訂閱，將報表直接傳遞到檔案系統。 若要使用此方式，您必須對每一個報表建立訂閱、選擇共用資料夾來儲存報表，並且定義排程以決定何時建立檔案。 一旦完成訂閱的定義，報表伺服器就可以使用您所提供的排程，自動執行報表並將報表檔案加入封存。 如果只是偶爾要封存報表，就可以建立僅使用一次的排程。 如需有關訂閱和檔案共用傳遞的詳細資訊，請參閱《SQL Server 線上叢書》中 [Reporting Services 文件集](http://go.microsoft.com/fwlink/?linkid=121312) 的＜Reporting Services 中的檔案傳遞＞。  
  

  
##  <a name="UsingReportHistory"></a> 使用報表記錄  
 您也可以使用報表記錄功能來建立歷程記錄複本。 然後就可以備份報表伺服器資料庫，並將備份儲存於安全的位置以供未來使用。 所有的報表記錄 (連同報表、共用資料來源項目、資料夾、訂閱和共用排程) 都會儲存在報表伺服器資料庫中。 您可以建立備份，以永久保留一份報表記錄和中繼資料的副本 (例如指出報表收件者的訂閱資訊)。 如需詳細資訊，請參閱《SQL Server 線上叢書》中 [Reporting Services 文件集](http://go.microsoft.com/fwlink/?linkid=121312) 的＜管理報表記錄＞。  
  

  
##  <a name="HowTo"></a> 如何主題  
  
-   [將報表儲存到報表伺服器&#40;報表產生器&#41;](save-reports-to-a-report-server-report-builder.md)  
  
-   [將報表儲存至 SharePoint 文件庫&#40;報表產生器&#41;](save-a-report-to-a-sharepoint-library-report-builder.md)  
  
-   [將報表儲存到您的電腦&#40;報表產生器&#41;](../save-reports-to-your-computer-report-builder.md)  
  

  
## <a name="see-also"></a>另請參閱  
 [報表、 報表組件，以及報表定義&#40;報表產生器及 SSRS&#41;](../report-design/reports-report-parts-and-report-definitions-report-builder-and-ssrs.md)   
 [安裝、 解除安裝與報表產生器支援](../install-uninstall-and-report-builder-support.md)   
 [尋找、檢視和管理報表 &#40;報表產生器及 SSRS &#41;](finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [匯出報表&#40;報表產生器及 SSRS&#41;](export-reports-report-builder-and-ssrs.md)   
 [列印報表 &#40;報表產生器及 SSRS&#41;](print-reports-report-builder-and-ssrs.md)  
  
  
