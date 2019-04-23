---
title: 將報表檢視器 Web 組件新增至網頁 (SharePoint 整合模式的 Reporting Services) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- SharePoint integration [Reporting Services], viewing reports
- Web Parts [Reporting Services]
- SharePoint integration [Reporting Services], Web Parts
- Report Viewer Web Part [Reporting Services]
ms.assetid: cac75345-2380-467d-a394-0a2140908a5a
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 566ae0a91dd36d71ab6690e8910f1dd1cfe50043
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/22/2019
ms.locfileid: "59963494"
---
# <a name="add-the-report-viewer-web-part-to-a-web-page-reporting-services-in-sharepoint-integrated-mode"></a>將報表檢視器 Web 組件加入至網頁 (SharePoint 整合模式的 Reporting Services)
  您可以使用報表檢視器 Web 組件來檢視在設定為以 SharePoint 整合模式執行之報表伺服器上執行的報表。 您可以使用 Web 組件顯示在報表產生器或報表設計師中建立，並且上傳至文件庫的報表定義 (.rdl) 檔案。  
  
 如果您要在網頁上內嵌報表，您可以將報表檢視器 Web 組件加入至該網頁中。  
  
> [!NOTE]  
>  雖然它們有相同的名稱，但是透過 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 增益集安裝的報表檢視器 Web 組件，與包含在 RSWebParts.cab 檔案中的報表檢視器 Web 組件不同。 本主題中的指示是特別針對透過 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 增益集安裝的報表檢視器 Web 組件。  
  
 若要將 Web 組件加入至網頁中，您必須在網站層級，擁有「新增並自訂頁面」權限。 如果您要使用預設的安全性設定，此權限會授與具備「完整控制」等級之權限的**擁有者**群組成員。  
  
### <a name="to-embed-a-report-in-a-web-page"></a>在網頁中內嵌報表  
  
1.  開啟或建立網頁組件頁面或儀表板。  
  
2.  在 [網站動作] 中，按一下 [編輯頁面]。  
  
3.  按一下 **新增網頁組件**。  
  
4.  在網頁組件類別目錄的清單中，選取 [其他] 類別目錄，然後選取 [SQL Server Reporting Services 報表檢視器]。  
  
5.  按一下 **[加入]**。 Web 組件會加入區域頂端。 您可將它拖曳至該區域中的其他位置。  
  
6.  在檢視器中，按一下 [請按這裡開啟工具窗格]。  
  
7.  按一下瀏覽 ([...]) 按鈕，選取目前網站集合中任意文件庫的報表。 您也可以輸入報表的 URL。 若要判斷任何報表的 URL，請以滑鼠右鍵按一下報表，然後選取 [屬性]。 請勿按報表旁邊的向下箭號，因為在項目的 [檢視屬性] 頁面中不會指示報表 URL。 如果您從 [屬性] 對話方塊複製並貼上 URL，請將 "%20" URL 編碼取代為空格 (例如，"Company%20Sales" 應該是 "Company Sales")。  
  
    > [!NOTE]  
    >  每一個報表檢視器 Web 組件都包含單一報表。 URL 必須是完整的路徑，指向位於目前的 SharePoint 網站，或是位於相同 Web 應用程式或伺服陣列內之網站的報表。 URL 必須解析為文件庫，或包含該報表之文件庫內的資料夾。 報表 URL 必須包括副檔名 .rdl。 如果報表是根據模型或共用資料來源檔案，則不需要在 URL 中指定這些檔案。 報表會包含所需的檔案參考。  
  
8.  在工具窗格開啟時，可以設定屬性以修改預設的外觀和配置。  
  
9. 按一下工具窗格底部的 [套用]，然後按一下 [確定] 關閉窗格。  
  
## <a name="see-also"></a>另請參閱  
 [SharePoint 網站上的報表檢視器 Web 組件](../report-viewer-web-part-on-a-sharepoint-site.md)   
 [自訂報表檢視器 Web 組件](../customize-the-report-viewer-web-part.md)   
 [授與 SharePoint 網站上報表伺服器項目的權限](../security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)   
 [安裝或解除安裝 Reporting Services 增益集，適用於 SharePoint &#40;SharePoint 2010 和 SharePoint 2013&#41;](../install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)  
  
  
