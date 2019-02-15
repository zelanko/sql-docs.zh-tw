---
title: 設定圖表上數列色彩的格式 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10245"
- "10252"
- sql12.rtp.rptdesigner.serieslabelproperties.borders.f1
- sql12.rtp.rptdesigner.seriesproperties.borders.f1
ms.assetid: fe541501-cac5-47b1-b95f-c410db789190
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 3f3622ea10c5dbd0b38e7562ec8039fb1f28571b
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/15/2019
ms.locfileid: "56298166"
---
# <a name="formatting-series-colors-on-a-chart-report-builder-and-ssrs"></a>設定圖表上數列色彩的格式 (報表產生器及 SSRS)
  Reporting Services 為圖表提供數個內建的調色盤，或者您也可以定義自訂的調色盤。 根據預設，圖表會使用內建**BrightPastel**調色盤來填滿每個數列。 這些色彩也會出現在圖例中。 在圖表中加入多個序列時，圖表會以調色盤定義色彩的順序為序列指派色彩。  
  
 如果序列的數目超過調色盤中的色彩數，則圖表會重覆使用色彩，因此兩個序列可能會擁有相同的色彩。 如果您所使用的是形狀圖，就會經常發生這種情形，其中會為每個資料點指派調色盤的一個色彩。 為了避免混淆，請至少使用與圖表上的序列一樣多的色彩來定義自訂調色盤。  
  
 您可以選取新的調色盤，或從 [屬性] 窗格定義自訂調色盤。 如需詳細資訊，請參閱[使用調色盤定義圖表的色彩 &#40;報表產生器及 SSRS&#41;](define-colors-on-a-chart-using-a-palette-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="using-built-in-palettes"></a>使用內建調色盤  
 Reporting Services 提供預先定義的內建調色盤清單，可用來為圖表上的序列定義色彩集。 所有內建調色盤都包含 10 到 16 個色彩值。 您不能擴充內建調色盤來加入其他色彩，所以如果需要超過 16 種色彩，就必須定義自訂的調色盤。  
  
 如果您要列印報表，請考慮使用 [灰階] 調色盤。 這個調色盤會使用黑白色彩來表示圖表中的每個序列。  
  
 在舊版的 Reporting Services 中是使用名為「預設」的調色盤做為預設的圖表調色盤。 這個調色盤仍維持相同名稱以求一致性。 圖表將使用 [預設] 調色盤進行無接縫的升級，但在升級之後，您可以考慮加以變更。  
  
## <a name="using-custom-palettes"></a>使用自訂調色盤  
 如果要將自己的色彩套用至圖表，請使用自訂調色盤。 自訂調色盤可讓您將依照要在圖表上顯示色彩的順序，加入自己的色彩。 如果在設計階段時還不知道圖表中的序列數，則自訂調色盤特別有用。 如需詳細資訊，請參閱[使用調色盤定義圖表的色彩 &#40;報表產生器及 SSRS&#41;](define-colors-on-a-chart-using-a-palette-report-builder-and-ssrs.md)。  
  
## <a name="using-a-color-fill-on-each-series"></a>在每個序列上使用色彩填滿  
 您也可以針對圖表上的每個序列指定色彩，在圖表上定義自己的色彩。 若要進行這項作業，請開啟 [數列屬性] 對話方塊，然後設定 [填滿] 的 [色彩] 屬性。 這個方法會覆寫所有定義的調色盤。 一般來說，最好使用自訂調色盤來定義自己的色彩，因為可能要到處理報表之後，才會知道資料集中的序列數。  
  
 當您想要根據運算式有條件地設定序列的色彩時，這個方法最適用。  如需詳細資訊，請參閱 [格式化圖表上的資料點 &#40;報表產生器及 SSRS&#41;](formatting-data-points-on-a-chart-report-builder-and-ssrs.md)。  
  
## <a name="in-this-section"></a>本節內容  
 [跨多個形狀圖指定一致的色彩 &#40;報表產生器及 SSRS&#41;](charts-report-builder-and-ssrs.md)  
  
 [使用調色盤定義圖表的色彩 &#40;報表產生器及 SSRS&#41;](define-colors-on-a-chart-using-a-palette-report-builder-and-ssrs.md)  
  
 [加入帶狀線來強調圖表資料 &#40;報表產生器及 SSRS&#41;](highlight-chart-data-by-adding-strip-lines-report-builder-and-ssrs.md)  
  
## <a name="see-also"></a>另請參閱  
 [格式化圖表 &#40;報表產生器和 SSRS&#41;](formatting-a-chart-report-builder-and-ssrs.md)   
 [將斜面、浮凸與紋理樣式加入至圖表 &#40;報表產生器及 SSRS&#41;](chart-effects-add-bevel-emboss-or-texture-report-builder.md)   
 [圖表 &#40;報表產生器及 SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [在圖表上格式化圖例 &#40;報表產生器及 SSRS&#41;](chart-legend-formatting-report-builder.md)  
  
  
