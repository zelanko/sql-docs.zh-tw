---
title: "子系 (MDX) |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CHILDREN
dev_langs:
- kbMDX
helpviewer_keywords:
- Children function
ms.assetid: ce2c3069-914c-44a3-8a4c-5cbd4fb71e4c
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 4d55ca99aade56ae6cf5b1e01402877c924b78d8
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="children-mdx"></a>Children (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回指定成員的子系集合。  
  
## <a name="syntax"></a>語法  
  
```  
  
Member_Expression.Children  
```  
  
## <a name="arguments"></a>引數  
 *Member_Expression*  
 傳回成員的有效多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 **子系**函式會傳回一個自然順序的集合包含指定成員的子系。 如果指定的成員沒有子系，此函數會傳回空的集合。  
  
## <a name="example"></a>範例  
 下列範例會傳回 Geography 維度中 Geography 階層之 United States 成員的子系。  
  
```  
SELECT [Geography].[Geography].[Country].&[United States].Children ON 0  
FROM [Adventure Works]  
```  
  
 下列範例會傳回中的所有成員**量值**維度資料行在軸上，這包括所有導出的成員和集合之所有子系`[Product].[Model Name]`屬性階層中的資料列軸上**Adventure Works** cube。  
  
```  
SELECT  
    Measures.AllMembers ON COLUMNS,  
    [Product].[Model Name].Children ON ROWS  
FROM  
    [Adventure Works]  
  
```  
  
|版本|記錄|  
|-------------|-------------|  
|[!INCLUDE[ssBOL2005_R03](../includes/ssbol2005-r03-md.md)]|**已變更的內容：**<br /> -更新語法和引數，以改善清晰度。<br /><br /> — 新增更新的範例。|  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

