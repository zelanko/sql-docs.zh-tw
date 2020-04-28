---
title: DataMember （MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 4395f0ff113c8549ec2250d5fa87d37090627b3c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68892909"
---
# <a name="datamember-mdx"></a>DataMember (MDX)


  傳回由系統所產生，與維度某個非分葉成員相關的資料成員。  
  
## <a name="syntax"></a>語法  
  
```  
  
Member_Expression.DataMember  
```  
  
## <a name="arguments"></a>引數  
 *Member_Expression*  
 傳回成員的有效多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 此函式會在任何階層中的非分葉成員上運作，並可由[UPDATE CUBE 語句（MDX）](../mdx/mdx-data-manipulation-update-cube.md)命令用來直接將資料回寫到非分葉成員，而不是對分葉成員的下階。  
  
> [!NOTE]  
>  如果指定的成員是分葉成員，或如果非分葉成員沒有相關聯的資料成員，就會傳回指定的成員。  
  
## <a name="example"></a>範例  
 下列範例會在匯出量值中使用**DataMember**函數，以顯示每個個別員工的銷售配額：  
  
```  
WITH MEMBER measures.InvidualQuota AS   
([Employee].[Employees].currentmember.datamember, [Measures].[Sales Amount Quota])  
,FORMAT_STRING='Currency'  
SELECT {[Measures].[Sales Amount Quota],[Measures].InvidualQuota} ON COLUMNS,  
[Employee].[Employees].MEMBERS ON ROWS  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另請參閱  
 [Mdx 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)   
 [MDX 的關鍵概念 &#40;Analysis Services&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services)  
  
  
