---
title: MemberValue (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 73a54986a951095b16465cd4934b4dfd447d38bb
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/24/2019
ms.locfileid: "63456712"
---
# <a name="membervalue-mdx"></a>MemberValue (MDX)


  傳回成員的值。  
  
## <a name="syntax"></a>語法  
  
```  
  
Member_Expression.MemberValue  
```  
  
## <a name="arguments"></a>引數  
 *Member_Expression*  
 評估為成員的有效多維度運算式 (MDX) 運算式。  
  
## <a name="return-value"></a>傳回值  
 傳回的成員值包含下列資訊 (以資訊出現在傳回值中的順序列出)：  
  
-   值繫結 (如果有定義)。  
  
-   具有原始資料類型的關鍵字 (若沒有名稱繫結，或關鍵字與標題繫結到相同資料行時)。  
  
-   成員的標題。  
  
## <a name="example"></a>範例  
 下列範例會為 Adventure Works Cube 中 Date 維度的第一個日期，傳回值繫結、成員索引鍵和標題。  
  
```  
WITH MEMBER Measures.ValueColumn as [Date].[Calendar].[July 1, 2001].MemberValue  
MEMBER Measures.KeyColumn as [Date].[Calendar].[July 1, 2001].Member_Key  
MEMBER Measures.NameColumn as [Date].[Calendar].[July 1, 2001].Member_Name  
  
SELECT {Measures.ValueColumn, Measures.KeyColumn, Measures.NameColumn}  ON 0  
from [Adventure Works]  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
