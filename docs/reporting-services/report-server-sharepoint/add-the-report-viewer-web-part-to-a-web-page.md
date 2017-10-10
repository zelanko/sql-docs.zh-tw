---
title: "將報表檢視器 web 組件加入至網頁 |Microsoft 文件"
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
ms.translationtype: MT
ms.sourcegitcommit: ea362cd05de5d1ba17ca717d94354d5786119bab
ms.openlocfilehash: 26080938c9849d6021f30d970ab2262f405df00c
ms.contentlocale: zh-tw
ms.lasthandoff: 10/06/2017

---
# <a name="add-the-report-viewer-web-part-to-a-web-page"></a>將報表檢視器 web 組件加入至 web 網頁

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

您可以使用報表檢視器 web 組件來檢視，已設定的報表伺服器上執行才能在 SharePoint 整合模式的報表。 您可以使用 web 組件，以顯示您在報表產生器或報表設計師中建立並上傳至文件庫的報表定義 (.rdl) 檔案。

如果您想要將報表內嵌在該頁面上的報表，您可以加入報表檢視器 web 組件至網頁。

> [!NOTE]
> 本文是特定隨附 Reporting Services 增益集適用於 SharePoint 產品與報表檢視器 web 組件。 SQL Server 2016 之後已無法再使用 reporting Services 與 SharePoint 整合。

若要將 web 組件加入至網頁，您必須新增並自訂頁面的權限在網站層級。 如果您使用預設安全性設定，此權限授與成員的**擁有者**具有完整控制權限等級的權限的群組。

## <a name="to-embed-a-report-in-a-web-page"></a>若要在網頁中內嵌報表

1.  開啟或建立 web 組件頁面或儀表板。  
  
2.  在**網站動作**，按一下 **編輯頁面**。  
  
3.  按一下**新增網頁組件**。  
  
4.  在 web 組件類別目錄清單中，選取**其他**類別目錄，然後選取**SQL Server Reporting Services 報表檢視器**。  
  
5.  按一下 **[加入]**。 Web 組件加入區域頂端。 您可將它拖曳至該區域中的其他位置。  
  
6.  在檢視器中，按一下**按這裡開啟工具窗格**。  
  
7.  從目前的站台集合中的任何文件庫中選取報表，依序按一下瀏覽 (**...**) 按鈕。 您也可以輸入報表的 URL。 若要判斷任何報表的 URL，以滑鼠右鍵按一下報表，然後選取**屬性**。 請勿按報表旁邊的向下箭號，因為在項目的 [檢視屬性] 頁面中不會指示報表 URL。 如果您複製並貼上 URL 從**屬性**對話方塊方塊中，將"%20"URL 編碼取代空格 （例如，"Company %20sales"應該是"Company Sales"）。  
  
    > [!NOTE]  
    >  每個報表檢視器 web 組件包含單一的報表。 URL 必須是完整的路徑，指向位於目前的 SharePoint 網站，或是位於相同 Web 應用程式或伺服陣列內之網站的報表。 URL 必須解析為文件庫，或包含該報表之文件庫內的資料夾。 報表 URL 必須包括副檔名 .rdl。 如果報表是根據模型或共用資料來源檔案，則不需要在 URL 中指定這些檔案。 報表會包含所需的檔案參考。  
  
8.  在工具窗格開啟時，可以設定屬性以修改預設的外觀和配置。  
  
9. 按一下**套用**工具窗格中，然後再按一下底部**確定**關閉窗格。  
  
## <a name="see-also"></a>另請參閱

 [在 SharePoint 網站上的報表檢視器 web 組件](../../reporting-services/report-server-sharepoint/report-viewer-web-part-on-a-sharepoint-site.md)   
 [自訂報表檢視器 web 組件](../../reporting-services/report-server-sharepoint/customize-the-report-viewer-web-part.md)   
 [授與 SharePoint 網站上報表伺服器項目的權限](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)   
 [安裝或解除安裝 SharePoint 的 Reporting Services 增益集](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)  
