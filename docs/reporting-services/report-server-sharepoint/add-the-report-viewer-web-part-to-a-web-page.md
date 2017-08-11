---
title: "將報表檢視器 Web 組件加入至網頁 |Microsoft 文件"
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
- SharePoint integration [Reporting Services], viewing reports
- Web Parts [Reporting Services]
- SharePoint integration [Reporting Services], Web Parts
- Report Viewer Web Part [Reporting Services]
ms.assetid: cac75345-2380-467d-a394-0a2140908a5a
caps.latest.revision: 13
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 0fd8adf79a7eeccb66b5efd6fc90e1312020973a
ms.contentlocale: zh-tw
ms.lasthandoff: 08/09/2017

---
# <a name="add-the-report-viewer-web-part-to-a-web-page"></a>將報表檢視器 Web 組件加入至網頁
  您可以使用報表檢視器 Web 組件來檢視在設定為以 SharePoint 整合模式執行之報表伺服器上執行的報表。 您可以使用 Web 組件顯示在報表產生器或報表設計師中建立，並且上傳至文件庫的報表定義 (.rdl) 檔案。  
  
 如果您要在網頁上內嵌報表，您可以將報表檢視器 Web 組件加入至該網頁中。  
  
> [!NOTE]  
>  雖然它們有相同的名稱，但是透過 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 增益集安裝的報表檢視器 Web 組件，與包含在 RSWebParts.cab 檔案中的報表檢視器 Web 組件不同。 本主題中的指示是特別針對透過 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 增益集安裝的報表檢視器 Web 組件。  
  
 若要將 Web 組件加入至網頁中，您必須在網站層級，擁有「新增並自訂頁面」權限。 如果您使用預設安全性設定，此權限授與成員的**擁有者**具有完整控制權限等級的權限的群組。  
  
### <a name="to-embed-a-report-in-a-web-page"></a>在網頁中內嵌報表  
  
1.  開啟或建立網頁組件頁面或儀表板。  
  
2.  在**網站動作**，按一下 **編輯頁面**。  
  
3.  按一下 [加入網頁組件]。  
  
4.  在 web 組件類別目錄清單中，選取**其他**類別目錄，然後選取**SQL Server Reporting Services 報表檢視器**。  
  
5.  按一下 **[加入]**。 Web 組件會加入區域頂端。 您可將它拖曳至該區域中的其他位置。  
  
6.  在檢視器中，按一下**按這裡開啟工具窗格**。  
  
7.  從目前的站台集合中的任何文件庫中選取報表，依序按一下瀏覽 (**...**) 按鈕。 您也可以輸入報表的 URL。 若要判斷任何報表的 URL，以滑鼠右鍵按一下報表，然後選取**屬性**。 請勿按報表旁邊的向下箭號，因為在項目的 [檢視屬性] 頁面中不會指示報表 URL。 如果您複製並貼上 URL 從**屬性**對話方塊方塊中，將"%20"URL 編碼取代空格 （例如，"Company %20sales"應該是"Company Sales"）。  
  
    > [!NOTE]  
    >  每一個報表檢視器 Web 組件都包含單一報表。 URL 必須是完整的路徑，指向位於目前的 SharePoint 網站，或是位於相同 Web 應用程式或伺服陣列內之網站的報表。 URL 必須解析為文件庫，或包含該報表之文件庫內的資料夾。 報表 URL 必須包括副檔名 .rdl。 如果報表是根據模型或共用資料來源檔案，則不需要在 URL 中指定這些檔案。 報表會包含所需的檔案參考。  
  
8.  在工具窗格開啟時，可以設定屬性以修改預設的外觀和配置。  
  
9. 按一下工具窗格底部的 [套用]，然後按一下 [確定] 關閉窗格。  
  
## <a name="see-also"></a>另請參閱  
 [SharePoint 網站上的報表檢視器 Web 組件](../../reporting-services/report-server-sharepoint/report-viewer-web-part-on-a-sharepoint-site.md)   
 [自訂報表檢視器 Web 組件](../../reporting-services/report-server-sharepoint/customize-the-report-viewer-web-part.md)   
 [授與權限在 SharePoint 網站上的報表伺服器項目](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)   
 [安裝或解除安裝 SharePoint 的 Reporting Services 增益集](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)  
  
  
