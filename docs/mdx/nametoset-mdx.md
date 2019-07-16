---
title: NameToSet (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 77731495eb058da05f6c61be391591a40725e579
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68088387"
---
# <a name="nametoset-mdx"></a>NameToSet (MDX)


  傳回一個集合，包含多維度運算式 (MDX） 格式化的字串所指定的成員。  
  
## <a name="syntax"></a>語法  
  
```  
  
NameToSet(Member_Name)   
```  
  
## <a name="arguments"></a>引數  
 *Member_Name*  
 代表成員名稱的有效字串運算式。  
  
## <a name="remarks"></a>備註  
 如果指定的成員名稱的話**NameToSet**函式會傳回包含該成員的集合。 否則，函數會傳回空的集合。  
  
> [!NOTE]  
>  指定的成員名稱只能是成員名稱，不能是成員運算式。 若要使用成員運算式，請參閱[StrToSet &#40;MDX&#41;](../mdx/strtoset-mdx.md)。  
  
## <a name="example"></a>範例  
 下列範例會傳回指定成員名稱的預設量值。  
  
```  
SELECT NameToSet('[Date].[Calendar].[July 2001]') ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
