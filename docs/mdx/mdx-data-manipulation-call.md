---
title: CALL 陳述式 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: de74590ac4c43a9141c0ab2092babf41ffd23ba5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68106306"
---
# <a name="mdx-data-manipulation---call"></a>MDX 資料操作 - CALL


  在目前範圍中或選擇性在指定 Cube 上，執行會傳回空值的預存程序。  
  
## <a name="syntax"></a>語法  
  
```  
  
CALL SP_Name   
   [ (SP_Argument   
      [, SP_Argument ,...n]  
      ) ]   
[ONCube_Expression]  
```  
  
## <a name="arguments"></a>引數  
 *SP_Name*  
 提供預存程序名稱的有效字串運算式。  
  
 *SP_Argument*  
 提供引數給被呼叫之預存程序的有效字串運算式。  
  
 *Cube_Expression*  
 提供 Cube 名稱的有效字串 Cube 運算式。  
  
## <a name="remarks"></a>備註  
 **呼叫**陳述式會執行指定已註冊預存程序，選擇性地包括指定的預存程序的一或多個引數。 **呼叫**陳述式是只能搭配傳回空值的預存程序使用。 此陳述式無法與 MDX 運算式內的其他函數或運算子組合。 傳回值的已註冊預存程序可以直接在 MDX 運算式內呼叫，而且可與其他 MDX 函數與運算子組合。  
  
 如果沒有指定 Cube，陳述式會在目前 Cube 上執行預存程序。  
  
> [!NOTE]  
>  如果預存程序未登錄在用戶端**呼叫**陳述式嘗試呼叫預存程序的執行個體從[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]。  
  
## <a name="see-also"></a>另請參閱  
 [MDX 資料操作陳述式&#40;MDX&#41;](../mdx/mdx-data-manipulation-statements-mdx.md)   
 [使用預存程序 &#40;MDX&#41;](../mdx/using-stored-procedures-mdx.md)  
  
  
