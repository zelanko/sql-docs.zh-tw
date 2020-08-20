---
description: AllMembers (MDX)
title: AllMembers (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ba70d4ad8b301cbd8af2fd76ce058f2dab2e4a4c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461670"
---
# <a name="allmembers-mdx"></a>AllMembers (MDX)


  評估階層或層級運算式，並且傳回集合，其中包含指定之階層或層級的所有成員，包括階層或層級中的所有導出成員。  
  
## <a name="syntax"></a>語法  
  
```  
  
Hierarchy syntax  
Hierarchy_Expression.AllMembers  
  
Level syntax  
Level_Expression.AllMembers  
```  
  
## <a name="arguments"></a>引數  
 *Hierarchy_Expression*  
 傳回階層的有效多維度運算式 (MDX) 運算式。  
  
 *Level_Expression*  
 傳回層級的有效多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 **AllMembers**函數會傳回一個集合，其中包含指定之階層或層級中的所有成員，包括匯出成員。 **AllMembers**函數會傳回匯出成員，即使指定的階層或層級不包含可見的成員也一樣。  
  
> [!IMPORTANT]  
>  當維度只包含單一可見的階層，該階層可由維度名稱或階層名稱參考，因為此狀況下維度名稱會解析成其唯一可見的階層。 例如，`Measures.AllMembers` 即是有效的 MDX 運算式，因為它解析成量值維度上唯一的階層。  
  
> [!NOTE]  
>  **AllMembers**函數在語義上類似于[AddCalculatedMembers (MDX) ](../mdx/addcalculatedmembers-mdx.md)函數。  
  
## <a name="examples"></a>範例  
 下列範例會傳回 [資料行軸上的 [屬性] 階層中的所有成員 `Date].[Calendar Year]` ，包括匯出成員，以及 `[Product].[Model Name]` 來自 [ **艾德作品** ] cube 之資料列軸上屬性階層的所有子系集合。  
  
```  
SELECT  
   [Date].[Calendar Year].AllMembers ON COLUMNS,  
   [Product].[Model Name].Children ON ROWS  
FROM  
   [Adventure Works]  
```  
  
 下列範例會傳回資料行軸上 [ **量值** ] 維度中的所有成員，這包括所有匯出成員，以及 `[Product].[Model Name]` 來自 [ **艾德作品** ] cube 之資料列軸上屬性階層的所有子系集合。  
  
```  
SELECT  
    Measures.AllMembers ON COLUMNS,  
    [Product].[Model Name].Children ON ROWS  
FROM  
    [Adventure Works]  
```  
  
## <a name="see-also"></a>另請參閱  
 [AddCalculatedMembers &#40;MDX&#41;](../mdx/addcalculatedmembers-mdx.md)   
 [&#40;MDX 的子系&#41;](../mdx/children-mdx.md)   
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
