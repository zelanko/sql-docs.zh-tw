---
title: 使用成員屬性 (MDX) |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7876031fddb74115fd1fe412f4c8a9d9aacdb054
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62740238"
---
# <a name="mdx-member-properties"></a>MDX 成員屬性
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  成員屬性包含每個 Tuple 中每個成員的基本資訊。 此基本資訊包括成員名稱、父層級、子系數目等等。 指定層級上的所有成員都能使用成員屬性。 就組織而言，會將成員屬性視為儲存在單一維度上，且以維度方式組織的資料。  
  
> [!NOTE]
>  在 [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]中，成員屬性稱為屬性關聯性。 如需詳細資訊，請參閱 [屬性關聯性](../../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md)。  
  
 成員屬性不是 *「內建」* 就是 *「自訂」*：  
  
 內建成員屬性  
 當維度與層級提供其他內建維度與層級成員屬性 (如成員識別碼) 時，所有成員都會支援內建成員屬性 (例如，格式化的成員值)。  
  
 如需詳細資訊，請參閱[內建成員屬性 &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-member-properties-intrinsic-member-properties.md)。  
  
 使用者自訂成員屬性  
 成員通常會擁有與之相關的其他屬性。 例如，Products 層級可能會為每項產品提供 SKU、SRP、Weight 與 Volume 屬性。 這些屬性不是成員，但包含了有關 Products 層級上成員的其他資訊。  
  
 如需詳細資訊，請參閱[使用者自訂成員屬性 &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-member-properties-user-defined-member-properties.md)。  
  
 使用 **PROPERTIES** 關鍵字或 [Properties](../../../mdx/properties-mdx.md) 函數，就可以擷取內建與使用者自訂的成員屬性。  
  
## <a name="using-the-properties-keyword"></a>使用 PROPERTIES 關鍵字  
 **PROPERTIES** 關鍵字可以指定成員屬性，以供指定的座標軸維度使用。 **PROPERTIES** 關鍵字內嵌在 MDX `<axis specification>` SELECT [陳述式的](../../../mdx/mdx-data-manipulation-select.md) 子句中：  
  
```  
SELECT [<axis_specification>  
       [, <axis_specification>...]]  
  FROM [<cube_specification>]  
[WHERE [<slicer_specification>]]  
```  
  
 `<axis_specification>` 子句包含一個選擇性的 `<dim_props>` 子句，如以下語法所示：  
  
```  
<axis_specification> ::= <set> [<dim_props>] ON <axis_name>  
```  
  
> [!NOTE]  
>  如需 `<set>` 和 `<axis_name>` 值的詳細資訊，請參閱[指定查詢座標軸的內容 &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-specify-the-contents-of-a-query-axis.md)。  
  
 `<dim_props>` 子句可讓您使用 **PROPERTIES** 關鍵字，查詢維度、層級與成員屬性。 以下語法顯示 `<dim_props>` 子句的格式：  
  
```  
<dim_props> ::= [DIMENSION] PROPERTIES <property> [,<property>...]  
```  
  
 `<property>` 語法的解析會依據您查詢的屬性而有所不同：  
  
-   可區分內容的內建成員屬性，必須在前面加上維度或層級的名稱。 但是，不區分內容的內建成員屬性，就無法以維度或層級名稱來限定。 如需如何使用 **PROPERTIES** 關鍵字搭配內建成員屬性的詳細資訊，請參閱[內建成員屬性 &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-member-properties-intrinsic-member-properties.md)。  
  
-   使用者自訂成員屬性應該在前面加上所屬層級的名稱。 如需如何使用 **PROPERTIES** 關鍵字搭配使用者定義成員屬性的詳細資訊，請參閱[使用者自訂成員屬性 &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-member-properties-user-defined-member-properties.md)。  
  
## <a name="see-also"></a>另請參閱  
 [建立和使用屬性值 &#40;MDX&#41;](http://msdn.microsoft.com/library/0cafb269-03c8-4183-b6e9-220f071e4ef2)  
  
  
