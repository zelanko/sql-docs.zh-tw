---
title: "加入分頁符號 （報表產生器及 SSRS） |Microsoft 文件"
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
ms.assetid: 3846cd48-2787-47e9-b13b-7fc45a205f68
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 81f305fdb34231a14c53d376ed9c4535ce6b9f53
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="add-a-page-break-report-builder-and-ssrs"></a>加入分頁符號 (報表產生器及 SSRS)
  您可以在資料區內的矩形、資料區或群組中加入分頁符號，以控制每頁的資料量。 加入分頁符號可以改善已發行報表的效能，因為在檢視報表時，只有每個頁面上的項目需要進行處理。 當整個報表只有單一頁面時，必須先將所有的項目進行處理，才能檢視報表。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-page-break-to-a-data-region"></a>將分頁符號加入至資料區域  
  
1.  在設計介面上，以滑鼠右鍵按一下資料區域的角控點，然後按一下 [Tablix 屬性]。  
  
2.  在 **[一般]** 索引標籤的 **[分頁符號選項]**下方，選取下列其中一個選項：  
  
    -   **在前方加入分頁符號**— 如果要在資料表之前加入分頁符號，請選取此選項。  
  
    -   **在後方加入分頁符號**— 如果要在資料表之後加入分頁符號，請選取此選項。  
  
    -   **盡可能將資料表納入一個頁面**— 如果要將資料放入單一頁面，請選取此選項。  
  
### <a name="to-add-a-page-break-to-a-rectangle"></a>將分頁符號加入至矩形  
  
1.  在設計介面上，以滑鼠右鍵按一下要加入分頁符號的矩形，然後按一下 [矩形屬性]。  
  
2.  在 **[一般]** 索引標籤的 **[分頁符號選項]**下方，選取下列其中一個選項：  
  
    -   **在前方加入分頁符號**— 如果要在矩形之前加入分頁符號，請選取此選項。  
  
    -   **在後方加入分頁符號**— 如果要在矩形之後加入分頁符號，請選取此選項。  
  
    -   **省略分頁符號上的框線**— 如果不要顯示分頁符號上的框線，請選取此選項。  
  
    -   **盡可能將內容保持在一頁**— 如果要將矩形內部的內容放入單一頁面，請選取此選項。  
  
### <a name="to-add-a-page-break-to-a-row-group-in-a-table-matrix-or-list"></a>若要將分頁符號加入至資料表、矩陣或清單中的資料列群組  
  
1.  在 [群組] 窗格中，以滑鼠右鍵按一下資料列群組，然後按一下 [群組屬性]。  
  
    > [!NOTE]  
    >  系統就會忽略資料行群組上的分頁符號。  
  
2.  在 **[分頁符號]** 索引標籤上，選取 **[在群組的每個執行個體之間]** ，以在資料表中的每個群組執行個體之間加入分頁符號。  
  
3.  或者，也可以選取 **[也在群組的開頭]** 或 **[也在群組的結尾]** ，指定在資料表中的群組開頭或結尾處加入分頁符號。  
  
## <a name="see-also"></a>請參閱＜  
 [Reporting Services 中的分頁 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [轉譯行為 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)   
 [頁首和頁尾 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/page-headers-and-footers-report-builder-and-ssrs.md)  
  
  
