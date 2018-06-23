---
title: 交叉驗證報表中的量值 |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- root mean square error [data mining]
- cross-validation [data mining]
- mean absolute error [data mining]
- log score [data mining]
- likelihood [data mining]
ms.assetid: a07b1665-7f72-4266-82a4-43a91ae2571d
caps.latest.revision: 27
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: bedc8656248ced7c8f25b0868804e36ad410d642
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36037146"
---
# <a name="measures-in-the-cross-validation-report"></a>交叉驗證報表中的量值
  在交叉驗證期間， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會將採礦結構中的資料分割成多個交叉區段，然後反覆地測試結構及任何相關聯的採礦模型。 根據這項分析，結果會輸出有關結構及每個模型的一組標準精確度量值。  
  
 此報表除了包含一些有關資料中的摺疊數以及每個摺疊中的資料量等基本資訊外，也包含一組描述資料分佈的一般標準。 藉由比較針對每個交叉區段的一般標準，您可以評估結構或模型的可靠性。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 也會顯示採礦模型的一組詳細量值。 這些量值會因模型類型及要分析的屬性類型而異：例如，其為離散或連續。  
  
 本節提供 [交叉驗證] 報表中含有的量值清單，及其代表的意義。 如需每個量值導出方式的詳細資訊，請參閱[交叉驗證公式](cross-validation-formulas.md)。  
  
## <a name="list-of-measures-in-the-cross-validation-report"></a>交叉驗證報表中的量值清單  
 下表列出交叉驗證報表中顯示的量值清單。 這些量值會依「測試類型」分組，並顯示於下表左欄中。 左欄列出量值在報表中顯示的名稱，並簡短說明其代表的意義。  
  
|測試類型|量值和描述|  
|---------------|-------------------------------|  
|群集|套用至群集模型的量值：<br /><br /> **案例可能性**： 此量值通常表示可能的案例屬於特定叢集。 <br />                      針對交叉驗證，此分數會先加總，再除以案例數，即得到平均案例可能性的分數。|  
|分類|套用至分類模型的量值：<br /><br /> **真肯定**/<br />                      **True 負數**/ **False Positive**/ **False Positive**： 其中預測的狀態與目標狀態相符，資料分割中的資料列或值的計數和預測機率大於指定的臨界值。 已排除擁有遺漏值的目標屬性的情況下，這表示所有值的計數可能不會加總|  
||**通過/失敗**： 計算的資料列或資料分割中的值，其中預測的狀態與目標狀態相符，而且預測機率值大於 0。|  
|可能性|可能性量值適用於多種模型類型：<br /><br /> **提起**： 實際預測機率與測試案例中臨界機率的比率。 不包括目標屬性擁有遺漏值的資料列。 此量值通常顯示在使用模型時目標結果之機率的改進程度。<br /><br /> **均方根誤差**： 所有的資料分割案例平均誤差的平方根除以資料分割，不包括擁有遺漏值的目標屬性的資料列中的案例數目。 RMSE 是常用的預測模型估計工具。 此分數會平均每個案例的餘數，得出模型誤差的單一指標。<br /><br /> **對數分數**： 為每個案例中，實際的機率的對數加總，，然後除以輸入資料集，不包括擁有遺漏值的目標屬性的資料列中的資料列數目。 由於機率會以小數表示，因此對數分數永遠為負數。 越接近 0 的數字，表示越高的分數。 鑑於原始分數可能具有非常不尋常或偏斜的散發，對數分數會與百分比類似。|  
|估計|量值僅套用至估計模型，預測連續的數值屬性：<br /><br /> **均方根誤差**： 預測的值與實際值相較下的平均誤差。 RMSE 是常用的預測模型估計工具。 此分數會平均每個案例的餘數，得出模型誤差的單一指標。<br /><br /> **平均絕對誤差**： 比較實際的值，以誤差絕對總和的計算預測的值的平均誤差。 平均絕對誤差有助於了解整體預測與實際值之間的差距。 分數愈小，表示預測愈精準。<br /><br /> **對數分數**： 為每個案例中，實際的機率的對數加總，，然後除以輸入資料集，不包括擁有遺漏值的目標屬性的資料列中的資料列數目。 由於機率會以小數表示，因此對數分數永遠為負數。 越接近 0 的數字，表示越高的分數。 鑑於原始分數可能具有非常不尋常或偏斜的散發，對數分數會與百分比類似。|  
|彙總|彙總的量值會提供每個資料分割的結果中的變異數的指示：<br /><br /> **表示**： 特定量值的值的資料分割的平均值。<br /><br /> **標準差**： 平均模型中的所有資料分割與特定量值平均數的差異。 針對交叉驗證，此分數的值愈高意味著摺疊數之間會有顯著的變化。|  
  
## <a name="see-also"></a>另請參閱  
 [測試和驗證&#40;資料採礦&#41;](testing-and-validation-data-mining.md)  
  
  