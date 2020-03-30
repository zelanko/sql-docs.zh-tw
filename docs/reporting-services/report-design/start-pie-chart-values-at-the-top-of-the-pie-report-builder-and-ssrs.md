---
title: 從圓形圖頂端開始繪製圓形圖值 (報表產生器) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: d0e6fb59-ca4e-4d70-97cb-0ad183da21d3
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 3f23163da5fc4b23a364646be607167e663187fd
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "77080896"
---
# <a name="start-pie-chart-values-at-the-top-of-the-pie-report-builder-and-ssrs"></a>從圓形圖頂端開始繪製圓形圖值 (報表產生器及 SSRS)
依預設，在 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 分頁報表的圓形圖中，資料集的第一個值是從 90 度開始 (從圓形圖頂端算起)。 

![report-builder-pie-chart-start-at-90](../../reporting-services/media/report-builder-pie-chart-start-at-90.png)

*圖表值從 90 度開始。*

你可能會希望第一個值在頂端開始。 

![report-builder-pie-chart-start-at-top](../../reporting-services/media/report-builder-pie-chart-start-at-top.png)

*圖表值從圖表頂端算起。*
  
## <a name="to-start-the-pie-chart-at-the-top-of-the-pie"></a>若要從圓形圖頂端開始繪製圓形圖  
  
1.  按一下圓形圖本身。  
  
2.  如果 [屬性]  窗格沒有開啟，請按一下 [檢視]  索引標籤上的 [屬性]  。  
  
3.  在 [屬性]  窗格的 [自訂屬性]  底下，將 [PieStartAngle]  從 **0** 變更為 **270**。  
  
4.  按一下 [執行]  以預覽報表。  
  
 第一個值現在從圓形圖的頂端開始繪製。  
  
## <a name="see-also"></a>另請參閱  
 [格式化圖表 &#40;報表產生器和 SSRS&#41;](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)   
 [圓形圖 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/pie-charts-report-builder-and-ssrs.md)  
  
  
