---
title: 變更圖例項目的文字 (報表產生器) | Microsoft Docs
description: 了解如何變更圖例項目的文字，以顯示報表產生器中個別資料點的詳細資訊。
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 9e82fa34-17ed-494f-b25d-03dcc353a21f
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 7f13d4663cf0d4e27148e77eebc59068e8c36924
ms.sourcegitcommit: 02b22274da4a103760a376c4ddf26c4829018454
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/11/2020
ms.locfileid: "84681237"
---
# <a name="chart-legend---change-item-text-report-builder"></a>圖表圖例 - 變更項目文字 (報表產生器)
  將欄位放在圖表的 [值] 區域中時，系統會自動產生包含此欄位名稱的圖例項目。 每個圖例項目都會連接到報表上的個別數列，但是形狀圖例外 (其圖例會連接到個別資料點而非個別數列)。  
  
 在形狀圖上，您可以變更圖例項目的文字，以顯示有關個別資料點的詳細資訊。 例如，如果您要將資料點的值顯示為圖例中的百分比，可以使用關鍵字，例如， **#PERCENT**。 您可以配合關鍵字附加 .NET Framework 格式化程式碼來套用數值和日期格式。 如需關鍵字的詳細資訊，請參閱[格式化圖表上的資料點 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/formatting-data-points-on-a-chart-report-builder-and-ssrs.md)。  
  
 ![鮮明的圖表](../../reporting-services/report-design/media/sharpchart.png "鮮明的圖表")  
  
 在非形狀圖上，您可以變更圖例項目的文字。 例如，如果您的數列名稱為 "Series1"，您可能想要變更為其他敘述性的文字，例如 "Sales for 2008"。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-modify-the-text-that-appears-in-the-legend-on-a-shape-chart"></a>在形狀圖上修改出現在圖例中的文字  
  
1.  以滑鼠右鍵按一下數列，或以滑鼠右鍵按一下 [值] 區域中的欄位，然後選取 [數列屬性]。  
  
2.  按一下 [圖例]，然後在 [自訂圖例文字] 方塊中鍵入關鍵字。  
  
 下表提供用於 [自訂圖例文字] 屬性之圖表特定關鍵字的範例。 如需關鍵字的詳細資訊，請參閱[格式化圖表上的資料點 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/formatting-data-points-on-a-chart-report-builder-and-ssrs.md)。  
  
|關鍵字|描述|在圖例中顯示為文字的範例|  
|-------------|-----------------|---------------------------------------------------|  
|`#PERCENT{P1}`|將總值的百分比顯示為一個小數位數。|85.0%|  
|`#VALY`|顯示資料欄位的實際數值。|17000|  
|`#VALY{C2}`|將資料欄位的實際數值顯示為兩個小數位數的貨幣。|$17000.00|  
|`#AXISLABEL (#PERCENT{P0})`|顯示類別目錄欄位的文字表示法，後面接著每個類別目錄顯示在圖表上的百分比。|Michael Blythe (85%)|  
  
> [!NOTE]  
>  在 [數列群組] 區域中沒有指定任何欄位時，只能在執行階段評估 #AXISLABEL 關鍵字。  
  
### <a name="to-modify-the-text-that-appears-in-the-legend-on-a-non-shape-chart"></a>在非形狀圖上修改出現在圖例中的文字  
  
1.  以滑鼠右鍵按一下數列，或以滑鼠右鍵按一下 [值] 區域中的欄位，然後選取 [數列屬性]。  
  
2.  按一下 [圖例]，然後在 [自訂圖例文字] 方塊中鍵入圖例標籤。 數列會隨著您的文字更新。  
  
## <a name="see-also"></a>另請參閱  
 [在圖表上格式化圖例 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/chart-legend-formatting-report-builder.md)   
 [設定圖表上數列色彩的格式 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/formatting-series-colors-on-a-chart-report-builder-and-ssrs.md)   
 [隱藏圖表上的圖例項目 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/chart-legend-hide-items-report-builder.md)  
  
  
