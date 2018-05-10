---
title: 將報表檢視器網頁組件新增至網頁 | Microsoft Docs
ms.custom: ''
ms.date: 10/05/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-server-sharepoint
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 5d9eb107d1355a15d15c22fc3b24824cae009075
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="add-the-report-viewer-web-part-to-a-web-page"></a>將報表檢視器網頁組件新增至網頁

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

您可以使用報表檢視器網頁組件來檢視在設定為以 SharePoint 整合模式執行之報表伺服器上執行的報表。 您可以使用網頁組件顯示在報表產生器或報表設計師中建立，並且上傳至文件庫的報表定義 (.rdl) 檔案。

如果您要在網頁上內嵌報表，您可以將報表檢視器網頁組件新增至該網頁中。

> [!NOTE]
> 本文專門針對適用於 SharePoint 產品的 Reporting Services 增益集的隨附報表檢視器網頁組件。 SQL Server 2016 後即不再提供 Reporting Services 與 SharePoint 的整合。

若要將網頁組件新增至網頁，您必須在網站層級，擁有「新增並自訂頁面」權限。 如果您要使用預設的安全性設定，此權限會授與具備「完整控制」等級之權限的**擁有者**群組成員。

## <a name="to-embed-a-report-in-a-web-page"></a>在網頁中內嵌報表

1.  開啟或建立網頁組件頁面或儀表板。  
  
2.  在 [網站動作] 中，按一下 [編輯頁面]。  
  
3.  按一下 [新增網頁組件]。  
  
4.  在網頁組件類別目錄的清單中，選取 [其他] 類別目錄，然後選取 [SQL Server Reporting Services 報表檢視器]。  
  
5.  按一下 **[加入]**。 網頁組件會新增至區域頂端。 您可將它拖曳至該區域中的其他位置。  
  
6.  在檢視器中，按一下 [請按這裡開啟工具窗格]。  
  
7.  按一下瀏覽 ([...]) 按鈕，選取目前網站集合中任意文件庫的報表。 您也可以輸入報表的 URL。 若要判斷任何報表的 URL，請以滑鼠右鍵按一下報表，然後選取 [屬性]。 請勿按報表旁邊的向下箭號，因為在項目的 [檢視屬性] 頁面中不會指示報表 URL。 如果您從 [屬性] 對話方塊複製並貼上 URL，請將 "%20" URL 編碼取代為空格 (例如，"Company%20Sales" 應該是 "Company Sales")。  
  
    > [!NOTE]  
    >  每一個報表檢視器的網頁組件都包含單一報表。 URL 必須是完整的路徑，指向位於目前的 SharePoint 網站，或是位於相同 Web 應用程式或伺服陣列內之網站的報表。 URL 必須解析為文件庫，或包含該報表之文件庫內的資料夾。 報表 URL 必須包括副檔名 .rdl。 如果報表是根據模型或共用資料來源檔案，則不需要在 URL 中指定這些檔案。 報表會包含所需的檔案參考。  
  
8.  在工具窗格開啟時，可以設定屬性以修改預設的外觀和配置。  
  
9. 按一下工具窗格底部的 [套用]，然後按一下 [確定] 關閉窗格。  
  
## <a name="see-also"></a>另請參閱

 [SharePoint 網站上的報表檢視器 Web 組件](../../reporting-services/report-server-sharepoint/report-viewer-web-part-on-a-sharepoint-site.md)   
 [自訂報表檢視器網頁組件](../../reporting-services/report-server-sharepoint/customize-the-report-viewer-web-part.md)   
 [授與 SharePoint 網站上報表伺服器項目的權限](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)   
 [安裝或解除安裝 SharePoint 的 Reporting Services 增益集](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)  
