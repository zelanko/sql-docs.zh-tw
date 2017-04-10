---
title: "將報表或模型繫結至共用資料來源 (SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "共用資料來源 [Reporting Services]"
  - "資料來源 [Reporting Services], 共用"
ms.assetid: 23cc15f2-2883-48e2-bc6c-fa0ab61a2e21
caps.latest.revision: 11
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 11
---
# 將報表或模型繫結至共用資料來源 (SSRS)
  在某些情況下 (例如，將報表或模型從測試伺服器移到實際伺服器時)，您可能想先將檔案儲存在本機電腦，然後再上傳到不同報表伺服器。 當您將報表或模型上傳到新伺服器時，您必須將它重新繫結至新報表伺服器上儲存的共用資料來源。 如果不重新繫結報表或模型，從新報表伺服器存取該報表或模型時將無法正常運作。  
  
> [!IMPORTANT]  
>  將報表或模型重新繫結至共用資料來源時，資料來源必須已存在報表伺服器或 SharePoint 文件庫中。 如需資料來源的詳細資訊，請參閱[建立、修改和刪除共用資料來源 &#40;SSRS&#41;](../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md)。  
  
### 將報表或模型繫結至以原生模式執行之報表伺服器上的共用資料來源  
  
1.  在 **[報表管理員]**中，按一下要上傳至伺服器的報表或模型名稱。  
  
     [屬性] 索引標籤隨即開啟。  
  
2.  按一下 **[資料來源]**。  
  
3.  按一下 **[瀏覽]**，然後導覽到報表或模型要繫結的資料來源。  
  
4.  選取資料來源，然後按一下 **[確定]**。  
  
5.  按一下 **[套用]**。  
  
     現在報表或模型已繫結至所選取的資料來源。  
  
### 將報表或模型繫結至以 SharePoint 整合模式執行之報表伺服器上的共用資料來源  
  
1.  如果文件庫尚未開啟，請在 [快速啟動] 列上按一下文件庫名稱。 如果找不到您的文件庫名稱，請先按一下 **[檢視所有網站內容]**，然後再按一下文件庫名稱。  
  
2.  指向報表或模型，然後按一下向下箭頭。  
  
3.  按一下 **[管理資料來源]**。  
  
4.  按一下 **[dataSource1]**。  
  
5.  在 **[連接類型]** 區域中，確認已選取 **[共用資料來源]** 。  
  
6.  在 [資料來源連結] 區域中，按一下省略符號 (...) 按鈕。  
  
7.  找到要使用的資料來源。  
  
8.  選取資料來源，然後按一下 **[確定]**。  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
10. 按一下 [ **關閉**]。  
  
## 請參閱＜  
 [上傳檔案或報表 &#40;報表管理員&#41;](../../reporting-services/reports/upload-a-file-or-report-report-manager.md)   
 [將文件上傳到 SharePoint 文件庫 &#40;SharePoint 模式的 Reporting Services&#41;](../../reporting-services/report-server-sharepoint/upload-documents-to-a-sharepoint-library-reporting-services-in-sharepoint-mode.md)   
 [建立和管理共用資料來源 &#40;SharePoint 整合模式的 Reporting Services&#41;](../Topic/Create%20and%20Manage%20Shared%20Data%20Sources%20\(Reporting%20Services%20in%20SharePoint%20Integrated%20Mode\).md)   
 [建立、刪除或修改共用資料來源 &#40;報表管理員&#41;](../Topic/Create,%20Delete,%20or%20Modify%20a%20Shared%20Data%20Source%20\(Report%20Manager\).md)   
 [資料連接、資料來源及連接字串 &#40;報表產生器和 SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)   
 [Reporting Services 支援的資料來源 &#40;SSRS&#41;](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)  
  
  