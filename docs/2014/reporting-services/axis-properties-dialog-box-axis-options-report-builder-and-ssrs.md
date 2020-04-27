---
title: 軸屬性對話方塊、軸選項（報表產生器及 SSRS） |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.axisproperties.axisoptions.f1
- "10138"
ms.assetid: b276e210-7a12-48ae-971b-7dabae51df11
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ff9f3281e47cf6dfdf8a189c653d0e061f4a761d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66109954"
---
# <a name="axis-properties-dialog-box-axis-options-report-builder-and-ssrs"></a>軸屬性對話方塊、軸選項 (報表產生器及 SSRS)
  選取 [**水準**] 或 [**垂直軸屬性**] 對話方塊上的 [**軸選項**]，即可定義圖表中指定之軸的外觀。 在舊版 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]中，圖表預設會顯示 X 軸上的所有標籤。 不過，在 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 2008 中，圖表會略過標籤，以便產生較清晰的圖表影像並避免標籤互相衝突。 如需詳細資訊，請參閱[格式化圖表上的軸標籤 &#40;報表產生器及 SSRS&#41;](report-design/formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)。  
  
## <a name="options"></a>選項。  
 **啟用刻度斷層**  
 選擇此選項讓圖表在必要時，繪製刻度斷層。 啟用此選項時，圖表會先自動計算資料集的高低點之間是否有足夠的差距，然後才繪製刻度斷層。  
  
 **相反方向**  
 選取這個選項來反轉圖表的方向。 例如，依預設，直條圖會在圖表左側顯示 Y 軸，而類別目錄由左至右顯示。 選取此選項時，圖表會在圖表右側顯示 Y 軸，而類別目錄由右至左顯示。  
  
 **使用交錯式色彩**  
 選取此選項可將帶狀線加入至圖表，然後選取色彩或輸入運算式。 帶狀線是圖表區域上有陰影的曲線，可以在格線之間提供明暗交錯之區域的效果。 這些帶狀線非常適合在軸上強調重複的圖樣。  
  
 **永遠包含零**  
 選取此選項即可在軸刻度上永遠包含零。 如果未啟用此選項，圖表將不會在軸上標示零值。 當資料集包含負值或零值時，包含零值相當實用。  
  
 **純量軸**  
 選取此選項即可在連續的刻度上顯示一組軸值。 例如，如果資料集包含 1 月、3 月和 11 月的資料，非純量軸只會顯示這些月份，而純量軸則會顯示一年的所有月份。  
  
 **使用對數刻度**  
 選取此選項可以表示軸刻度是對數。 只有在軸包含正數值時，Y 軸上才會提供這個選項。  
  
 在此方塊中，輸入在軸設定為使用對數刻度時所要使用的對數基底。 根據預設，圖表會針對軸的對數刻度，使用基底 10。 只有在軸為數值時，Y 軸上才會提供這個選項。  
  
 **至少**  
 輸入運算式或值當做 X 軸的最小值。 如果忽略此值，則最小值由資料集所傳回的資料決定。  
  
 **高**  
 輸入運算式或值當做 X 軸的最大值。 如果忽略此值，則最大值由資料集所傳回的資料決定。  
  
 **期間**  
 針對軸標籤之間的間隔輸入運算式或值。 例如，輸入 1，即可顯示軸上的每個類別目錄標籤。 輸入 2，即可每隔一個類別目錄標籤進行顯示。 如果忽略此值，系統就會自動根據資料集的值計算標籤。  
  
 **間隔類型**  
 輸入運算式或值當做指定之間隔的間隔類型。 例如，如果您希望間隔為兩天，您要將間隔指定為 [2]****，並將間隔類型指定為 [天]****。  
  
 **側邊界**  
 輸入運算式或選取值，即可在圖表元素和圖表側邊之間加入或移除邊界。 如果此選項設定為 [自動]****，則會加入側邊界。  
  
## <a name="see-also"></a>另請參閱  
 [格式化圖表上的軸標籤 &#40;報表產生器和 SSRS&#41;](report-design/formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
 [圖表 &#40;報表產生器和 SSRS&#41;](report-design/charts-report-builder-and-ssrs.md)   
 [格式化圖表上的數列色彩 &#40;報表產生器和 SSRS&#41;](report-design/formatting-series-colors-on-a-chart-report-builder-and-ssrs.md)   
 [指定報表產生器和 SSRS &#40;的軸間隔&#41;](report-design/specify-an-axis-interval-report-builder-and-ssrs.md)   
 [將軸標籤格式化為日期或貨幣 &#40;報表產生器和 SSRS&#41;](report-design/format-axis-labels-as-dates-or-currencies-report-builder-and-ssrs.md)   
 [在次要軸上繪製資料 &#40;報表產生器和 SSRS&#41;](report-design/plot-data-on-a-secondary-axis-report-builder-and-ssrs.md)   
 [走勢圖和資料橫條 &#40;報表產生器和 SSRS&#41;](report-design/sparklines-and-data-bars-report-builder-and-ssrs.md)   
 [加入或移除圖表中的邊界 &#40;報表產生器及 SSRS&#41;](report-design/add-or-remove-margins-from-a-chart-report-builder-and-ssrs.md)  
  
  
