---
title: 將報表繫結至共用資料來源 (SSRS) | Microsoft Docs
ms.date: 05/24/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
helpviewer_keywords:
- shared data sources [Reporting Services]
- data sources [Reporting Services], shared
ms.assetid: 23cc15f2-2883-48e2-bc6c-fa0ab61a2e21
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 9e41ac864403dce2cad648790099496b53c4b6dc
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "74190900"
---
# <a name="bind-a-report-to-a-shared-data-source-ssrs"></a>將報表繫結至共用資料來源 (SSRS)
  在某些情況下 (例如，將報表從測試伺服器移到生產環境伺服器時)，您可能想先將檔案儲存在本機電腦，然後再上傳到不同的報表伺服器。 當您將報表上傳到新伺服器時，您必須將它重新繫結至新報表伺服器上儲存的共用資料來源。 如果不重新繫結報表，從新報表伺服器存取該報表時將無法正常運作。  
  
> [!IMPORTANT]  
>  將報表重新繫結至共用資料來源時，資料來源必須已存在報表伺服器或 SharePoint 文件庫中。 如需資料來源的詳細資訊，請參閱[建立、修改和刪除共用資料來源 &#40;SSRS&#41;](../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md)。  
  
## <a name="to-bind-a-report-to-a-shared-data-source-on-a-report-server-running-in-native-mode"></a>將報表繫結至以原生模式執行之報表伺服器上的共用資料來源  
  
1.  在入口網站中，按一下報表磚右上角的省略符號 (...) > [管理]  。  

2.  按一下 **[資料來源]** 。  
  
3.  按一下 [共用資料來源]  ，然後巡覽至報表要繫結的資料來源。  
  
4.  選取資料來源，然後按一下 [儲存]  。  
  
5.  按一下 [套用]  。  
  
     現在報表已繫結至所選取的資料來源。  
  
## <a name="to-bind-a-report-to-a-shared-data-source-on-a-report-server-running-in-sharepoint-integrated-mode"></a>將報表繫結至以 SharePoint 整合模式執行之報表伺服器上的共用資料來源  
  
1.  如果文件庫尚未開啟，請在 [快速啟動] 列上按一下文件庫名稱。 如果找不到您的文件庫名稱，請先按一下 **[檢視所有網站內容]** ，然後再按一下文件庫名稱。  
  
2.  指向報表，然後按一下向下箭號。  
  
3.  按一下 **[管理資料來源]** 。  
  
4.  按一下 **[dataSource1]** 。  
  
5.  在 **[連接類型]** 區域中，確認已選取 **[共用資料來源]** 。  
  
6.  在 [資料來源連結]  區域中，按一下省略符號 (...) 按鈕。  
  
7.  找到要使用的資料來源。  
  
8.  選取資料來源，然後按一下 **[確定]** 。  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
10. 按一下 [關閉]  。  
  
## <a name="see-also"></a>另請參閱  
 [將文件上傳到 SharePoint 文件庫 &#40;SharePoint 模式的 Reporting Services&#41;](../../reporting-services/report-server-sharepoint/upload-documents-to-a-sharepoint-library-reporting-services-in-sharepoint-mode.md)   
 [建立和管理共用資料來源 &#40;SharePoint 整合模式的 Reporting Services&#41;](https://msdn.microsoft.com/library/2d3428e4-a810-4e66-a287-ff18e57fad76)   
 [建立資料連接字串 - 報表產生器 & SSRS](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)   
 [Reporting Services 支援的資料來源 &#40;SSRS&#41;](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)  
  
  
