---
title: 指定對數刻度 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: f3092c1c-b128-433d-9a95-983508b2a8d4
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 0910888603528d899f0180bf96c66cfbea045aa4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66104941"
---
# <a name="specify-a-logarithmic-scale-report-builder-and-ssrs"></a>指定對數刻度 (報表產生器及 SSRS)
  如果您的資料在對數上成比例，您可能會想要考慮在圖表上使用對數刻度。 這樣可以讓您的資料更容易管理，而有助於改善圖表的外觀。 大部分的對數刻度都使用 10 當做基底。  
  
 此功能僅能在值軸上使用。 值軸通常是圖表的垂直軸 (或 Y 軸)， 而在長條圖中，則為水平軸 (即 X 軸)。  
  
 如果您的軸為對數，系統就會以對數的方式縮放與該軸相關的其他所有屬性。 例如，如果您在軸上指定基底為 10 的對數刻度，將軸間隔設定為 2 就會產生將間隔範圍 10 自乘至 2 的乘冪或 100。 這表示，您的軸值將讀取 1、100 或 10000 而非 1、10、100、1000 或 10000 的預設結果。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-specify-a-logarithmic-scale"></a>若要指定對數刻度  
  
1.  以滑鼠右鍵按一下圖表的 Y 軸，然後按一下 [垂直軸屬性]  。 [垂直軸屬性]  對話方塊隨即出現。  
  
2.  在 [軸選項]  中，選取 [使用對數刻度]  。  
  
3.  在 [對數底數]  文字方塊中，為對數底數鍵入正值。 如果沒有指定任何值，對數基底預設為 10。  
  
## <a name="see-also"></a>另請參閱  
 [格式化圖表上的軸標籤 &#40;報表產生器及 SSRS&#41;](formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
 [格式化圖表 &#40;報表產生器和 SSRS&#41;](formatting-a-chart-report-builder-and-ssrs.md)   
 [將軸標籤格式化成日期或貨幣 &#40;報表產生器及 SSRS&#41;](format-axis-labels-as-dates-or-currencies-report-builder-and-ssrs.md)   
 [圖表 &#40;報表產生器及 SSRS&#41;](charts-report-builder-and-ssrs.md)  
  
  
