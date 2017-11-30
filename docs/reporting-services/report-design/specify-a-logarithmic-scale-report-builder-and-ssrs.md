---
title: "指定對數刻度 (報表產生器及 SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f3092c1c-b128-433d-9a95-983508b2a8d4
caps.latest.revision: "7"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: b359abb24af2e1736097530973394a5b370223c2
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="specify-a-logarithmic-scale-report-builder-and-ssrs"></a>指定對數刻度 (報表產生器及 SSRS)
  如果您的資料在對數上成比例，您可能會想要考慮在 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 分頁報表的圖表上使用對數刻度。 這樣可以讓您的資料更容易管理，而有助於改善圖表的外觀。 大部分的對數刻度都使用 10 當做基底。  
  
 此功能僅能在值軸上使用。 值軸通常是圖表的垂直軸 (或 Y 軸)， 而在長條圖中，則為水平軸 (即 X 軸)。  
  
 如果您的軸為對數，系統就會以對數的方式縮放與該軸相關的其他所有屬性。 例如，如果您在軸上指定基底為 10 的對數刻度，將軸間隔設定為 2 就會產生將間隔範圍 10 自乘至 2 的乘冪或 100。 這表示，您的軸值將讀取 1、100 或 10000 而非 1、10、100、1000 或 10000 的預設結果。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-specify-a-logarithmic-scale"></a>若要指定對數刻度  
  
1.  以滑鼠右鍵按一下圖表的 Y 軸，然後按一下 [垂直軸屬性]。 [垂直軸屬性] 對話方塊隨即出現。  
  
2.  在 [軸選項] 中，選取 [使用對數刻度]。  
  
3.  在 [對數底數] 文字方塊中，為對數底數鍵入正值。 如果沒有指定任何值，對數基底預設為 10。  
  
## <a name="see-also"></a>另請參閱  
 [格式化圖表上的軸標籤 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
 [格式化圖表 &#40;報表產生器和 SSRS&#41;](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)   
 [將軸標籤格式化成日期或貨幣 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/format-axis-labels-as-dates-or-currencies-report-builder-and-ssrs.md)   
 [圖表 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)  
  
  
