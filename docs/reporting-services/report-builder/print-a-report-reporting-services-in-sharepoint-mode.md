---
title: "列印報表 (Reporting Services SharePoint 模式) |Microsoft 文件"
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
helpviewer_keywords:
- printing reports, SharePoint Web application
- printing reports
ms.assetid: 026784f7-8cb4-4351-93ee-230b2ab0f8f5
caps.latest.revision: 11
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: f89c8f0d330561aacd678e4556fdaf2910b5dcc7
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="print-a-report-reporting-services-in-sharepoint-mode"></a>列印報表 (SharePoint 模式的 Reporting Services)
  當報表伺服器以 SharePoint 模式執行時，您可以使用下列三種方法從 SharePoint Web 應用程式列印報表：  
  
-   **從 SharePoint 網站** ：請從 **[動作]** 功能表 (開啟報表後，此功能表便會出現在報表工具列中) 選取 **[列印]** 。 這個動作可提供 Reporting Services 列印功能，包括用來選取印表機、指定頁數和邊界及預覽報表的標準 **[列印]** 對話方塊。 這項列印功能是要用來取代瀏覽器 [檔案] 功能表上的 [列印] 命令。 使用這種方法列印報表時，報表會像原來設計那樣列印出來，而不會有您在網頁輸出中所看到的多餘元素。  
  
-   **從瀏覽器** ：瀏覽器的列印功能最適合用來列印單頁的 HTML 報表。 通常，您從瀏覽器列印的頁面會包括網頁上的所有視覺化元素，以及識別網頁或網站的頁首和頁尾資訊。 當您從瀏覽器列印時，只會列印目前視窗的內容。 如果報表很長，瀏覽器只會列印報表的一部分 (通常是第一頁)。  
  
-   **從目標應用程式** ：您可以匯出報表，以使用目標應用程式 (例如 Microsoft Office Excel 或 Adobe Acrobat Reader) 的列印功能。 某些應用程式格式，例如 TIFF 或 PDF，非常適合用來列印多頁報表。 將報表匯出到桌面應用程式後，您就可以使用應用程式提供的所有專業列印功能。 若要匯出報表，請從 **[動作]** 功能表 (開啟報表後，此功能表便會出現在報表工具列中) 選擇 **[匯出]** 。  
  
> [!NOTE]  
>  若要列印報表，您必須擁有檢視報表的權限。  
  
 從網頁列印報表時，為求最佳效果，請使用 **[動作]** 功能表上的 **[列印]** 選項。 **[列印]** 動作是由下載自報表伺服器的用戶端列印控制項提供。 您只需下載此控制項一次；系統會在您第一次選取 **[列印]**時進行下載。  
  
 報表作者可以特別針對列印輸出或特定應用程式格式來設計報表。 由於不同應用程式格式實作的分頁方式有所不同，您可能無法使每一份報表的每一種匯出格式達到最佳列印輸出結果。 相對於針對列印輸出所設計的報表，畫面上的報表頁面是為了容納不同資料量而設計的。 例如，根據您擴充資料列和資料行的方式而定，包括矩陣的報表可能會造成頁面的水平與垂直成長。 列印大小變動的報表時，未展開矩陣的使用者與將矩陣展開的使用者將會得到不同的列印結果。 就大部分的匯出報表而言，報表列印輸出會包括報表上顯示的所有內容，如使用者在電腦螢幕上看到的一樣。  
  
### <a name="how-to-print-reports-from-the-actions-menu"></a>如何從動作功能表列印報表  
  
1.  開啟報表。  
  
2.  在 **[動作]** 功能表上，按一下 **[列印]**。 如果沒有看到 **[動作]** 功能表，表示系統已隱藏報表工具列，而且您不能使用工具列提供的功能。 如果有 **[動作]** 功能表，但功能表上沒有 **[列印]** 選項，則表示報表伺服器已經停用列印功能，而無法使用此功能。  
  
3.  在 **[列印]** 對話方塊中，選取您要使用的印表機和設定，然後按一下 **[確定]**。  
  
     若要修改預設值，請按一下 **[內容]** 按鈕。 頁面大小會由報表定義中所定義之報表頁面大小的預設高度和寬度來決定。 您可以變更頁面維度的範圍會根據所使用的印表機功能而定。  
  
     若要在列印之前檢視報表，請按一下 **[預覽]** 按鈕。 這樣就會在個別的預覽視窗中開啟報表的第一頁。 其他的頁面在報表於報表伺服器上完成轉譯之後即可使用。 預覽的報表會轉譯成 EMF 格式。 您可以導覽至上一頁或下一頁，直到出現最後一頁為止，此時 **[下一頁]** 按鈕就會停用。 若要在預覽頁面中修改列印邊界，請按一下 **[邊界]** 按鈕。 **[邊界]** 對話方塊隨即出現。 請設定您上、下、左、右邊界，然後按一下 **[確定]**。 對話方塊會關閉並儲存設定，以供轉譯預覽和列印使用。  
  
## <a name="see-also"></a>請參閱＜  
 [啟用和停用 Reporting Services 的用戶端列印功能](../../reporting-services/report-server/enable-and-disable-client-side-printing-for-reporting-services.md)  
  
  
