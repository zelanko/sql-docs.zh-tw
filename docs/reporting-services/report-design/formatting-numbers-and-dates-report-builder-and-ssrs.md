---
title: "格式化數字和日期 (報表產生器及 SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-design
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.rtp.rptdesigner.placeholderproperties.number.f1
- "10127"
- sql13.rtp.rptdesigner.textboxproperties.number.f1
- "10130"
- "10286"
- sql13.rtp.rptdesigner.serieslabelproperties.number.f1
- "10285"
- sql13.rtp.rptdesigner.axisproperties.number.f1
ms.assetid: 6de1a725-9f06-4708-be26-2d55e442e344
caps.latest.revision: "6"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 57bc37f13bdd0757a1142fbec57cd499e0c35fd7
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="formatting-numbers-and-dates-report-builder-and-ssrs"></a>格式化數字和日期 (報表產生器及 SSRS)
  您可以從對應資料區之 **[屬性]** 對話方塊的 **[數字]** 頁面選取一種格式，藉以格式化資料區中的數字和日期。  
  
 若要在文字方塊報表項目中指定格式字串，您需要選取要格式化的項目，按一下滑鼠右鍵，選取 **[文字方塊屬性]**，然後按一下 **[數字]**。 您可以使用相同的方式格式化資料表或矩陣資料區中的個別資料格，因為資料表或矩陣資料區中的資料格為個別的文字方塊。  
  
 圖表資料區通常會顯示類別目錄 (x) 軸上的日期，以及值 (y) 軸上的值。 若要指定圖表中的格式，請以滑鼠右鍵按一下軸，然後選取 **[軸屬性]**。 在值軸上，您僅能指定數字的格式。 如需詳細資訊，請參閱[格式化圖表上的軸標籤 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)。  
  
 若要指定量測計資料區中的格式，以滑鼠右鍵按一下量測計的標尺，然後選取 **[星形標尺屬性]** 或 **[線性標尺屬性]**。  
  
> [!NOTE]  
>  如果您想要使用的部分格式選項呈現灰色，這表示那些格式選項與資料來源中所設定之欄位的資料類型不相容。 例如，如果該欄位包含數值，但是欄位的資料類型為「字串」，則無法套用數值資料格式選項，例如貨幣或十進位。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="considerations-for-formatting-numbers-and-dates"></a>格式化數字和日期的考量  
 格式化報表中的數字和日期之前，請考慮下列事項：  
  
-   根據預設，數字會經過格式化以反映用戶端電腦上的文化特性設定。 使用格式字串來指定顯示數字的方式，因此不管檢視報表的人身在何處，格式都是一致的。  
  
-   在 **[數字]** 頁面上提供的格式為 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 標準數值格式字串的子集。 若要使用對話方塊中沒有顯示的自訂格式來格式化數字或日期，您可以針對數字或日期使用任何 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 格式字串。 如需有關自訂格式字串的詳細資訊，請參閱 MSDN 上的＜ [格式化型別](http://go.microsoft.com/fwlink/?LinkId=112024) ＞主題。  
  
-   如果已經指定自訂格式字串，其優先順序會高於文化專用的預設值。 例如，假設您設定 "#,###" 的自訂格式字串，將數字 1234 顯示為 1,234。 這對於美國的使用者與歐洲的使用者可能代表不同的意義。 在您指定自訂格式之前，請考慮您選擇的格式影響不同文化的使用者檢視報表的方式。  
  
-   如果您指定無效的格式字串，格式化的文字會解譯為覆寫格式的常值字串。  
  
-   如果您要在相同的文字方塊中格式化數字和字串的混合時，請考慮使用預留位置來分別格式化數字與其餘文字。 如需詳細資訊，請參閱 [格式化文字和預留位置 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/formatting-text-and-placeholders-report-builder-and-ssrs.md)。 如果在文字方塊上針對 Format 屬性指定的格式字串無效，則會略過該格式字串。 如果在圖表或量測計上針對 Format 屬性指定的格式字串無效，您所指定的格式字串會解譯為字串，而且不會套用該格式。  
  
-   如果您選取 **[類別目錄]** 底下的 **[貨幣]** ，並核取 **[值的顯示單位]**，您可以選取 **[千]**、 **[百萬]**或 **[十億]** 來使用財務格式顯示數值。 例如，如果欄位值為 1,789,905,394，而且您選取 **[十億]** 並指定 2 位小數位數，顯示在報表中的值為 1.78。  
  
## <a name="see-also"></a>另請參閱  
 [格式化文字和預留位置 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/formatting-text-and-placeholders-report-builder-and-ssrs.md)   
 [格式化線條、色彩和影像 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/formatting-lines-colors-and-images-report-builder-and-ssrs.md)   
 [格式化圖表 &#40;報表產生器和 SSRS&#41;](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)   
 [將軸標籤格式化成日期或貨幣 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/format-axis-labels-as-dates-or-currencies-report-builder-and-ssrs.md)   
 [格式化量測計上的標尺 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/formatting-scales-on-a-gauge-report-builder-and-ssrs.md)  
  
  
