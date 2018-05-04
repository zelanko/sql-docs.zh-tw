---
title: 交叉驗證報表中的量值 |Microsoft 文件
ms.custom: ''
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- root mean square error [data mining]
- cross-validation [data mining]
- mean absolute error [data mining]
- log score [data mining]
- likelihood [data mining]
ms.assetid: a07b1665-7f72-4266-82a4-43a91ae2571d
caps.latest.revision: 28
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 16431d09b0c505cf91a16ce00a09ed1d3a1f96ec
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="measures-in-the-cross-validation-report"></a>交叉驗證報表中的量值
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  在交叉驗證期間，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會將採礦結構中的資料分割成多個交叉區段，然後反覆地測試結構及任何相關聯的採礦模型。 根據這項分析，結果會輸出有關結構及每個模型的一組標準精確度量值。  
  
 此報表除了包含一些有關資料中的摺疊數以及每個摺疊中的資料量等基本資訊外，也包含一組描述資料分佈的一般標準。 藉由比較針對每個交叉區段的一般標準，您可以評估結構或模型的可靠性。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 也會顯示採礦模型的一組詳細量值。 這些量值會因模型類型及要分析的屬性類型而異：例如，其為離散或連續。  
  
 本節提供 [交叉驗證] 報表中含有的量值清單，及其代表的意義。 如需每個量值導出方式的詳細資訊，請參閱[交叉驗證公式](../../analysis-services/data-mining/cross-validation-formulas.md)。  
  
## <a name="list-of-measures-in-the-cross-validation-report"></a>交叉驗證報表中的量值清單  
 下表列出交叉驗證報表中顯示的量值清單。 這些量值會依「測試類型」分組，並顯示於下表左欄中。 左欄列出量值在報表中顯示的名稱，並簡短說明其代表的意義。  
  
|測試類型|量值和描述|  
|---------------|-------------------------------|  
|群集|套用至叢集模型的量值|  
||**案例可能性**：<br />                      此量值通常表示案例屬於特定群集的可能性。 針對交叉驗證，此分數會先加總，再除以案例數，即得到平均案例可能性的分數。|  
|分類|套用至分類模型的量值|  
||**真肯定**/**真否定**/**誤判**/**誤否定**：<br /><br /> 資料分割中的資料列或值計數，其中預測的狀態與目標狀態相符，而且預測機率大於指定的臨界值。<br /><br /> 不包括目標屬性擁有遺漏值的案例，亦即可能不會加總所有值的計數。|  
||**通過/失敗**：<br />                      資料分割中的資料列或值計數，其中預測的狀態與目標狀態相符，而且預測機率值大於 0。|  
|可能性|可能性量值可套用至多個模型類型。|  
||**增益**：<br />                      實際預測機率與測試案例中臨界機率的比率。 不包括目標屬性擁有遺漏值的資料列。<br /><br /> 此量值通常顯示在使用模型時目標結果之機率的改進程度。|  
||**均方根誤差**：<br />                      所有資料分割案例平均誤差的平方根，除以資料分割中的案例數目，不包括目標屬性擁有遺漏值的資料列。<br /><br /> RMSE 是常用的預測模型估計工具。 此分數會平均每個案例的餘數，得出模型誤差的單一指標。|  
||**對數分數**：<br />                      每一個案例之實際機率的對數，經過加總，然後除以輸入資料集中的資料列數目，不包括目標屬性擁有遺漏值的資料列。<br /><br /> 由於機率會以小數表示，因此對數分數永遠為負數。 越接近 0 的數字，表示越高的分數。 鑑於原始分數可能具有非常不尋常或偏斜的散發，對數分數會與百分比類似。|  
|估計|僅套用至估計模型的量值，可預測連續數值屬性。|  
||**均方根誤差**：<br />                      預測值與實際值相較下的平均誤差。<br /><br /> RMSE 是常用的預測模型估計工具。 此分數會平均每個案例的餘數，得出模型誤差的單一指標。|  
||**平均絕對誤差**：<br />                      預測值與實際值相較下的平均誤差，以誤差絕對總和的平均數來計算。<br /><br /> 平均絕對誤差有助於了解整體預測與實際值之間的差距。 分數愈小，表示預測愈精準。|  
||**對數分數**：<br />                      每一個案例之實際機率的對數，經過加總，然後除以輸入資料集中的資料列數目，不包括目標屬性擁有遺漏值的資料列。<br /><br /> 由於機率會以小數表示，因此對數分數永遠為負數。 越接近 0 的數字，表示越高的分數。 鑑於原始分數可能具有非常不尋常或偏斜的散發，對數分數會與百分比類似。|  
|彙總|彙總量值以每個資料分割的結果提供變異數的指示。|  
||**平均數**：<br />                      特定量值的資料分割值的平均值。|  
||**標準差**：<br />                      在模型的所有資料分割中，與特定量值平均數的差異平均值。<br /><br /> 針對交叉驗證，此分數的值愈高意味著摺疊數之間會有顯著的變化。|  
  
## <a name="see-also"></a>另請參閱  
 [測試和驗證 &#40;資料採礦&#41;](../../analysis-services/data-mining/testing-and-validation-data-mining.md)  
  
  
