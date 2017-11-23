---
title: "MemberValue (MDX) |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: MEMBERVALUE
dev_langs: kbMDX
helpviewer_keywords: MemberValue function
ms.assetid: f9b2af16-2b81-48e4-ae81-99f64e4bbc98
caps.latest.revision: "15"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 2d6a74903eb98002864e8d3ae5a68e5af4f07112
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="membervalue-mdx"></a>MemberValue (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
  
## <a name="see-also"></a>請參閱＜  
 [MDX 函數參考 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
