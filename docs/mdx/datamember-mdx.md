---
title: "DataMember (MDX) |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DATAMEMBER
dev_langs:
- kbMDX
helpviewer_keywords:
- DataMember function
ms.assetid: 65bf21e8-1cb2-4ae8-bfbe-bb4d72589557
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: b6be9e31f666eafaba1ec7ad346a7e5bb28da9b0
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="datamember-mdx"></a>DataMember (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回由系統所產生，與維度某個非分葉成員相關的資料成員。  
  
## <a name="syntax"></a>語法  
  
```  
  
Member_Expression.DataMember  
```  
  
## <a name="arguments"></a>引數  
 *Member_Expression*  
 傳回成員的有效多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 此函式中的任何階層的非分葉成員上運作，並可供[UPDATE CUBE 陳述式 (MDX)](../mdx/mdx-data-manipulation-update-cube.md)命令到非分葉成員直接管理，而不是分葉成員的下階的回寫資料。  
  
> [!NOTE]  
>  如果指定的成員是分葉成員，或如果非分葉成員沒有相關聯的資料成員，就會傳回指定的成員。  
  
## <a name="example"></a>範例  
 下列範例會使用**DataMember**中顯示的銷售配額每個員工的導出量值函式：  
  
```  
WITH MEMBER measures.InvidualQuota AS   
([Employee].[Employees].currentmember.datamember, [Measures].[Sales Amount Quota])  
,FORMAT_STRING='Currency'  
SELECT {[Measures].[Sales Amount Quota],[Measures].InvidualQuota} ON COLUMNS,  
[Employee].[Employees].MEMBERS ON ROWS  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)   
 [MDX &#40; 中的重要概念Analysis Services &#41;](../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md)  
  
  

