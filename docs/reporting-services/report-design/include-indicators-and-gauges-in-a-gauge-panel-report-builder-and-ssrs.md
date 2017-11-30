---
title: "在量測計面板中加入指標與量測計 (報表產生器及 SSRS) | Microsoft Docs"
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
ms.assetid: 4dff9b67-b483-4c51-a822-6dbe706a6840
caps.latest.revision: "8"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 4597b87876b52b41810f62423a59fef7b45394b8
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="include-indicators-and-gauges-in-a-gauge-panel-report-builder-and-ssrs"></a>在量測計面板中加入指標與量測計 (報表產生器及 SSRS)
  量測計面板是最上層的容器，其中保存一個或多個量測計和指標。 指標可以內嵌在量測計中，或置於量測計面板旁邊。  
  
 如果指標和量測計在量測計面板中是相鄰的，而且顯示不同欄位中的資料，您可能要加入標籤，讓它清除量測計和指標所傳達的內容。  
  
 量測計和指標選項可以使用運算式來設定。 如需詳細資訊，請參閱[運算式 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-embed-an-indicator-in-a-gauge"></a>若要將指標內嵌在量測計中  
  
1.  開啟現有的報表，或建立新的報表，其中包含的資料表和矩陣含有您想要顯示的資料。   
  
2.  將資料行插入資料表或矩陣中。 如需詳細資訊，請參閱[插入或刪除資料行 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/insert-or-delete-a-column-report-builder-and-ssrs.md)。  
  
3.  在 [插入] 索引標籤的 [資料區] 群組中，按一下 [量測計]，然後按一下新資料行中的資料格。 **[選取量測計類型]** 對話方塊隨即出現。  
  
4.  按一下 [星形]。 這樣會選取第一個星形量測計。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
6.  按一下量測計。 [量測計資料] 窗格隨即開啟。  
  
7.  在 [值] 區域的 [(未指定)] 清單方塊中，按一下您希望其值顯示在量測計中的欄位。 或者，從報表資料集拖曳要使用的欄位。  
  
8.  以滑鼠右鍵按一下量測計，按一下 [新增指標]，然後按一下 [子系]。 [選取指標樣式] 對話方塊隨即開啟。  
  
9. 在左窗格的 [選取指標樣式] 對話方塊中，按一下您想要的指標類型，然後按一下指標集合。  
  
10. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
11. 按一下指標。 [量測計資料] 窗格隨即開啟。  
  
12. 在 [值] 區域的 [(未指定)] 清單方塊中，按一下您希望其值顯示為指標的欄位。 或者，從報表資料集拖曳要使用的欄位。  
  
     此欄位可以與您在量測計中使用的欄位相同或相異。  
  
13. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-show-an-indicator-and-gauge-side-by-side"></a>若要並排顯示指標及量測計  
  
1.  開啟現有的報表，或建立新的報表，其中包含的資料表和矩陣含有您想要顯示的資料。  
  
2.  將資料行插入資料表或矩陣中。 如需詳細資訊，請參閱[插入或刪除資料行 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/insert-or-delete-a-column-report-builder-and-ssrs.md)。  
  
3.  在 [插入] 索引標籤的 [資料區] 群組中，按一下 [量測計]，然後按一下您插入之資料行中的資料格。 [選取量測計類型] 對話方塊隨即出現。  
  
4.  按一下 [星形]。 這樣會選取第一個星形量測計。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
6.  按一下量測計。 [量測計資料] 窗格隨即開啟。  
  
7.  在 [值] 區域的 [(未指定)] 清單方塊中，按一下您希望其值顯示在量測計中的欄位。 或者，從報表資料集拖曳要使用的欄位。  
  
8.  以滑鼠右鍵按一下量測計，按一下 [新增指標]，然後按一下 [相鄰]。 [選取指標樣式] 對話方塊隨即開啟。  
  
9. 在左窗格的 [選取指標樣式] 對話方塊中，按一下您想要的指標類型，然後按一下指標集合。  
  
10. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
11. 按一下指標。 [量測計資料] 窗格隨即開啟。  
  
12. 在 [值] 區域的 [(未指定)] 清單方塊中，按一下您希望其值顯示為指標的欄位。 或者，從報表資料集拖曳要使用的欄位。  
  
     此欄位可以與您在量測計中使用的欄位相同或相異。  
  
13. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
14. 以滑鼠右鍵按一下量測計面板，然後按一下 [新增標籤]。 標籤就會加入至量測計面板。 再重複一次。  
  
     量測計面板有兩個標籤。  
  
15. 將每個標籤拖曳到量測計或指標附近的位置。  
  
16. 以滑鼠右鍵按一下量測計附近的標籤，按一下 [標籤屬性]，然後在 [文字] 方塊中鍵入您想要的文字。  
  
17. 以滑鼠右鍵按一下指標附近的標籤，按一下 [標籤屬性]，然後在 [文字] 方塊中鍵入您想要的文字。  
  
18. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [指標 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/indicators-report-builder-and-ssrs.md)  
  
  
