---
title: 使用元組運算式 |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 55b55f2104e900104c051021fc02761d32c63e5e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68135127"
---
# <a name="using-tuple-expressions"></a>使用 Tuple 運算式


  Tuple 是由 Cube 內所含各維度的一個成員所組成。 因此，Tuple 可以唯一識別 Cube 內的單一資料格。  
  
> [!NOTE]  
>  參考一個或多個成員的無效 Tuple，稱為空白 Tuple。  
  
 Tuple 識別碼的完整運算式是由一個或多個明確指定的成員所組成 (嵌在括號中)：  
  
 （*Member_expression* [，*Member_expression* ...]）  
  
 Tuple 可以是完整 Tuple、可以包含隱含成員，或也可以包含單一成員。  
  
## <a name="tuples-and-implicit-members"></a>Tuple 與隱含成員  
 可從 Cube 內包含的每個維度明確指定單一成員的 Tuple，稱為完整 Tuple。 但是，Tuple 不需要是完整 Tuple。  
  
 在 Tuple 內未明確參考的任何維度，則為隱含地參考。 隱含參考之維度的成員取決於維度的結構以及其中定義的屬性關聯性而定。 如果與隱含參考之階層相同的維度上有階層的明確參考，而且明確參考的階層與隱含參考的階層之間有定義直接或間接關聯性，則 tuple 的行為就像是它包含隱含參考之階層上的成員，而該成員與明確參考之階層上的成員一起存在。 例如，如果 cube 包含具有 City 和 Country 屬性的 Customer 維度，而且這兩個屬性之間有定義關聯性，好讓 City 具有一個 Country 而且一個 Country 可包含許多 City，則明確將 City 'London' 包含在 tuple 內會隱含地參考 Country 'United Kingdom'。 但是，如果未定義任何屬性關聯性、此關聯性是相反的方向 (例如，雖然 City 可能與 Country 之間有關聯性，但是您無法從某個人居住的 Country 來判斷他所在的 City)，或者兩個定義的屬性之間沒有直接關聯性 (從 Customer 到 City 之間以及 Customer 到 Country 之間可能有定義關聯性，但是 City 與 Country 之間沒有定義關聯性)，則適用以下規則：  
  
-   如果隱含參考的階層有預設成員，則會將該預設成員加入 Tuple。  
  
-   如果隱含參考的階層沒有預設成員，則會使用預設階層的 **（全部）** 成員。  
  
-   如果隱含參考的階層沒有預設成員，就會使用此階層之最高層級的第一個成員。  
  
## <a name="one-member-tuples"></a>單一成員 Tuple  
 如果 Tuple 運算式有單一成員，MDX 會將該成員轉換成單一成員 Tuple，以供評估運算式之用。 換句話說，提供成員運算式 `[Measures].[TestMeasure]` (而非 Tuple 運算式)，在功能上相當於 Tuple 運算式 `( [Measures].[TestMeasure] ).`  
  
## <a name="see-also"></a>另請參閱  
 [MDX&#41;&#40;的運算式](../mdx/expressions-mdx.md)   
 [Mdx 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
