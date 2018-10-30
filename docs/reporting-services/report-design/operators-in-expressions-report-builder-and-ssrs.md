---
title: 運算式中的運算子 (報表產生器及 SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: d22dc8b6-4353-40e7-91a1-65e8dae6325d
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 870792045a0281461362262fe81a831644ac06dd
ms.sourcegitcommit: 3daacc4198918d33179f595ba7cd4ccb2a13b3c0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/25/2018
ms.locfileid: "50021132"
---
# <a name="operators-in-expressions-report-builder-and-ssrs"></a>運算式中的運算子 (報表產生器及 SSRS)
  運算子是一個符號，代表套用至運算式中一個或多個詞彙的動作。 在運算式中支援下列的運算子類別：算術、比較、串連、邏輯或位元，以及位元移位。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="arithmetic"></a>算術  
 算術運算子會針對運算式中的兩個數值詞彙執行數學運算。  
  
|運算子|Description|  
|--------------|-----------------|  
|^|將一數值對另一數值做乘冪運算。|  
|*|兩個數目相乘。|  
|/|兩數相除並傳回浮點結果。|  
|\|兩數相除並傳回整數結果。|  
|Mod|傳回除法的整數餘數。 例如，7 Mod 5 = 2，因為 7 除以 5 的餘數是 2。|  
|+|將兩個數目相加。|  
|-|傳回兩個數值運算式之間的差異，或指出數值詞彙的負值。|  
  
### <a name="comparison"></a>比較  
 比較運算子用來測試兩個運算式是否相同。  
  
|運算子|Description|  
|--------------|-----------------|  
|<|小於。|  
|\<=|小於或等於。|  
|>|大於。|  
|>=|大於或等於。|  
|=|等於。|  
|<>|不等於。|  
|相似|判斷特定字元字串是否符合指定的模式。 模式中可以包含一般字元及萬用字元。 在模式比對期間，一般字元必須與字元字串中所指定的字元完全相符。 不過，萬用字元可以符合任意字元字串片段。 使用萬用字元要比使用 = 與 != 字串比較運算子能讓 LIKE 運算子更有彈性。<br /><br /> 下列表格列出可用來當做萬用字元的字元。<br /><br /> %：任何含有零或多個字元的字串。<br /><br /> _：任何單一字元。<br /><br /> [ ]：指定範圍中的任何單一字元 (例如 [a-f]) 或集合 (例如 [aeiou])。<br /><br /> [^]：不在指定範圍中的任何單一字元 (例如 [^a - f]) 或集合 (例如 [^aeiou])。|  
|Is|比較兩個物件參考。|  
  
### <a name="string-concatenation"></a>字串串連  
 字串串連會在運算式中將第二個字串附加至第一個字串。 如果要進行其他字串作業，請使用內建的函數。  
  
|運算子|Description|  
|--------------|-----------------|  
|&|串連兩個字串|  
|+|串連兩個字串|  
  
### <a name="logical-and-bitwise"></a>邏輯和位元  
 邏輯和位元運算子會在運算式的兩個整數詞彙之間，執行邏輯操作。  
  
|運算子|Description|  
|--------------|-----------------|  
|And|對兩個布林運算式執行邏輯結合，或對兩個數值運算式 (Numeric Expression) 執行位元結合。|  
|Not|對布林運算式執行邏輯否定，或對數值運算式執行位元否定。|  
|或|對兩個布林運算式執行邏輯分離，或對兩個數值運算式執行位元分離。|  
|Xor|對兩個布林運算式執行邏輯互斥作業，或對兩個數值運算式執行位元互斥。|  
|AndAlso|對兩個運算式執行邏輯結合。|  
|OrElse|對兩個運算式執行邏輯分離。|  
  
### <a name="bit-shift"></a>位元位移  
 位元運算子會在運算式的兩個整數詞彙之間，執行位元操作。  
  
|運算子|Description|  
|--------------|-----------------|  
|<\<|執行位元模式的算術左移位。|  
|>>|執行位元模式的算術右移位。|  
  
## <a name="see-also"></a>另請參閱  
 [運算式對話方塊](https://msdn.microsoft.com/library/e6c74ccb-4594-4d4f-b958-618d710e34eb)   
 [運算式 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [運算式範例 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [運算式中的資料類型 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [運算式對話方塊 &#40;報表產生器&#41;](https://msdn.microsoft.com/library/e89c4d97-5d41-4b55-8695-79329edac15d)  
  
  
