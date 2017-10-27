---
title: "連接篩選或文件 web 組件與 Reporting Services 報表檢視器 web 組件 |Microsoft 文件"
ms.custom: 
ms.date: 10/05/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: ea362cd05de5d1ba17ca717d94354d5786119bab
ms.openlocfilehash: 87d4b4a3f0c01804329f3a7b0688632c20ed6c9b
ms.contentlocale: zh-tw
ms.lasthandoff: 10/06/2017

---
# <a name="connect-filter-or-documents-web-part-with-a-reporting-services-report-viewer-web-part"></a>連接篩選或文件 web 組件與 Reporting Services 報表檢視器 web 組件

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

如果您使用 SharePoint 產品，您可以建立儀表板或網頁組件包含篩選網頁組件或文件 web 組件以及報表檢視器 web 組件的頁面。 支援的版本為 [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] 或 [!INCLUDE[SPS2010](../../includes/sps2010-md.md)]。 另外也支援 [!INCLUDE[winSPServ3](../../includes/winspserv3-md.md)] 或 [!INCLUDE[offSPServ](../../includes/offspserv-md.md)] 2007。 藉由連接篩選網頁組件，在篩選 web 組件中選取篩選值的使用者可以將值傳送至相同的頁面上的參數化報表。 藉由連接文件 web 組件，按一下 文件庫中的報表的使用者可以檢視報表，相鄰的報表檢視器 web 組件中。

> [!NOTE]
> SQL Server 2016 之後已無法再使用 reporting Services 與 SharePoint 整合。

 篩選網頁組件用來將值傳送到報表上的一個或多個參數。 若要使用篩選網頁組件，報表必須為它定義的參數值、 資料類型和 web 組件所傳送的格式與相容。  
  
 文件 web 組件都與主網站的文件庫。 若要檢視，新增，或移除文件庫中的項目，請按一下**檢視所有網站內容**。 在程式庫，按一下 **文件**。 您可以使用**新增**，**上傳**，和**動作**功能表來管理文件庫中的項目。  
  
## <a name="connect-a-filter-web-part"></a>連接篩選網頁組件
  
1.  開啟或建立 web 組件頁面或儀表板。  
  
2.  在**網站動作**功能表上，按一下 **編輯頁面**。  
  
3.  按一下**新增網頁組件**。  
  
4.  在**所有網頁組件**，請在**其他**類別目錄中，選取**SQL Server Reporting Services 報表檢視器**。  
  
5.  按一下 **[加入]**。 Web 組件加入區域頂端。  
  
6.  在相同的 web 組件頁面或儀表板中的另一個區域，按一下 **新增網頁組件**。  
  
7.  在**所有網頁組件**，請在**篩選**區段中，選取網頁組件。  
  
8.  按一下 **[加入]**。 Web 組件加入區域頂端。  
  
9. 在包含網頁組件區域中，按一下 web 組件**編輯**功能表上，指向**連線**，指向 **傳送篩選值至**，然後選取**報表檢視器** - *報表名稱*。  
  
10. 簽入變更並儲存頁面。  
  
## <a name="connect-a-documents-web-part"></a>文件 web 組件連接  
  
1.  開啟或建立 web 組件頁面或儀表板。  
  
2.  在**網站動作**功能表上，按一下 **編輯頁面**。  
  
3.  按一下**新增網頁組件**。  
  
4.  在**所有網頁組件**，請在**清單和程式庫**區段中，選取**文件。**  
  
5.  按一下 **[加入]**。 Web 組件加入區域頂端。  
  
6.  按一下**套用**工具窗格中，然後再按一下底部**確定**關閉窗格。  
  
7.  在相同的 web 組件頁面或儀表板中的另一個區域，按一下 **新增網頁組件**。  
  
8.  在**所有網頁組件**，請在**其他**類別目錄中，選取**SQL Server Reporting Services 報表檢視器。**  
  
9. 按一下 **[加入]**。 Web 組件加入區域頂端。  
  
10. 在包含網頁組件區域中，按一下 web 組件**編輯**功能表上，指向**連線**，指向 **報表定義取得來源**，然後選取**文件**。  
  
11. 簽入變更並儲存頁面。  
  
## <a name="see-also"></a>另請參閱

 [將報表檢視器 web 組件加入至 web 網頁](../../reporting-services/report-server-sharepoint/add-the-report-viewer-web-part-to-a-web-page.md)   
 [在 SharePoint 網站上的報表檢視器 web 組件](../../reporting-services/report-server-sharepoint/report-viewer-web-part-on-a-sharepoint-site.md)   
 [自訂報表檢視器 Web 組件](../../reporting-services/report-server-sharepoint/customize-the-report-viewer-web-part.md)  

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](http://go.microsoft.com/fwlink/?LinkId=620231)

