---
title: 將邊框新增至圖表 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: ca0c5040-40bb-4cb7-bc2b-5bcbe73858bb
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b6b354cbb09a61e5fdd2444afaff0e6c8e0bb5b7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66106905"
---
# <a name="add-a-border-frame-to-a-chart-report-builder-and-ssrs"></a>將邊框加入至圖表 (報表產生器及 SSRS)
  若要為圖表提供一個更吸引人的外觀，請考慮在圖表的周圍使用邊框。 您可以使用 **[圖表屬性]** 對話方塊或 [屬性] 窗格來選取邊框。 圖表邊框無法套用到其他任何資料區。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-apply-a-border-to-a-chart"></a>將框線套用到圖表  
  
1.  以滑鼠右鍵按一下圖表的任何位置，並選取 [圖表屬性]  。  
  
    > [!NOTE]  
    >  如果您沒有看到 [圖表屬性]  ，請指向捷徑功能表上的 [圖表]  ，並選取 [圖表屬性]  。  
  
2.  選取 **[框線]** ，然後按一下要套用到圖表的框線類型。  
  
3.  (選擇性) 選取一個值，或輸入代表框線樣式的運算式。  
  
4.  (選擇性) 指定將會繪製在圖表周圍當做框線的線條色彩。  
  
    > [!NOTE]  
    >  **[線條色彩]** 清單包含常見的色彩。 如果您想要從更多色彩的清單中選取，請按一下清單中的 [更多色彩]  ，或是按一下清單旁邊的運算式 (**fx**) 按鈕，叫出 [運算式]  編輯器。  
  
5.  (選擇性) 指定框線的寬度。 有效值介於 0.25pt 和 20pt 之間。 為了得到最佳視覺效果，請考慮將框線的大小維持在 1 與 3pt 之間。  
  
6.  (選擇性) 如果您的報表包含白色以外的背景色彩，請考慮定義相同色彩的頁面色彩。 頁面色彩就是框線外面的背景色彩。  
  
7.  (選擇性) 如果您選擇框架類型，請為框架指定樣式和色彩。 **[框架填滿色彩]** 清單包含常見的色彩。  
  
## <a name="see-also"></a>另請參閱  
 [圖表 &#40;報表產生器及 SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [格式化圖表 &#40;報表產生器及 SSRS&#41;](formatting-a-chart-report-builder-and-ssrs.md)   
 [將斜面、浮凸與紋理樣式加入至圖表 &#40;報表產生器及 SSRS&#41;](chart-effects-add-bevel-emboss-or-texture-report-builder.md)  
  
  
