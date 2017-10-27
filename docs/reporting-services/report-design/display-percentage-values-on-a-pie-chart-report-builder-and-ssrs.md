---
title: "圓形圖 （報表產生器及 SSRS） 上顯示百分比值 |Microsoft 文件"
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
ms.assetid: eb905fc1-5235-4773-a27e-b07be9318be5
caps.latest.revision: 9
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Active
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 6c0fdf9d1b694f2f6d49389e913d1c156ba77838
ms.contentlocale: zh-tw
ms.lasthandoff: 08/09/2017

---
# <a name="display-percentage-values-on-a-pie-chart-report-builder-and-ssrs"></a>在圓形圖上顯示百分比值 (報表產生器及 SSRS)
在[!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)]分頁的報表，依預設圖例顯示的類別。 您也可以在圖例或本身的圓形圖配量的百分比。   

![report-builder-pie-chart-preview-percents](../../reporting-services/media/report-builder-pie-chart-preview-percents.png)

 [教學課程： 將圓形圖加入至報表 （報表產生器）](Tutorial:%20Add%20a%20Pie%20Chart%20to%20Your%20Report%20\(Report%20Builder\).md)會引導您完成百分比加入圓形圖配量，如果您想要先嘗試這以範例資料。
 
  
## <a name="to-display-percentage-values-as-labels-on-a-pie-chart"></a>將百分比值顯示為圓形圖的標籤  
  
1.  將圓形圖加入到報表中。 如需詳細資訊，請參閱[將圖表加入至報表 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/add-a-chart-to-a-report-report-builder-and-ssrs.md)。  
  
2.  在設計介面上以滑鼠右鍵按一下圓形圖，然後選取 [顯示資料標籤]。 資料標籤會顯示在圓形圖的每個扇區內。  
  
3.  在設計介面上以滑鼠右鍵按一下標籤，然後選取 [數列標籤屬性]。 [數列標籤屬性] 對話方塊便會出現。  
  
4.  針對 [標籤資料] 選項輸入 **#PERCENT**。  
  
5.  （選擇性）若要指定標籤所顯示的方式有許多小數位數，請輸入"#PERCENT {P*n*}"其中 *n* 是要顯示的小數位數。 例如，如果不要顯示任何小數位數，請輸入 "#PERCENT{P0}"。  
  
## <a name="to-display-percentage-values-in-the-legend-of-a-pie-chart"></a>若要在圓形圖的圖例中顯示百分比值  
  
1.  在設計介面上，以滑鼠右鍵按一下圓形圖，然後選取 [數列屬性]。 [數列屬性] 對話方塊隨即顯示。  
  
2.  在 [圖例] 中，針對 [自訂圖例文字] 屬性輸入 **#PERCENT**。  
  
## <a name="see-also"></a>另請參閱  
* [教學課程： 將圓形圖加入至報表 （報表產生器）](Tutorial:%20Add%20a%20Pie%20Chart%20to%20Your%20Report%20\(Report%20Builder\).md)
*  [圓形圖 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/pie-charts-report-builder-and-ssrs.md)   
*  [在圖表上格式化圖例 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/chart-legend-formatting-report-builder.md)   
*  [在圓形圖外部顯示資料點標籤 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/display-data-point-labels-outside-a-pie-chart-report-builder-and-ssrs.md)   
 
  

