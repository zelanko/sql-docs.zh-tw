---
title: 錯誤 (MDX) |Microsoft 文件
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 774bcd1a0093350b3eb3cbf8cac4f4eeae188ed1
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2018
ms.locfileid: "34579650"
---
# <a name="error-mdx"></a>Error (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  引發錯誤，選擇性提供指定的錯誤訊息。  
  
## <a name="syntax"></a>語法  
  
```  
  
Error( [ Error_Text ] )  
```  
  
## <a name="arguments"></a>引數  
 *Error_Text*  
 包含要傳回之錯誤訊息的有效字串運算式。  
  
## <a name="examples"></a>範例  
 下列查詢會示範如何使用**錯誤**函式內的導出量值：  
  
 `WITH MEMBER MEASURES.ERRORDEMO AS ERROR("THIS IS AN ERROR")`  
  
 `SELECT`  
  
 `MEASURES.ERRORDEMO ON 0`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
