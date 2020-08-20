---
description: '從 &lt; 模型選取 &gt; 。DIMENSION_CONTENT (DMX) '
title: 從 &lt; 模型選取 &gt; 。DIMENSION_CONTENT (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: e3d7bbfcce023ce994f71a5897a1cbf4b0095419
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471985"
---
# <a name="select-from-ltmodelgtdimension_content-dmx"></a>從 &lt; 模型選取 &gt; 。DIMENSION_CONTENT (DMX) 
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  採礦模型可用來做為 OLAP Cube 中的維度，而模型中的每個節點都代表該維度的成員。 **SELECT FROM \<model> 。Dimension_CONTENT** 語句會將其使用方式的相關模型內容傳回為維度。  
  
## <a name="syntax"></a>語法  
  
```  
  
SELECT [FLATTENED] [TOP <n>] <expression list> FROM <model>.Dimension_CONTENT   
[WHERE <condition expression>]  
[ORDER BY <expression> [DESC|ASC]]  
```  
  
## <a name="arguments"></a>引數  
 *n*  
 選擇性。 指定要傳回多少資料列的整數。  
  
 *運算式清單*  
 從內容結構描述資料列集衍生之相關資料行識別碼的逗號分隔清單。  
  
 *model*  
 模型識別碼。  
  
 *條件運算式*  
 選擇性。 限制從資料行清單傳回之值的條件。  
  
 *expression*  
 選擇性。 傳回純量值的運算式。  
  
## <a name="remarks"></a>備註  
 演算法提供者會定義傳回哪些內容，以及如何組織內容。 例如，提供者可能會限制維度內容中所描述的節點數目。  
  
 下表會列出可以查詢維度內容的資料行，以及每個資料行當成資料採礦維度執行的函數。  
  
|CONTENT 資料列集資料行|資料採礦維度中的函數|  
|---------------------------|---------------------------------------|  
|ATTRIBUTE_NAME|成員屬性。|  
|NODE_NAME|成員屬性。|  
|NODE_UNIQUE_NAME|索引鍵屬性。|  
|NODE_TYPE|成員屬性。|  
|NODE_CAPTION|索引 **鍵** 屬性的 CaptionColumn。|  
|CHILDREN_CARDINALITY|成員屬性。|  
|PARENT_UNIQUE_NAME|RelatedAttribute) 父子式階層中的索引 **鍵** 屬性 (ParentAttribute。|  
|NODE_DESCRIPTION|成員屬性。|  
|NODE_RULE|成員屬性。|  
|MARGINAL_RULE|成員屬性。|  
|NODE_PROBABILITY|成員屬性。|  
|MARGINAL_PROBABILITY|成員屬性。|  
|NODE_SUPPORT|成員屬性。|  
  
## <a name="examples"></a>範例  
  
### <a name="description"></a>描述  
 範例選取所有來自 `[TM Decision Tree]` 模型內容的資料行，其中均為使用模型作為維度的相關內容。  
  
### <a name="code"></a>程式碼  
  
```  
SELECT *   
FROM [TM Decision Tree].Dimension_Content  
```  
  
## <a name="see-also"></a>另請參閱  
 [選取 &#40;DMX&#41;](../dmx/select-dmx.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 資料定義語句](../dmx/dmx-statements-data-definition.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 資料動作陳述式](../dmx/dmx-statements-data-manipulation.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 陳述式參考](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
