---
title: 指定軸間隔 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: ae46712d-a5bf-44c0-9929-e30ccc1e7e33
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 8b86ef40b0a796c1d340a1d7ccadcc68fcdbed74
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48151938"
---
# <a name="specify-an-axis-interval-report-builder-and-ssrs"></a>指定軸間隔 (報表產生器及 SSRS)
  軸間隔定義軸上的標籤數及隨附的刻度。 在值軸上，軸間隔會為圖表上的資料點提供一致的量值； 不過，在類別目錄軸上，這項功能則可能導致類別目錄無法顯示軸標籤。 您可以在軸 Interval 屬性中指定所需間隔數。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 會根據結果集中的資料，在執行階段計算間隔數。 如需如何計算軸間隔的詳細資訊，請參閱[格式化圖表上的軸標籤 &#40;報表產生器及 SSRS&#41;](formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)。  
  
 此主題並不適用於類別目錄軸上的日期或時間值。 根據預設，`DateTime`值會顯示為天。 若要指定其他的日期或時間間隔 (例如月份或時間間隔)，則必須設定軸標籤的格式，並將軸設定為顯示 `DateTime` 類型 (而非 `String` 類型) 的執行個體。 此外，也必須設定 Interval 屬性。 如需詳細資訊，請參閱[將軸標籤格式化成日期或貨幣 &#40;報表產生器及 SSRS&#41;](format-axis-labels-as-dates-or-currencies-report-builder-and-ssrs.md)。  
  
 此主題並不適用於圓形圖、環圈圖、漏斗圖或金字塔圖，因為這些圖表並沒有軸。  
  
> [!NOTE]  
>  類別目錄軸通常是水平軸或 X 軸。 不過，如果是長條圖，類別目錄軸會是垂直軸或 Y 軸。  
  
 指定不同軸間隔的圖表範例可從範例報表取得。 如需下載這個範例報表及其他項目的詳細資訊，請參閱 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][報表產生器與報表設計師範例報表](http://go.microsoft.com/fwlink/?LinkId=198283)：  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-show-all-category-labels-on-the-x-axis"></a>若要在 X 軸上顯示所有類別目錄標籤  
  
1.  以滑鼠右鍵按一下類別目錄軸，然後按一下 **[軸屬性]**。 **[軸屬性]** 對話方塊隨即開啟。  
  
2.  在 **軸選項**，將`Interval`要**1**。 每個類別目錄群組標籤隨即顯示。 如果想要在 X 軸上每隔一個類別目錄群組標籤進行顯示，請輸入 **2**。  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
    > [!NOTE]  
    >  在設定軸間隔後，所有的自動標籤都會停用。 如果指定軸間隔的值，則可能會遭遇非預期的標籤行為，依類別目錄軸上有多少類別目錄而定。  
  
### <a name="to-enable-a-variable-interval-calculation-on-an-axis"></a>在軸上啟用可變間隔計算  
  
1.  以滑鼠右鍵按一下要變更的圖表軸，然後按一下 **[軸屬性]**。 **[軸屬性]** 對話方塊隨即開啟。  
  
2.  在 **軸選項**，將`Interval`要**自動**。圖表將顯示可納入軸的最佳類別目錄標籤數目。  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [格式化圖表 &#40;報表產生器和 SSRS&#41;](formatting-a-chart-report-builder-and-ssrs.md)   
 [格式化圖表上的資料點&#40;報表產生器及 SSRS&#41;](formatting-data-points-on-a-chart-report-builder-and-ssrs.md)   
 [在資料區中排序資料 &#40;報表產生器及 SSRS&#41;](sort-data-in-a-data-region-report-builder-and-ssrs.md)   
 [軸屬性對話方塊、軸選項 &#40;報表產生器及 SSRS&#41;](../axis-properties-dialog-box-axis-options-report-builder-and-ssrs.md)   
 [指定對數刻度 &#40;報表產生器及 SSRS&#41;](specify-a-logarithmic-scale-report-builder-and-ssrs.md)   
 [繪製副座標軸上的資料 &#40;報表產生器及 SSRS&#41;](plot-data-on-a-secondary-axis-report-builder-and-ssrs.md)  
  
  
