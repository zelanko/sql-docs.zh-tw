---
title: 運算子優先順序與關聯性 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- associativity [Integration Services]
- precedence [Integration Services]
ms.assetid: 5094164f-dabc-45b5-b611-384feb2b3fe3
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 77f98e86a5ac4b03d4a21b0242a2324c61b2081a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62768814"
---
# <a name="operator-precedence-and-associativity"></a>運算子優先順序與關聯性
  在運算式評估工具支援的一組運算子中，每個運算子在優先順序階層中都有指定的優先順序，且包含評估的方向。 運算子的評估方向即為運算子關聯性。 具有較高優先順序的運算子會在低優先順序的運算子之前評估。 如果複雜的運算式有多個運算子時，運算子優先順序即決定運算子執行的順序。 執行的順序對結果值會有很大的影響。 某些運算子的優先順序相同。 如果運算式含有多個優先順序相同的運算子，則會按照左到右或右到左的方向評估運算子。  
  
 下表按高到低的順序列出運算子的優先順序。 同層級的運算子擁有相同的優先順序。  
  
|運算子符號|運算類型|關聯性|  
|---------------------|-----------------------|-------------------|  
|( )|運算是|由左至右|  
|-、!、~|一元 (Unary)|由右至左|  
|轉換|一元 (Unary)|由右至左|  
|*, / ,%|乘法|由左至右|  
|+、 -|加法|由左至右|  
|\<, >, \<=, >=|關聯式|由左至右|  
|==, !=|等式|由左至右|  
|&|位元 AND|由左至右|  
|^|位元排除 OR|由左至右|  
|&#124;|位元包含 OR|由左至右|  
|&&|邏輯 AND|由左至右|  
|&#124;&#124;|邏輯 OR|由左至右|  
|? 所解碼的字元：|條件運算式|由右至左|  
  
## <a name="see-also"></a>另請參閱  
 [運算子 &#40;SSIS 運算式&#41;](operators-ssis-expression.md)  
  
  
