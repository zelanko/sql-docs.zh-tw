---
title: 在圓形圖上顯示百分比值 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: eb905fc1-5235-4773-a27e-b07be9318be5
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b3beb87611f258d0c028b0a02b5d226864314620
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66106029"
---
# <a name="display-percentage-values-on-a-pie-chart-report-builder-and-ssrs"></a>在圓形圖上顯示百分比值 (報表產生器及 SSRS)
  根據預設，圖例中會顯示類別目錄來識別每個值。 如果您已使用類別目錄標籤做為圓形圖的標籤，則可能會想在圖例中顯示百分比。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-display-percentage-values-as-labels-on-a-pie-chart"></a>將百分比值顯示為圓形圖的標籤  
  
1.  將圓形圖加入到報表中。 如需詳細資訊，請參閱[將圖表加入至報表 &#40;報表產生器及 SSRS&#41;](add-a-chart-to-a-report-report-builder-and-ssrs.md)。  
  
2.  在設計介面上，以滑鼠右鍵按一下圓形圖，然後選取 [顯示資料標籤]。 資料標籤會顯示在圓形圖的每個扇區內。  
  
3.  在設計介面上，以滑鼠右鍵按一下標籤，然後選取 [數列標籤屬性]。 [數列標籤屬性] 對話方塊便會出現。  
  
4.  型別`#PERCENT`for**標籤資料**選項。  
  
5.  (選擇性) 若要指定標籤所顯示的小數位數，請輸入 "#PERCENT{P*n*}"，其中 *n* 是要顯示的小數位數。 例如，如果不要顯示任何小數位數，請輸入 "#PERCENT{P0}"。  
  
### <a name="to-display-percentage-values-in-the-legend-of-a-pie-chart"></a>若要在圓形圖的圖例中顯示百分比值  
  
1.  在設計介面上，以滑鼠右鍵按一下圓形圖，然後選取 [數列屬性]。 [數列屬性] 對話方塊隨即顯示。  
  
2.  在 **圖例**，型別`#PERCENT`如**自訂圖例文字**屬性。  
  
## <a name="see-also"></a>另請參閱  
 [圓形圖 &#40;報表產生器及 SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [在圖表上格式化圖例 &#40;報表產生器及 SSRS&#41;](chart-legend-formatting-report-builder.md)   
 [在圓形圖外部顯示資料點標籤 &#40;報表產生器及 SSRS&#41;](display-data-point-labels-outside-a-pie-chart-report-builder-and-ssrs.md)   
 [收集圓形圖上的小配量 &#40;報表產生器及 SSRS&#41;](collect-small-slices-on-a-pie-chart-report-builder-and-ssrs.md)  
  
  
