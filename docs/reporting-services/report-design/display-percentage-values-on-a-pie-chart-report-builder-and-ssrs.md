---
title: "在圓形圖上顯示百分比值 (報表產生器及 SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: eb905fc1-5235-4773-a27e-b07be9318be5
caps.latest.revision: 9
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 6
---
# 在圓形圖上顯示百分比值 (報表產生器及 SSRS)
  根據預設，圖例中會顯示類別目錄來識別每個值。 如果您已使用類別目錄標籤做為圓形圖的標籤，則可能會想在圖例中顯示百分比。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### 將百分比值顯示為圓形圖的標籤  
  
1.  將圓形圖加入到報表中。 如需詳細資訊，請參閱[將圖表加入至報表 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/add-a-chart-to-a-report-report-builder-and-ssrs.md)。  
  
2.  在設計介面上以滑鼠右鍵按一下圓形圖，然後選取 [顯示資料標籤]。 資料標籤會顯示在圓形圖的每個扇區內。  
  
3.  在設計介面上以滑鼠右鍵按一下標籤，然後選取 [數列標籤屬性]。 [數列標籤屬性] 對話方塊便會出現。  
  
4.  針對 [標籤資料] 選項輸入 **#PERCENT**。  
  
5.  (選擇性) 若要指定標籤所顯示的小數位數，請輸入 "#PERCENT{P*n*}"，其中 *n* 是要顯示的小數位數。 例如，如果不要顯示任何小數位數，請輸入 "#PERCENT{P0}"。  
  
### 若要在圓形圖的圖例中顯示百分比值  
  
1.  在設計介面上，以滑鼠右鍵按一下圓形圖，然後選取 [數列屬性]。 [數列屬性] 對話方塊隨即顯示。  
  
2.  在 [圖例] 中，針對 [自訂圖例文字] 屬性輸入 **#PERCENT**。  
  
## 另請參閱  
 [圓形圖 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/pie-charts-report-builder-and-ssrs.md)   
 [在圖表上格式化圖例 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/formatting-the-legend-on-a-chart-report-builder-and-ssrs.md)   
 [在圓形圖外部顯示資料點標籤 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/display-data-point-labels-outside-a-pie-chart-report-builder-and-ssrs.md)   
 [收集圓形圖上的小配量 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/collect-small-slices-on-a-pie-chart-report-builder-and-ssrs.md)  
  
  