---
title: MemberValue (MDX) |Microsoft 文件
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 33e91cadc6a63f6b55403aed552c6a15c8afc03d
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2018
ms.locfileid: "34580110"
---
# <a name="membervalue-mdx"></a>MemberValue (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
 [MDX 函數參考&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
