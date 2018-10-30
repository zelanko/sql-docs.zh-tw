---
title: 指定軸間隔 (報表產生器及 SSRS) | Microsoft Docs
ms.date: 09/02/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: ae46712d-a5bf-44c0-9929-e30ccc1e7e33
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 05e0650c71c7f2ed8f9dc51bf01bbb33e325add5
ms.sourcegitcommit: 3daacc4198918d33179f595ba7cd4ccb2a13b3c0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/25/2018
ms.locfileid: "50030177"
---
# <a name="specify-an-axis-interval-report-builder-and-ssrs"></a>指定軸間隔 (報表產生器及 SSRS)
了解如何藉由設定 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 分頁報表的軸間隔，在圖表中變更類別 (x) 軸中標籤及刻度的數目。
 
在值軸上 (通常是 y 軸)，軸間隔會為圖表上的資料點提供一致的量值； 

但在類別軸上 (通常是 x 軸)，有時自動軸間隔會產生沒有軸標籤的類別。 您可以在軸 Interval 屬性中指定所需間隔數。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 會根據結果集中的資料，在執行階段計算間隔數。 如需如何計算軸間隔的詳細資訊，請參閱 [格式化圖表上的軸標籤](../../reporting-services/report-design/formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)。  

若要嘗試使用範例資料設定軸間隔，請參閱[教學課程︰將直條圖新增至報表 (報表產生器)](Tutorial:%20Add%20a%20Column%20Chart%20to%20Your%20Report%20\(Report%20Builder\).md)。
  
> [!NOTE]  
>  類別目錄軸通常是水平軸或 X 軸。 不過，如果是長條圖，類別目錄軸會是垂直軸或 Y 軸。  
>
> 本主題不適用於︰
>-   在類別軸上的日期或時間值。 根據預設， **DateTime** 值會顯示為天。 您可以指定不同的日期或時間間隔，例如一個月或時間間隔。 如需詳細資訊，請參閱 [將軸標籤格式化成日期或貨幣](../../reporting-services/report-design/format-axis-labels-as-dates-or-currencies-report-builder-and-ssrs.md)。  
>-  圓形圖、環圈圖、漏斗圖或金字塔圖，因為這些圖表並沒有軸。 
  
## <a name="to-show-all-the-category-labels-on-the-x-axis"></a>在 X 軸上顯示所有類別標籤  

此直條圖中，水平標籤間隔設定為 Auto。

![report-builder-column-chart-preview-x-axis-interval-auto](../../reporting-services/report-design/media/report-builder-column-chart-preview-x-axis-interval-auto.png)
  
1.  以滑鼠右鍵按一下類別軸，然後按一下 [水平軸屬性]。   

    ![report-builder-column-chart-x-axis-labels](../../reporting-services/report-design/media/report-builder-column-chart-x-axis-labels.png)
  
2.  在 [水平軸屬性] 對話方塊 > [軸選項] 索引標籤上，將 [間隔] 設為 **1** 以顯示每個類別群組標籤。 若要在 X 軸上每隔一個類別目錄群組標籤進行顯示，請輸入 **2**。 

     ![report-builder-column-chart-x-axis-interval-one](../../reporting-services/report-design/media/report-builder-column-chart-x-axis-interval-one.png)
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

    現在直條圖會顯示其所有的水平軸標籤。

    ![report-builder-column-chart-preview-x-axis-interval-one](../../reporting-services/report-design/media/report-builder-column-chart-preview-x-axis-interval-one.png)
  
    > [!NOTE]  
    >  在設定軸間隔後，所有的自動標籤都會停用。 如果指定軸間隔的值，則可能會看到非預期的標籤行為，依類別目錄軸上有多少類別而定。  

## <a name="change-the-label-interval-in-properties-pane"></a>變更 [屬性] 窗格中的標籤間隔

您也可以在 [屬性] 窗格中設定標籤間隔。

1.  在報表設計檢視中，按一下圖表，然後選取水平軸標籤。

3. 在 [屬性] 窗格中，將 LabelInterval 設為 **1**。

    ![report-builder-column-chart-set-label-interval](../../reporting-services/media/report-builder-column-chart-set-label-interval.png)

    這個圖表與在設計檢視中相同。 
    
5.  按一下 **[執行]** 預覽報表。

    ![report-builder-column-chart-label-interval-one-preview](../../reporting-services/media/report-builder-column-chart-label-interval-one-preview.png)
    
    現在，圖表會顯示其所有標籤。
  
## <a name="to-enable-a-variable-interval-calculation-on-an-axis"></a>在軸上啟用可變間隔計算  

根據預設， [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 會將軸間隔設為 [自動]。此程序說明如何將它設回預設值。 
  
1.  以滑鼠右鍵按一下要變更的圖表軸，然後按一下 **[軸屬性]**。 
  
2.  在 [水平軸屬性] 對話方塊 > [軸選項] 索引標籤上，將 [間隔] 設為 [自動]。圖表將顯示可納入軸的最佳類別目錄標籤數目。  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [格式化圖表 &#40;報表產生器和 SSRS&#41;](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)   
 [格式化圖表上的資料點 (報表產生器及 SSRS)](../../reporting-services/report-design/formatting-data-points-on-a-chart-report-builder-and-ssrs.md)   
 [在資料區中排序資料 (報表產生器及 SSRS)](../../reporting-services/report-design/sort-data-in-a-data-region-report-builder-and-ssrs.md)   
 [軸屬性對話方塊，軸選項 &#40;報表產生器及 SSRS&#41;](https://msdn.microsoft.com/library/b276e210-7a12-48ae-971b-7dabae51df11)   
 [指定對數刻度 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/specify-a-logarithmic-scale-report-builder-and-ssrs.md)   
 [繪製副座標軸上的資料 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/plot-data-on-a-secondary-axis-report-builder-and-ssrs.md)  
  
  
