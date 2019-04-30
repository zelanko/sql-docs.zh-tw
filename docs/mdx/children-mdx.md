---
title: 子系 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 03c96a1c90f7ca0a18bd49c371a2ec90582b38f1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63208771"
---
# <a name="children-mdx"></a>Children (MDX)


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
  
 下列範例會傳回中的所有成員**量值**維度資料行在軸上，這包括所有導出的成員和集合之所有子系`[Product].[Model Name]`屬性階層的資料列軸上，從**Adventure Works** cube。  
  
```  
SELECT  
    Measures.AllMembers ON COLUMNS,  
    [Product].[Model Name].Children ON ROWS  
FROM  
    [Adventure Works]  
  
```  
  
|版本|記錄|  
|-------------|-------------|  
|[!INCLUDE[ssBOL2005_R03](../includes/ssbol2005-r03-md.md)]|**已變更的內容：**<br /> -更新語法和引數，以改善清晰度。<br /><br /> -新增更新的範例。|  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
