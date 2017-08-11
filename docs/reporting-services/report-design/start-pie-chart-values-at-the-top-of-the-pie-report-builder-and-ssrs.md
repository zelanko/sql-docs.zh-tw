---
title: "從開始繪製圓形圖值上方的圓形圖 （報表產生器及 SSRS） |Microsoft 文件"
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
ms.assetid: d0e6fb59-ca4e-4d70-97cb-0ad183da21d3
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8a12864064849ffc3bb0fa6937833ffee57e0df5
ms.contentlocale: zh-tw
ms.lasthandoff: 08/09/2017

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
  
2.  如果 [屬性] 窗格沒有開啟，請按一下 [檢視] 索引標籤上的 [屬性]。  
  
3.  在 [屬性] 窗格的 [自訂屬性] 底下，將 [PieStartAngle] 從 **0** 變更為 **270**。  
  
4.  按一下 [執行] 以預覽報表。  
  
 第一個值現在從圓形圖的頂端開始繪製。  
  
## <a name="see-also"></a>請參閱＜  
 [格式化圖表 &#40;報表產生器及 SSRS &#41;](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)   
 [圓形圖 &#40;報表產生器及 SSRS &#41;](../../reporting-services/report-design/pie-charts-report-builder-and-ssrs.md)  
  
  
