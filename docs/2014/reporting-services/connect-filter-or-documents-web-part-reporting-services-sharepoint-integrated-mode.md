---
title: 連接篩選或檔網頁元件（SharePoint 整合模式中的 Reporting Services） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Filter Web Part [Reporting Services]
- SharePoint integration [Reporting Services], Web Parts
- Report Viewer Web Part [Reporting Services]
- Documents Web Part [Reporting Services]
ms.assetid: 6a303135-c0ef-44cd-a423-1cea8df3dcf3
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 062733f1ee68cd90ccc1b9a15d0cadc06b7e6f89
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66109720"
---
# <a name="connect-filter-or-documents-web-part-reporting-services-in-sharepoint-integrated-mode"></a>連接篩選或文件網頁組件 (SharePoint 整合模式的 Reporting Services)
  如果您使用的是 SharePoint 產品，可以建立包含篩選網頁組件或文件網頁組件以及報表檢視器網頁組件的儀表板或網頁組件頁面。 支援的版本為 [!INCLUDE[SPF2010](../includes/spf2010-md.md)] 或 [!INCLUDE[SPS2010](../includes/sps2010-md.md)]。 另外也支援 [!INCLUDE[winSPServ3](../includes/winspserv3-md.md)] 或 [!INCLUDE[offSPServ](../includes/offspserv-md.md)] 2007。 藉由連接篩選網頁組件，使用者可以在篩選網頁組件中選取篩選值，並將值傳送到相同頁面上的參數化報表； 藉由連接文件網頁組件，使用者則可在文件庫中按一下報表，並在相鄰的報表檢視器網頁組件中檢視該報表。  
  
 篩選網頁組件可用來將值傳送給報表中的一個或多個參數。 若要使用篩選網頁組件，報表必須定義與網頁組件傳送之值、資料類型和格式相容的參數。  
  
 文件網頁組件與主網站的文件庫相關聯。 若要檢視、新增或移除文件庫中的項目，請按一下 [檢視所有網站內容]****。 在 [程式庫] 中按一下 [文件]****。 您可以使用 [新增]****、[上傳]**** 和 [動作]**** 功能表來管理文件庫中的項目。  
  
### <a name="to-connect-a-filter-web-part"></a>連接篩選網頁組件  
  
1.  開啟或建立網頁組件頁面或儀表板。  
  
2.  在 [網站動作]**** 功能表中，按一下 [編輯頁面]****。  
  
3.  按一下 [**新增網頁元件**]。  
  
4.  在 [**所有 Web 組件**的 [**其他**] 分類中，選取 [ **SQL Server Reporting Services 報表檢視器]**。  
  
5.  按一下 **[新增]** 。 Web 組件會加入區域頂端。  
  
6.  在相同網頁元件頁面或儀表板的另一個區域中，按一下 [**新增網頁元件**]。  
  
7.  在 [**所有 Web 組件**的 [**篩選器**] 區段中，選取 [Web 元件]。  
  
8.  按一下 **[新增]** 。 Web 組件會加入區域頂端。  
  
9. 在包含網頁元件的區域中，按一下 [網頁元件] [**編輯**] 功能表，指向 [**連接**]，再指向 [**傳送篩選值至**]，然後選取 [**報表檢視器** - *報表名稱*]。  
  
10. 簽入變更並儲存頁面。  
  
### <a name="to-connect-a-documents-web-part"></a>連接文件網頁組件  
  
1.  開啟或建立網頁組件頁面或儀表板。  
  
2.  在 [網站動作]**** 功能表中，按一下 [編輯頁面]****。  
  
3.  按一下 [**新增網頁元件**]。  
  
4.  在 [**所有 Web 組件**的 [**清單和程式庫**] 區段中，選取 [**檔]。**  
  
5.  按一下 **[新增]** 。 Web 組件會加入區域頂端。  
  
6.  按一下工具窗格底部的 [套用]****，然後按一下 [確定]**** 關閉窗格。  
  
7.  在相同網頁元件頁面或儀表板的另一個區域中，按一下 [**新增網頁元件**]。  
  
8.  在 [**所有 Web 組件**的 [**其他**] 分類中，選取 [ **SQL Server Reporting Services 報表檢視器]。**  
  
9. 按一下 **[新增]** 。 Web 組件會加入區域頂端。  
  
10. 在包含網頁元件的區域中，按一下 [網頁元件] [**編輯**] 功能表，指向 [**連接**]，指向 [**取得報表定義來源**]，然後選取 [**檔**]。  
  
11. 簽入變更並儲存頁面。  
  
## <a name="see-also"></a>另請參閱  
 [將報表檢視器 Web 元件加入至 SharePoint 整合模式中的網頁 &#40;Reporting Services&#41;](report-server-sharepoint/add-reporting-services-content-types-to-a-sharepoint-library.md)   
 [SharePoint 網站上的報表檢視器 Web 元件](../../2014/reporting-services/report-viewer-web-part-on-a-sharepoint-site.md)   
 [自訂報表檢視器 Web 組件](../../2014/reporting-services/customize-the-report-viewer-web-part.md)  
  
  
