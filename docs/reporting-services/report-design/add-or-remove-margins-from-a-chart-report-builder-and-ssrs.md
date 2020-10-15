---
title: 新增或移除圖表中的邊界 (報表產生器) | Microsoft Docs
description: 在報表產生器中，從直條圖或散佈圖新增或移除邊界。 改善編頁報表的可讀性或外觀。
ms.date: 03/03/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 91c43f58-5771-4d33-a54d-0e802d2f5cba
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: bbe5af103737cb9b4a5ba7e063f19b9cd6c1da41
ms.sourcegitcommit: fe59f8dc27fd633f5dfce54519d6f5dcea577f56
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/09/2020
ms.locfileid: "91935357"
---
# <a name="add-or-remove-margins-from-a-chart-report-builder-and-ssrs"></a>加入或移除圖表中的邊界 (報表產生器及 SSRS)
對於 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 分頁報表中的直條圖和散佈圖類型中，圖表會自動在 X 軸的端點加入側邊界。 在橫條圖類型中，圖表會自動在 Y 軸的端點加入側邊界。 在所有其他圖表類型中，圖表中都不會加入側邊界。 您不可以變更邊界的大小。  
  
 此主題不適用於圓形圖、環圈圖、漏斗圖或金字塔圖等圖表類型。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-enable-or-disable-side-margins"></a>啟用或停用側邊界  
  
1.  以滑鼠右鍵按一下座標軸，然後選取 [軸屬性]。 [垂直軸屬性] 或 [水平軸屬性] 對話方塊隨即出現。  
  
2.  在 [軸選項] 頁面上，設定 [側邊界] 屬性：  
  
    -   **自動** ：圖表將會判斷是否要根據圖表類型加入側邊界。  
  
    -   **停用** ：橫條圖、直條圖和散佈圖不會有側邊界。  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [格式化圖表上的軸標籤 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
 [軸屬性對話方塊、軸選項 &#40;報表產生器及 SSRS&#41;](/previous-versions/sql/)   
 [指定軸間隔 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/specify-an-axis-interval-report-builder-and-ssrs.md)   
 [將軸標籤格式化成日期或貨幣 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/format-axis-labels-as-dates-or-currencies-report-builder-and-ssrs.md)   
 [圖表 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)  
  
