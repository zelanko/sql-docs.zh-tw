---
title: "SELECT FROM&lt;模型&gt;。DIMENSION_CONTENT (DMX) |Microsoft 文件"
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
f1_keywords:
- SELECT
- FROM
- DIMENSION_CONTENT
dev_langs:
- DMX
helpviewer_keywords:
- mining models [Analysis Services], dimension content
- SELECT FROM <model>.DIMENSION_CONTENT statement
ms.assetid: 907fb3fb-2131-4a10-8635-2a39b9a805aa
caps.latest.revision: 42
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: f9caf83d8d3d151f1b324f00abf5561549e111ad
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="select-from-ltmodelgtdimensioncontent-dmx"></a>SELECT FROM&lt;模型&gt;。DIMENSION_CONTENT (DMX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  採礦模型可用來做為 OLAP Cube 中的維度，而模型中的每個節點都代表該維度的成員。 **SELECT FROM\<模型 >。Dimension_CONTENT**陳述式會傳回模型的維度做為相關的內容。  
  
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
|NODE_CAPTION|CaptionColumn**金鑰**屬性。|  
|CHILDREN_CARDINALITY|成員屬性。|  
|PARENT_UNIQUE_NAME|屬性的 RelatedAttribute**金鑰**屬性 (父子式階層中的 ParentAttribute)。|  
|NODE_DESCRIPTION|成員屬性。|  
|NODE_RULE|成員屬性。|  
|MARGINAL_RULE|成員屬性。|  
|NODE_PROBABILITY|成員屬性。|  
|MARGINAL_PROBABILITY|成員屬性。|  
|NODE_SUPPORT|成員屬性。|  
  
## <a name="examples"></a>範例  
  
### <a name="description"></a>Description  
 範例選取所有來自 `[TM Decision Tree]` 模型內容的資料行，其中均為使用模型作為維度的相關內容。  
  
### <a name="code"></a>程式碼  
  
```  
SELECT *   
FROM [TM Decision Tree].Dimension_Content  
```  
  
## <a name="see-also"></a>另請參閱  
 [SELECT &#40; DMX &#41;](../dmx/select-dmx.md)   
 [資料採礦延伸模組 &#40; DMX &#41;資料定義陳述式](../dmx/dmx-statements-data-definition.md)   
 [資料採礦延伸模組 &#40; DMX &#41;資料操作陳述式](../dmx/dmx-statements-data-manipulation.md)   
 [資料採礦延伸模組 &#40; DMX &#41;陳述式參考](../dmx/data-mining-extensions-dmx-statements.md)  
  
  

