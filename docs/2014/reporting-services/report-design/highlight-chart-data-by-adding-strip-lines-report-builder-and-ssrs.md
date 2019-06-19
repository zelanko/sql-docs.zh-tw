---
title: 新增帶狀線來強調圖表資料 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: addd6137-4b6e-4e88-a7e8-9600fcd1ccce
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c50d242c7528485d5d21aa10f2680094628b484b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66105715"
---
# <a name="highlight-chart-data-by-adding-strip-lines-report-builder-and-ssrs"></a>加入帶狀線來強調圖表資料 (報表產生器及 SSRS)
  帶狀線 (或稱寬帶) 是水平或垂直的範圍，這些範圍會以規則或自訂的間隔來繪製圖表背景的陰影。 您可以使用區域線：  
  
-   改善可讀性以在圖表上尋找個別值。 以固定間隔指定區域線，這有助於在讀取圖表時區隔資料點。  
  
-   反白顯示以固定間隔發生的日期。 例如，您可以在銷售報表中使用區域線來識別週末資料點。  
  
-   反白顯示特定的關鍵範圍。 續前例，您可以使用一個區域線來反白顯示 $80 和 $100 之間的最高銷售範圍。  
  
 區域線不適用於「形狀」或「極座標」圖表類型。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-display-interlaced-strip-lines-at-regular-intervals-on-a-chart"></a>在圖表上以固定間隔顯示交錯的帶狀線  
  
1.  若要顯示水平帶狀線，請以滑鼠右鍵按一下垂直圖表軸，然後按一下 [垂直軸屬性]  。  
  
     若要顯示垂直帶狀線，請以滑鼠右鍵按一下水平圖表軸，然後按一下 [水平軸屬性]  。  
  
2.  選取 [使用交錯式]  選項。 灰色帶狀線會出現在圖表上。  
  
3.  (選擇性) 使用相鄰的 [色彩]  下拉式清單來指定帶狀線的色彩。  
  
### <a name="to-display-interlaced-strip-lines-at-custom-intervals-on-a-chart"></a>在圖表上以自訂間隔顯示交錯的帶狀線  
  
1.  若要顯示水平帶狀線，請以滑鼠右鍵按一下垂直圖表軸，然後按一下 [垂直軸屬性]  。  
  
     若要顯示垂直帶狀線，請以滑鼠右鍵按一下水平圖表軸，然後按一下 [水平軸屬性]  。  
  
     軸屬性會在 [屬性] 視窗中顯示。  
  
2.  在 [屬性] 窗格的 [外觀]  區段中，針對 StripLines 屬性按一下 [編輯集合] 按鈕 (…) 來開啟 [ChartStripLine 集合編輯器]  。  
  
3.  按一下 [新增]  ，將新的帶狀線新增集合。  
  
4.  按一下 [StripWidth] 來指定帶狀線的寬度，在報表上是以英吋表示。 如果要反白顯示日期或時間，請按一下 [StripWidthType] 並選取時間間隔。  
  
5.  輸入 Interval 的值或運算式，以指定帶狀線重複的頻率。  例如，如果指定的間隔為 10，而區域線寬度為 5，則區域線會在 0 到 5、15 到 20、30 到 35 的值位置顯示，以此類推。  
  
> [!NOTE]  
>  根據預設，Interval 是設為 [自動]，代表圖表不會計算自訂帶狀線的間隔。 只有在有設定間隔值時，圖表才會計算區域線的間隔。  
  
## <a name="see-also"></a>另請參閱  
 [格式化圖表上的軸標籤 &#40;報表產生器及 SSRS&#41;](formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
 [格式化圖表 &#40;報表產生器和 SSRS&#41;](formatting-a-chart-report-builder-and-ssrs.md)   
 [將移動平均加入至圖表 &#40;報表產生器及 SSRS&#41;](add-a-moving-average-to-a-chart-report-builder-and-ssrs.md)  
  
  
