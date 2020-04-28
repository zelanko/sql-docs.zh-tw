---
title: CALL 語句（MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: de74590ac4c43a9141c0ab2092babf41ffd23ba5
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
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
 **CALL**語句會執行指定的已註冊預存程式，並選擇性地包含指定預存程式的一個或多個引數。 **CALL**語句僅適用于傳回空白的預存程式。 此陳述式無法與 MDX 運算式內的其他函數或運算子組合。 傳回值的已註冊預存程序可以直接在 MDX 運算式內呼叫，而且可與其他 MDX 函數與運算子組合。  
  
 如果沒有指定 Cube，陳述式會在目前 Cube 上執行預存程序。  
  
> [!NOTE]  
>  如果預存程式未在用戶端上註冊，則**call**語句會嘗試從的實例呼叫預存程式[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]。  
  
## <a name="see-also"></a>另請參閱  
 [Mdx&#41;&#40;mdx 資料動作陳述式](../mdx/mdx-data-manipulation-statements-mdx.md)   
 [使用預存程序 &#40;MDX&#41;](../mdx/using-stored-procedures-mdx.md)  
  
  
