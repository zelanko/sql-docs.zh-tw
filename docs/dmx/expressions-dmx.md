---
title: "運算式 (DMX) |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- DMX
helpviewer_keywords:
- Data Mining Extensions [Analysis Services], expressions
- DMX [Analysis Services], expressions
- expressions [DMX]
ms.assetid: 00579552-19c8-4e9d-a790-f88df3e1aeea
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: c04c55fc461d4429d55d32a776f5bea8eca345e8
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="expressions-dmx"></a>運算式 (DMX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  在資料採礦延伸模組 (DMX)，運算式是識別碼、 數值與運算子的組合， [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]可以評估而取得結果。  
  
 DMX 運算式可能很簡單或很複雜。 簡單運算式可以是下列項目之一：  
  
 常數  
 常數是代表單一特定值的符號。 常數可以是字串，或者數值或日期值。 您必須使用單引號 (') 來分隔字串與日期常數。  
  
 純量函數  
 純量函數會傳回單一值。  
  
 非純量函數  
 非純量函數會傳回資料表。  
  
 物件識別碼  
 物件識別碼在 DMX 中視為簡單運算式。  
  
 若要建立複雜運算式，可以使用運算子結合這些運算式。 如需有關運算子的詳細資訊，請參閱[資料採礦延伸模組 &#40; DMX &#41;運算子參考](../dmx/data-mining-extensions-dmx-operator-reference.md)。  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦延伸模組 &#40; DMX &#41;參考](../dmx/data-mining-extensions-dmx-reference.md)   
 [資料採礦延伸模組 &#40; DMX &#41;函數參考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [資料採礦延伸模組 &#40; DMX &#41;陳述式參考](../dmx/data-mining-extensions-dmx-statements.md)   
 [資料採礦延伸模組 &#40; DMX &#41;語法慣例](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [資料採礦延伸模組 &#40; DMX &#41;語法元素](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [一般預測函數 &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)   
 [結構和使用方式的 DMX 預測查詢](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [了解 DMX Select 陳述式](../dmx/understanding-the-dmx-select-statement.md)  
  
  

