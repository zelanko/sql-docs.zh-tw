---
description: Children (MDX)
title: " (MDX 的子系) |Microsoft Docs"
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 9a37bc27564baf9d75e10af78fb477ea08be092e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466510"
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
 **子**函數會傳回一個自然排序的集合，其中包含指定成員的子系。 如果指定的成員沒有子系，此函數會傳回空的集合。  
  
## <a name="example"></a>範例  
 下列範例會傳回 Geography 維度中 Geography 階層之 United States 成員的子系。  
  
```  
SELECT [Geography].[Geography].[Country].&[United States].Children ON 0  
FROM [Adventure Works]  
```  
  
 下列範例會傳回資料行軸上 [ **量值** ] 維度中的所有成員，這包括所有匯出成員，以及 `[Product].[Model Name]` 來自 [ **艾德作品** ] cube 之資料列軸上屬性階層的所有子系集合。  
  
```  
SELECT  
    Measures.AllMembers ON COLUMNS,  
    [Product].[Model Name].Children ON ROWS  
FROM  
    [Adventure Works]  
  
```  
  
|版本|記錄|  
|-------------|-------------|  
|[!INCLUDE[ssBOL2005_R03](../includes/ssbol2005-r03-md.md)]|**變更的內容：**<br /> -已更新語法和引數，以改善清晰度。<br /><br /> -已新增更新的範例。|  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
