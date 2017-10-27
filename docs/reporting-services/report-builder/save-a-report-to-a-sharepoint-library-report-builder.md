---
title: "將報表儲存至 SharePoint 文件庫 （報表產生器） |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4daa1eee-78b7-43d0-8b22-4a98e8fa66ba
caps.latest.revision: 10
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Inactive
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e6e87cb6c8daa8744b676d5ed78ed8339705f28e
ms.contentlocale: zh-tw
ms.lasthandoff: 08/09/2017

---
# <a name="save-a-report-to-a-sharepoint-library-report-builder"></a>將報表儲存至 SharePoint 文件庫 (報表產生器)
  若要將報表儲存至針對 SharePoint 整合所設定的報表伺服器，您必須瀏覽至 SharePoint 伺服器，然後建立報表伺服器的連接。 在報表定義中，與報表相關之項目的所有參考都必須使用 SharePoint 報表伺服器特有的值。 相關的項目包括子報表、鑽研報表和資源，例如以 Web 為基礎的影像。 如需詳細資訊，請參閱[指定外部項目的路徑 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/specifying-paths-to-external-items-report-builder-and-ssrs.md)。  
  
 您在 SharePoint 網站上必須具有「 **成員** 」或「 **擁有者** 」權限才能設定專案的屬性。  
  
### <a name="to-save-a-report-to-a-sharepoint-site"></a>若要將報表儲存至 SharePoint 網站  
  
1.  在報表產生器的按鈕中，按一下 **[儲存]**。 **存***\<報表項目 >*對話方塊隨即開啟。  
  
    > [!NOTE]  
    >  如果您重新儲存報表，報表會自動重新儲存到之前的位置。 使用 [另存新檔] 選項可變更位置。  
  
2.  您也可以選擇按一下 **[最近使用的網站和伺服器]** 來顯示最近使用過的報表伺服器和 SharePoint 網站清單。  
  
3.  瀏覽至 SharePoint 網站，然後按一下 [儲存]。  
  
    > [!NOTE]  
    >  如果您保留已變更的報表超過 10 小時而未加以儲存，此報表就會與伺服器中斷連接，但不會儲存。 如果發生這種情況，請按一下右下狀態列中的 [中斷連接]，然後按一下 [連接]。 最新的伺服器將位於可用的伺服器清單中。 選取該伺服器，然後報表將會重新連接。  
  
## <a name="see-also"></a>請參閱＜  
 [尋找、檢視和管理報表 &#40;報表產生器及 SSRS &#41;](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)  
  
  

