---
title: 定義自訂成員公式 |Microsoft 文件
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
- members [Analysis Services], custom
- custom rollup formulas [Analysis Services]
- MDX [Analysis Services], custom rollup formulas
- custom member formulas [Analysis Services]
ms.assetid: 258304e2-d900-4013-97e3-871f51dfdce2
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 2983c826b96f681971a6c1fc5be56084a8213453
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36035093"
---
# <a name="define-custom-member-formulas"></a>定義自訂成員公式
  您可以定義多維度運算式 (MDX) 運算式 (稱為自訂成員公式)，來提供所指定屬性之成員的值。 來自資料來源檢視之資料表中的資料行，為屬性的每一個成員提供該運算式，來提供該成員的值。  
  
 自訂成員公式決定與成員相關聯的資料格值，並覆寫量值的彙總函式。 自訂成員公式是用 MDX 撰寫。 每個自訂成員公式適用於單一成員。 自訂成員公式會儲存在維度資料表中，或者儲存在與維度資料表有外部索引鍵關聯性的另一個資料表中。  
  
 屬性 (Attribute) 上的 `CustomRollupColumn` 屬性 (Property) 指定含有屬性 (Attribute) 成員之自訂成員公式的資料行。 如果資料行中的資料列是空的，則會正常傳回成員的資料格值。 如果資料行中的公式無效，則只要擷取使用成員的資料格值時，就會發生執行階段錯誤。  
  
 在為屬性指定自訂成員公式之前，請確認包含該屬性的維度資料表，或直接相關的資料表中有字串資料行可儲存自訂成員公式。 如果這種情況，您可以設定`CustomRollupColumn`屬性上的屬性以手動方式或使用商業智慧精靈的設定自訂成員公式增強功能啟用自訂成員公式的屬性上。 如需如何使用這項增強功能的詳細資訊，請參閱 [在維度中設定屬性的自訂成員公式](bi-wizard-custom-member-formulas-for-attributes-in-a-dimension.md)。  
  
## <a name="evaluating-custom-member-formulas"></a>評估自訂成員公式  
 自訂成員公式與導出成員不同。 自訂成員公式是套用至維度資料表中的成員，並只提供成員的值。 相反地，導出成員不是儲存在維度資料表中，而導出成員運算式會定義維度或階層所含之其他成員的資料和中繼資料。  
  
 自訂成員公式覆寫與量值相關聯的彙總函式。 例如，在指定自訂成員公式之前，使用 `Sum` 彙總函式的量值含有 Time 維度下列成員的下列值：  
  
-   2003: 2100  
  
    -   第 1 季：700  
  
    -   第 2 季：500  
  
    -   第 3 季：100  
  
    -   第 4 季：800  
  
-   2004: 1500  
  
    -   第 1 季：600  
  
    -   第 2 季：200  
  
    -   第 3 季：300  
  
    -   第 4 季：400  
  
 利用自訂成員公式，成員的值將改由自訂積存公式提供。 例如，可使用以下自訂成員公式，提供 Time 維度之 2004 成員 Quarter 4 子成員的值 450。  
  
```  
Time.[Quarter 3] * 1.5  
```  
  
 自訂成員公式儲存在維度資料表的一個資料行中。 藉由設定啟用自訂積存公式`CustomRollupColumn`屬性上的屬性。  
  
 若要將單一 MDX 運算式套用至屬性的所有成員，請在維度資料表上建立具名計算，以常值字串傳回 MDX 運算式。 然後，以您要設定之屬性上的 `CustomRollupColumn` 屬性設定，來指定具名計算。 具名計算是資料來源檢視資料表中的一個資料行，它傳回 SQL 運算式所定義的資料列值。 如需建構具名計算的詳細資訊，請參閱[在資料來源檢視中定義具名計算 &#40;Analysis Services&#41;](define-named-calculations-in-a-data-source-view-analysis-services.md)  
  
> [!NOTE]  
>  若要將 MDX 運算式套用至特定層級的成員，而非以特定屬性為基礎之所有層級的成員，則可將運算式定義為層級上的 MDX 指令碼。 如需詳細資訊，請參閱 [MDX 指令碼基礎觀念 &#40;Analysis Services&#41;](mdx/mdx-scripting-fundamentals-analysis-services.md)。  
  
 如果您對屬性的成員同時使用導出成員和自訂積存公式，則必須知道評估順序。 導出成員是在解析自訂積存公式之前解析。  
  
## <a name="see-also"></a>另請參閱  
 [屬性和屬性階層](../multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)   
 [在維度中設定屬性的自訂成員公式](bi-wizard-custom-member-formulas-for-attributes-in-a-dimension.md)  
  
  