---
title: "運算式 （報表產生器及 SSRS） 中的運算子 |Microsoft 文件"
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
ms.assetid: d22dc8b6-4353-40e7-91a1-65e8dae6325d
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 35e702d0d1944cd5e7f2b7120da07e272f30cf70
ms.contentlocale: zh-tw
ms.lasthandoff: 08/09/2017

---
# <a name="operators-in-expressions-report-builder-and-ssrs"></a>運算式中的運算子 (報表產生器及 SSRS)
  運算子是一個符號，代表套用至運算式中一個或多個詞彙的動作。 在運算式中支援下列的運算子類別：算術、比較、串連、邏輯或位元，以及位元移位。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="arithmetic"></a>算術  
 算術運算子會針對運算式中的兩個數值詞彙執行數學運算。  
  
|運算子|說明|  
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
  
|運算子|說明|  
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
  
|運算子|說明|  
|--------------|-----------------|  
|&|串連兩個字串|  
|+|串連兩個字串|  
  
### <a name="logical-and-bitwise"></a>邏輯和位元  
 邏輯和位元運算子會在運算式的兩個整數詞彙之間，執行邏輯操作。  
  
|運算子|說明|  
|--------------|-----------------|  
|And|對兩個布林運算式執行邏輯結合，或對兩個數值運算式 (Numeric Expression) 執行位元結合。|  
|Not|對布林運算式執行邏輯否定，或對數值運算式執行位元否定。|  
|或|對兩個布林運算式執行邏輯分離，或對兩個數值運算式執行位元分離。|  
|Xor|對兩個布林運算式執行邏輯互斥作業，或對兩個數值運算式執行位元互斥。|  
|AndAlso|對兩個運算式執行邏輯結合。|  
|OrElse|對兩個運算式執行邏輯分離。|  
  
### <a name="bit-shift"></a>位元位移  
 位元運算子會在運算式的兩個整數詞彙之間，執行位元操作。  
  
|運算子|說明|  
|--------------|-----------------|  
|<\<|執行位元模式的算術左移位。|  
|>>|執行位元模式的算術右移位。|  
  
## <a name="see-also"></a>請參閱＜  
 [運算式對話方塊](http://msdn.microsoft.com/library/e6c74ccb-4594-4d4f-b958-618d710e34eb)   
 [運算式 &#40;報表產生器及 SSRS &#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [運算式範例 &#40;報表產生器及 SSRS &#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [運算式 &#40; 中的資料類型報表產生器及 SSRS &#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [運算式對話方塊 &#40;報表產生器 &#41;](http://msdn.microsoft.com/library/e89c4d97-5d41-4b55-8695-79329edac15d)  
  
  

