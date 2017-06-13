---
title: "連接篩選或文件 Web 組件-SharePoint 整合模式 |Microsoft 文件"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Filter Web Part [Reporting Services]
- SharePoint integration [Reporting Services], Web Parts
- Report Viewer Web Part [Reporting Services]
- Documents Web Part [Reporting Services]
ms.assetid: 6a303135-c0ef-44cd-a423-1cea8df3dcf3
caps.latest.revision: 12
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 5745964338889cd378a109636b2f6ebbdc32db26
ms.contentlocale: zh-tw
ms.lasthandoff: 06/13/2017

---
# <a name="connect-filter-or-documents-web-part---sharepoint-integrated-mode"></a>連接篩選或文件 Web 組件-SharePoint 整合模式
  如果您使用的是 SharePoint 產品，可以建立包含篩選網頁組件或文件網頁組件以及報表檢視器網頁組件的儀表板或網頁組件頁面。 支援的版本為 [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] 或 [!INCLUDE[SPS2010](../../includes/sps2010-md.md)]。 另外也支援 [!INCLUDE[winSPServ3](../../includes/winspserv3-md.md)] 或 [!INCLUDE[offSPServ](../../includes/offspserv-md.md)] 2007。 藉由連接篩選網頁組件，使用者可以在篩選網頁組件中選取篩選值，並將值傳送到相同頁面上的參數化報表； 藉由連接文件網頁組件，使用者則可在文件庫中按一下報表，並在相鄰的報表檢視器網頁組件中檢視該報表。  
  
 篩選網頁組件可用來將值傳送給報表中的一個或多個參數。 若要使用篩選網頁組件，報表必須定義與網頁組件傳送之值、資料類型和格式相容的參數。  
  
 文件網頁組件與主網站的文件庫相關聯。 若要檢視、加入或移除文件庫中的項目，請按一下 [檢視所有網站內容]。 在 [程式庫] 中按一下 [文件]。 您可以使用 [新增]、[上傳] 和 [動作] 功能表來管理文件庫中的項目。  
  
### <a name="to-connect-a-filter-web-part"></a>連接篩選網頁組件  
  
1.  開啟或建立網頁組件頁面或儀表板。  
  
2.  在 [網站動作] 功能表上，按一下 [編輯頁面]。  
  
3.  按一下 [加入網頁組件]。  
  
4.  在 [所有網頁組件] 的 [其他] 類別目錄中，選取 [SQL Server Reporting Services 報表檢視器]。  
  
5.  按一下 **[加入]**。 Web 組件會加入區域頂端。  
  
6.  在相同網頁組件頁面或儀表板的另一個區域中，按一下 [加入網頁組件]。  
  
7.  在 [所有網頁組件] 的 [篩選] 區段中，選取網頁組件。  
  
8.  按一下 **[加入]**。 Web 組件會加入區域頂端。  
  
9. 在包含網頁組件的區段中，按一下網頁組件的 [編輯] 功能表，並依序指向 [連接]和 [Send Filter Values To (傳送篩選值至)]，然後選取 [報表檢視器  - *報表名稱*]。  
  
10. 簽入變更並儲存頁面。  
  
### <a name="to-connect-a-documents-web-part"></a>連接文件網頁組件  
  
1.  開啟或建立網頁組件頁面或儀表板。  
  
2.  在 [網站動作] 功能表上，按一下 [編輯頁面]。  
  
3.  按一下 [加入網頁組件]。  
  
4.  在 [所有網頁組件] 的 [清單和文件庫] 區段中，選取 [文件]。  
  
5.  按一下 **[加入]**。 Web 組件會加入區域頂端。  
  
6.  按一下工具窗格底部的 [套用]，然後按一下 [確定] 關閉窗格。  
  
7.  在相同網頁組件頁面或儀表板的另一個區域中，按一下 [加入網頁組件]。  
  
8.  在 [所有網頁組件] 的 [其他] 類別目錄中，選取 [SQL Server Reporting Services 報表檢視器]。  
  
9. 按一下 **[加入]**。 Web 組件會加入區域頂端。  
  
10. 在包含網頁組件的區段中，按一下網頁組件的 [編輯] 功能表，並依序指向 [連接] 和 [Get report definitions from (報表定義取得來源)]，然後選取 [文件]。  
  
11. 簽入變更並儲存頁面。  
  
## <a name="see-also"></a>請參閱＜  
 [將報表檢視器 Web 組件加入網頁中 &#40;SharePoint 整合模式的 Reporting Services&#41;](../../reporting-services/report-server-sharepoint/add-the-report-viewer-web-part-to-a-web-page.md)   
 [SharePoint 網站上的報表檢視器 Web 組件](../../reporting-services/report-server-sharepoint/report-viewer-web-part-on-a-sharepoint-site.md)   
 [自訂報表檢視器 Web 組件](../../reporting-services/report-server-sharepoint/customize-the-report-viewer-web-part.md)  
  
  
