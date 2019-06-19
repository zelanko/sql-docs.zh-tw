---
title: 圖表類型 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10423"
ms.assetid: 57b00017-69ae-4e71-8d78-44744e208ac7
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e4c71d67b215732eae6e94af1d0c92d9231f4a01
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66106271"
---
# <a name="chart-types-report-builder-and-ssrs"></a>圖表類型 (報表產生器及 SSRS)
  針對您要呈現的資料類型選擇適當的圖表類型相當重要。 因為這可以決定以圖表形式放入資料時可以解譯資料的程度。 例如，如果您的資料集包含多個相對於圖表大小的資料點，最好使用區域、線條或散佈圖呈現。 如需如何根據選取的圖表類型準備資料的相關討論，請參閱 [圖表 &#40;報表產生器及 SSRS&#41;](charts-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="choosing-a-chart-type"></a>選擇圖表類型  
 每個圖表類型都有獨特的特性，可協助您將資料集視覺化。 您可以使用任何圖表類型來顯示資料，但是，根據您嘗試要在報表中顯示的項目使用適合您資料的圖表類型時，將會更容易讀取資料。 下表摘要說明影響特定資料集之圖表適合度的圖表功能。  
  
 您可以在建立圖表類型之後再加以變更。 如需詳細資訊，請參閱[變更圖表類型 &#40;報表產生器及 SSRS&#41;](change-a-chart-type-report-builder-and-ssrs.md)。  
  
 其中許多圖表類型的範例可從範例報表取得。 如需有關下載範例報表的詳細資訊，請參閱 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][報表產生器與報表設計師範例報表](https://go.microsoft.com/fwlink/?LinkId=198283)。  
  
|圖表類型|顯示比例資料|顯示庫存資料|顯示線性資料|顯示多重值資料|  
|----------------|------------------------|------------------------|-------------------------|-------------------------------|  
|[區域圖 &#40;報表產生器及 SSRS&#41;](area-charts-report-builder-and-ssrs.md)|||![可用](../media/greencheck.gif "可用")||  
|[橫條圖 &#40;報表產生器及 SSRS&#41;](bar-charts-report-builder-and-ssrs.md)|||![可用](../media/greencheck.gif "可用")||  
|[資料橫條](sparklines-and-data-bars-report-builder-and-ssrs.md)|||![可用](../media/greencheck.gif "可用")||  
|[直條圖 &#40;報表產生器及 SSRS&#41;](column-charts-report-builder-and-ssrs.md)|||![可用](../media/greencheck.gif "可用")||  
|[折線圖 &#40;報表產生器及 SSRS&#41;](line-charts-report-builder-and-ssrs.md)|||![可用](../media/greencheck.gif "可用")||  
|[圓形圖 &#40;報表產生器及 SSRS&#41;](pie-charts-report-builder-and-ssrs.md)|![可用](../media/greencheck.gif "可用")||||  
|[極座標圖 &#40;報表產生器及 SSRS&#41;](polar-charts-report-builder-and-ssrs.md)|![可用](../media/greencheck.gif "可用")||||  
|[範圍圖表 &#40;報表產生器及 SSRS&#41;](range-charts-report-builder-and-ssrs.md)|||![可用](../media/greencheck.gif "可用")|![可用](../media/greencheck.gif "可用")|  
|[散佈圖 &#40;報表產生器及 SSRS&#41;](scatter-charts-report-builder-and-ssrs.md)|![可用](../media/greencheck.gif "可用")||![可用](../media/greencheck.gif "可用")||  
|[形狀圖 &#40;報表產生器及 SSRS&#41;](shape-charts-report-builder-and-ssrs.md)|![可用](../media/greencheck.gif "可用")||||  
|[走勢圖](sparklines-and-data-bars-report-builder-and-ssrs.md)|![可用](../media/greencheck.gif "可用")|![可用](../media/greencheck.gif "可用")|![可用](../media/greencheck.gif "可用")|![可用](../media/greencheck.gif "可用")|  
|[股票圖 &#40;報表產生器及 SSRS&#41;](stock-charts-report-builder-and-ssrs.md)||![可用](../media/greencheck.gif "可用")||![可用](../media/greencheck.gif "可用")|  
  
## <a name="see-also"></a>另請參閱  
 [圖表 &#40;報表產生器及 SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [圖表中的空白和 Null 資料點 &#40;報表產生器及 SSRS&#41;](empty-and-null-data-points-in-charts-report-builder-and-ssrs.md)   
 [將圖表加入至報表 &#40;報表產生器及 SSRS&#41;](add-a-chart-to-a-report-report-builder-and-ssrs.md)  
  
  
