---
title: "建立查詢 (MDX) 中的 Cube 內容 |Microsoft 文件"
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- cubes [Analysis Services], MDX
- MDX [Analysis Services], cube context
- SELECT statement [MDX]
- Multidimensional Expressions [Analysis Services], cube context
- queries [MDX], cube context
ms.assetid: 79d6a1e8-2825-4eb9-97df-5071aecae8f0
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 826945c3b044e76db93204fcd29afbe822c7e8a6
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="establishing-cube-context-in-a-query-mdx"></a>建立查詢中的 Cube 內容 (MDX)
  每個  MDX 查詢都會在指定的 Cube 內容內執行。 此內容定義在查詢內由運算式評估的成員。  
  
 在 SELECT 陳述式中，FROM 子句可決定 Cube 內容。 此內容可以是整個 Cube 或只是 Cube 的一個 Subcube。 透過 FROM 子句取得指定的 Cube 內容，您可以使用其他函數來擴充或限制內容。  
  
> [!NOTE]  
>  您也可以使用 SCOPE 與 CALCULATE 陳述式，管理 MDX 指令碼內的 Cube 內容。 如需詳細資訊，請參閱 [MDX 指令碼基礎觀念 &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-scripting-fundamentals-analysis-services.md)。  
  
## <a name="from-clause-syntax"></a>FROM 子句語法  
 以下語法描述 FROM 子句：  
  
```  
<SELECT subcube clause> ::=  
   Cube_Identifier |   
   (SELECT [  
      * |   
      ( <SELECT query axis clause> [ , <SELECT query axis clause> ... ] ) ]   
   FROM <SELECT subcube clause> <SELECT slicer axis clause> )  
```  
  
 請注意，在此語法中，描述執行 SELECT 陳述式所在的 Cube 或 Subcube 是 `<SELECT subcube clause>` 子句。  
  
 針對整個 Adventure Works 範例 Cube 執行的 FROM 子句，就是簡單的 FROM 子句範例。 這類 FROM 子句可有以下格式：  
  
```  
FROM [Adventure Works]  
```  
  
 如需 MDX SELECT 陳述式的 FROM 子句詳細資訊，請參閱 [SELECT 陳述式 &#40;MDX&#41;](../../../mdx/mdx-data-manipulation-select.md)。  
  
## <a name="refining-the-context"></a>精簡內容  
 雖然 FROM 子句如同在單一 Cube 內指定 Cube 內容，但您要一次處理多個 Cube 的資料不會受到限制。  
  
 您可以使用 MDX [LookupCube](../../../mdx/lookupcube-mdx.md) 函數來擷取 Cube 內容之外的 Cube 資料。 此外，例如可用的 [Filter](../../../mdx/filter-mdx.md) 函數，允許在評估查詢時暫時限制內容。  
  
## <a name="see-also"></a>請參閱＜  
 [MDX 查詢基礎觀念 &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)  
  
  

