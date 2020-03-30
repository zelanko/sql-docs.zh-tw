---
title: 使用 Reporting Services 報表檢視器網頁組件連線篩選或文件網頁組件 | Microsoft Docs
ms.date: 11/26/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-sharepoint
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 1f513b93852863d7c3c03ac60289d4ba2bdb4b7b
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "77256709"
---
# <a name="connect-filter-or-documents-web-part-with-a-reporting-services-report-viewer-web-part"></a>使用 Reporting Services 報表檢視器網頁組件連線篩選或文件網頁組件

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)]  [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-and-later](../../includes/ssrs-appliesto-sharepoint-2013-and-later.md)] [!INCLUDE[ssrs-appliesto-not-sharepoint-online](../../includes/ssrs-appliesto-not-sharepoint-online.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

如果您使用的是 SharePoint 產品，可以建立包含篩選網頁組件或文件網頁組件以及報表檢視器網頁組件的儀表板或網頁組件頁面。 支援的版本為 [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] 或 [!INCLUDE[SPS2010](../../includes/sps2010-md.md)]。 另外也支援 [!INCLUDE[winSPServ3](../../includes/winspserv3-md.md)] 或 [!INCLUDE[offSPServ](../../includes/offspserv-md.md)] 2007。 藉由連線篩選網頁組件，使用者可以在篩選網頁組件中選取篩選值，並將值傳送到相同頁面上的參數化報表。 藉由連線文件網頁組件，使用者則可在文件庫中按一下報表，並在相鄰的報表檢視器網頁組件中檢視該報表。

> [!NOTE]
> SQL Server 2016 後即不再提供 Reporting Services 與 SharePoint 的整合。

 篩選網頁組件可用來將值傳送給報表中的一或多個參數。 若要使用篩選網頁組件，報表必須定義與網頁組件傳送之值、資料類型和格式相容的參數。  
  
 文件網頁組件與主網站的文件庫建立關聯。 若要檢視、新增或移除文件庫中的項目，請按一下 [檢視所有網站內容]  。 在 [程式庫] 中按一下 [文件]  。 您可以使用 [新增]  、[上傳]  和 [動作]  功能表來管理文件庫中的項目。  
  
## <a name="connect-a-filter-web-part"></a>連線篩選網頁組件
  
1.  開啟或建立網頁組件頁面或儀表板。  
  
2.  在 [網站動作]  功能表中，按一下 [編輯頁面]  。  
  
3.  按一下 [新增網頁組件]  。  
  
4.  在 [所有網頁組件]  的 [其他]  類別目錄中，選取 [SQL Server Reporting Services 報表檢視器]  。  
  
5.  按一下 [新增]  。 網頁組件會新增至區域頂端。  
  
6.  在相同網頁組件頁面或儀表板的另一個區域中，按一下 [新增網頁組件]  。  
  
7.  在 [所有網頁組件]  的 [篩選]  區段中，選取網頁組件。  
  
8.  按一下 [新增]  。 網頁組件會新增至區域頂端。  
  
9. 在包含網頁組件的區段中，按一下網頁組件的 [編輯]  功能表，並依序指向 [連]  和 [Send Filter Values To] \(傳送篩選值至)  ，然後選取 [報表檢視器 **報表名稱** - ]  。  
  
10. 簽入變更並儲存頁面。  
  
## <a name="connect-a-documents-web-part"></a>連線文件網頁組件  
  
1.  開啟或建立網頁組件頁面或儀表板。  
  
2.  在 [網站動作]  功能表中，按一下 [編輯頁面]  。  
  
3.  按一下 [新增網頁組件]  。  
  
4.  在 [所有網頁組件]  的 [清單和文件庫]  區段中，選取 [文件]  。  
  
5.  按一下 [新增]  。 網頁組件會新增至區域頂端。  
  
6.  按一下工具窗格底部的 [套用]  ，然後按一下 [確定]  關閉窗格。  
  
7.  在相同網頁組件頁面或儀表板的另一個區域中，按一下 [新增網頁組件]  。  
  
8.  在 [所有網頁組件]  的 [其他]  類別目錄中，選取 [SQL Server Reporting Services 報表檢視器]  。  
  
9. 按一下 [新增]  。 網頁組件會新增至區域頂端。  
  
10. 在包含網頁組件的區段中，按一下網頁組件的 [編輯]  功能表，指向 [連線]  ，再指向 [報表定義取得來源]  ，然後選取 [文件]  。  
  
11. 簽入變更並儲存頁面。  
  
## <a name="see-also"></a>另請參閱

 [將報表檢視器網頁組件新增至網頁](../../reporting-services/report-server-sharepoint/add-the-report-viewer-web-part-to-a-web-page.md)   
 [SharePoint 網站上的報表檢視器 Web 組件](../../reporting-services/report-server-sharepoint/report-viewer-web-part-on-a-sharepoint-site.md)   
 [自訂報表檢視器 Web 組件](../../reporting-services/report-server-sharepoint/customize-the-report-viewer-web-part.md)  

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](https://go.microsoft.com/fwlink/?LinkId=620231)
