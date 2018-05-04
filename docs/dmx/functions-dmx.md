---
title: 函式 (DMX) |Microsoft 文件
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- DMX
helpviewer_keywords:
- DMX [Analysis Services], functions
- VBA [DMX]
- stored procedures [DMX]
- functions [DMX]
- Excel [DMX]
- Data Mining Extensions [Analysis Services], functions
ms.assetid: 75ab6346-f4a4-4699-90f3-66d35f930ed7
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: ba4f13bed63954643e6678ca4210400cb91c3b98
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="functions-dmx"></a>函數 (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  當您使用資料採礦延伸模組 (DMX) 中的查詢物件[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，您可以使用函式中的資料採礦模型或輸入資料集的資料行中傳回比只值的詳細資訊。 例如，您可以使用 DMX 查詢傳回資料行的預測值之外，還可以傳回預測正確的機率。 您不只能使用 DMX 函數，也可以使用 Microsoft Visual Basic for Applications (VBA)、Microsoft Excel 與預存程序的函數。  
  
## <a name="dmx-functions"></a>DMX 函數  
 您可以使用 DMX 函數執行下列工作：  
  
-   傳回預測。  
  
-   傳回預測的相關統計資料，例如機率與支援。  
  
-   篩選您的查詢結果。  
  
-   重新排序資料表運算式。  
  
 大多數的 DMX 函數會傳回純量值，例如預測的支援，不過有些會傳回表格式結果。 例如，PredictHistogram 函數傳回的資料表，其中包含支援與指定之可預測資料行的每個狀態的機率。 結果會顯示為新的表格式資料行。  
  
 **如需詳細資訊：** [一般預測函數&#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)，[資料採礦延伸模組&#40;DMX&#41;函數參考](../dmx/data-mining-extensions-dmx-function-reference.md)  
  
## <a name="visual-basic-for-applications-vba-and-excel-functions"></a>Visual Basic for Applications (VBA) 與 Excel 函數  
 除了 DMX 函數以外，您還可以從 DMX 陳述式呼叫各種的 VBA 與 Excel 函數。 例如，您可以使用 lCase 函數修改 TM_Decision_Tree 模型內容中的則 Attribute_Name 資料行的顯示方式。 情形如下列的程式碼範例所示。  
  
```  
SELECT lCase([Attribute_Name])   
FROM [TM_Decision_Tree].CONTENT  
```  
  
 如果 VBA 與 Excel 中，有相同的函式，您必須在 DMX 陳述式中使用的首碼函式名稱**VBA**或**Excel**。 例如，您可以使用 `VBA!Log` 或 `Excel!Log`。 如果 DMX 或多維度運算式 (MDX) 中也有您想要使用的 VBA 或 Excel 函數，或者函數若包含錢幣符號字元 ($)，您就必須使用方括號 ([]) 來逸出函數。 例如，函數呼叫可能是 `[VBA!Format]`。  
  
## <a name="stored-procedures"></a>預存程序  
 您可以使用 Common Language Runtime 程式設計語言建立擴充 DMX 功能的預存程序。 比方說，迴歸樹採礦模型傳回係數，如 A、 B、 等等，描述迴歸方程式，但此模型不會傳回方程式本身，例如 A + Bx = y。 不過，您可以撰寫使用資料庫採礦模型物件導覽內容結構描述，以及將迴歸方程式當成輸出傳回的預存程序。 因此，DMX 陳述式可以傳回迴歸方程式的清單作為查詢結果的一部份。  
  
 **如需詳細資訊：** [多維度模型組件管理](../analysis-services/multidimensional-models/multidimensional-model-assemblies-management.md)  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦延伸模組 & #40; DMX & #41;參考](../dmx/data-mining-extensions-dmx-reference.md)   
 [資料採礦延伸模組&#40;DMX&#41;函數參考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [資料採礦延伸模組&#40;DMX&#41;運算子參考](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [資料採礦延伸模組 & #40; DMX & #41;陳述式參考](../dmx/data-mining-extensions-dmx-statements.md)   
 [資料採礦延伸模組&#40;DMX&#41;語法慣例](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [資料採礦延伸模組&#40;DMX&#41;語法元素](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [一般預測函數&#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [結構和使用方式的 DMX 預測查詢](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [了解 DMX Select 陳述式](../dmx/understanding-the-dmx-select-statement.md)  
  
  
