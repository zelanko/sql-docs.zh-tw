---
title: KPIValue （MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: c34e5b345ee0e4d780de66449473237cc413ace6
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "67905848"
---
# <a name="kpivalue-mdx"></a>KPIValue (MDX)


  傳回計算指定之關鍵效能指標 (KPI) 值的成員。  
  
## <a name="syntax"></a>語法  
  
```  
  
KPIValue(KPI_Name)  
```  
  
## <a name="arguments"></a>引數  
 *KPI_Name*  
 指定 KPI 名稱的有效字串運算式。  
  
## <a name="remarks"></a>備註  
  
## <a name="example"></a>範例  
 下列範例會為 [會計年度] 屬性階層的三位成員下階傳回通路營收量值的 KPI 值、KPI 目標、KPI 狀態及 KPI 趨勢。  
  
```  
SELECT  
   { KPIValue("Channel Revenue"),   
     KPIGoal("Channel Revenue"),  
     KPIStatus("Channel Revenue"),   
     KPITrend("Channel Revenue")  
   } ON Columns,  
Descendants  
   ( { [Date].[Fiscal].[Fiscal Year].&[2002],  
       [Date].[Fiscal].[Fiscal Year].&[2003],  
       [Date].[Fiscal].[Fiscal Year].&[2004]   
     }, [Date].[Fiscal].[Fiscal Quarter]  
   ) ON Rows  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
