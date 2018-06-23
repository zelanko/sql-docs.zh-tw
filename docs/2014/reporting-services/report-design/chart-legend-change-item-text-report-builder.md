---
title: 變更圖例項目的文字 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 9e82fa34-17ed-494f-b25d-03dcc353a21f
caps.latest.revision: 8
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 54ed1dcca5d1e690990953cd2c02d4ad4e1b7879
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36029777"
---
# <a name="change-the-text-of-a-legend-item-report-builder-and-ssrs"></a>變更圖例項目的文字 (報表產生器及 SSRS)
  將欄位放在圖表的 [值] 區域中時，系統會自動產生包含此欄位名稱的圖例項目。 每個圖例項目都會連接到報表上的個別數列，但是形狀圖例外 (其圖例會連接到個別資料點而非個別數列)。  
  
 在形狀圖上，您可以變更圖例項目的文字，以顯示有關個別資料點的詳細資訊。 例如，如果您想要的資料點值顯示為圖例中的百分比，您可以使用關鍵字例如`#PERCENT`。 您可以配合關鍵字附加 .NET Framework 格式化程式碼來套用數值和日期格式。 如需關鍵字的詳細資訊，請參閱[格式化圖表上的資料點 &#40;報表產生器及 SSRS&#41;](formatting-data-points-on-a-chart-report-builder-and-ssrs.md)。  
  
 ![鮮明的圖表](../media/sharpchart.png "鮮明的圖表")  
  
 在非形狀圖上，您可以變更圖例項目的文字。 例如，如果您的數列名稱為 "Series1"，您可能想要變更為其他敘述性的文字，例如 "Sales for 2008"。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-modify-the-text-that-appears-in-the-legend-on-a-shape-chart"></a>在形狀圖上修改出現在圖例中的文字  
  
1.  以滑鼠右鍵按一下數列，或以滑鼠右鍵按一下 [值] 區域中的欄位，然後選取 [數列屬性]。  
  
2.  按一下 [圖例]，然後在 [自訂圖例文字] 方塊中鍵入關鍵字。  
  
 下表提供用於 [自訂圖例文字] 屬性之圖表特定關鍵字的範例。 如需關鍵字的詳細資訊，請參閱[格式化圖表上的資料點 &#40;報表產生器及 SSRS&#41;](formatting-data-points-on-a-chart-report-builder-and-ssrs.md)。  
  
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
 [在圖表上格式化圖例&#40;報表產生器和 SSRS&#41;](chart-legend-formatting-report-builder.md)   
 [設定圖表上數列色彩的格式 &#40;報表產生器及 SSRS&#41;](formatting-series-colors-on-a-chart-report-builder-and-ssrs.md)   
 [隱藏圖表上的圖例項目 &#40;報表產生器及 SSRS&#41;](chart-legend-hide-items-report-builder.md)  
  
  