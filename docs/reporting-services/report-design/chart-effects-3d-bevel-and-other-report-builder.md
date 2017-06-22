---
title: "3D、 浮凸和其他效果圖表 （報表產生器及 SSRS） |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- "10156"
ms.assetid: 18ef2119-2931-43ae-9078-f39b460462dd
caps.latest.revision: 10
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: f6d149a116c243fba0587afe1dcf969f9356c57f
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="chart-effects---3d-bevel-and-other-report-builder"></a>圖表效果的 3D、 浮凸和其他 （報表產生器）
  三維 (3D) 效果可用來針對 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 分頁報表中的圖表提供深度及增加視覺效果。 例如，若要強調分裂式圓形圖的特殊扇區，則可以旋轉及變更圖表的檢視方塊，讓使用者能首先注意該扇區。 將 3D 效果套用至圖表時，所有的漸層色彩和影線樣式都會停用。  
  
 您可以將三維效果套用至個別的圖表，也可以同時在相同報表上顯示二維和三維圖表。  
  
 您可以針對所有的圖表類型選取 [圖表區域屬性] 對話方塊中的 [啟用 3D]，以對圖表區域加入三維效果。 如需詳細資訊，請參閱 [將 3D 效果加入至圖表 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/chart-effects-add-3d-effects-report-builder.md)。  
  
 另一種對圖表加入視覺效果的方式是在直條圖、橫條圖、圓形圖及環圈圖中加入按鈕形、浮凸和材質樣式。 如需詳細資訊，請參閱[將斜面、浮凸與紋理樣式加入至圖表 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/chart-effects-add-bevel-emboss-or-texture-report-builder.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="coordinate-based-three-dimensional-charts"></a>以座標為基礎的三維圖表  
 三維效果在使用以座標為基礎的圖表類型 (直條圖、橫條圖、區域圖、點圖、折線圖和範圍圖) 時，會以第三個軸 (也稱為 Z 軸) 來顯示圖表。 在引進這第三個軸後，您就可以對圖表套用各種視覺增強功能。  
  
### <a name="changing-the-white-space-in-a-3d-chart"></a>變更 3D 圖表中的空白  
 以三維模式顯示圖表區域時，每個數列都會沿著圖表的 Z 軸以個別的資料列顯示。 若要變更每個數列之間的空白量，請變更 [3D 效果] 對話方塊中的 **[點間隙深度]** 屬性來修改圖表的點間隙深度。  
  
### <a name="changing-the-projection-of-a-3d-chart"></a>變更 3D 圖表的投射  
 3D 投射有兩種類型：傾斜和遠近景深。 圖表的傾斜投射會對二維圖表加入深度維度。 Z 軸會從與水平及垂直軸相等的角度繪製，水平及垂直軸則彼此垂直，與二維圖表中一樣。  
  
 遠近景深投射轉換圖表的方式則是估計檢視平面並重新繪製圖表，使其好像是從該點進行檢視一般。 **[旋轉]** 值會將檢視從 0 度的「地平面」垂直提升到頭頂的 90 度。 **[傾斜]** 值則會將檢視角度轉至左方或右方。 0 值與圖表的二維檢視相同。 **[遠近景深]** 值定義在顯示投射時使用的扭曲百分比。 這種投射類型會維持圖表的比例，但圖表的外觀會扭曲，所以使用較低的遠近景深比較有效。  
  
> [!NOTE]  
>  傾斜和遠近景深投射是不同的投射類型，所以不能同時用於相同的圖表。  
  
### <a name="clustering-data"></a>群集資料  
 在 2D 圖表中，多個資料數列會並列顯示。 群集則會在 3D 圖表的個別資料列上顯示個別數列。 例如，如果圖表包含三個資料點數列，則群集會沿著 Z 軸以個別的資料列顯示這三個數列。 依預設，以 3D 顯示的所有圖表類型都會進行群集。  
  
 橫條圖和直條圖都可以停用群集。 當群集停用時，多個橫條和直條數列會並排顯示於單一資料列。  
  
## <a name="shape-based-three-dimensional-charts"></a>以形狀為基礎的三維圖表  
 以形狀為基礎的圖表類型 (圓形圖、環圈圖、漏斗圖、金字塔圖) 可用的三維效果較少。 在使用以形狀為基礎的圖表類型時，只能變更旋轉及傾斜值。  
  
## <a name="rotations"></a>旋轉  
 可以將圖表從 -90 度水平及垂直旋轉至 90 度。 正值的水平角度會沿著 X 軸逆時針旋轉圖表，正值的垂直角度則會沿 Y 軸順時針旋轉圖表。  
  
## <a name="highlighting-3d-effects"></a>反白顯示 3D 效果  
 您可以透過 **[陰影]** 屬性來反白顯示 3D 圖表的樣式，這個屬性會在您選取圖表區域時顯示在 [屬性] 窗格的 [Area3DStyle] 下方。 簡單的光源樣式會對圖表區域項目套用相同的色調。 真實感的樣式會根據指定的光源角度而變更圖表區域項目的色調。  
  
## <a name="see-also"></a>請參閱＜  
 [格式化圖表上的軸標籤 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
 [格式化圖表 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)   
 [將 3D 效果加入至圖表 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/chart-effects-add-3d-effects-report-builder.md)  
  
  
