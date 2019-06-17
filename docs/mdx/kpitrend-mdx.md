---
title: KPITrend (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d5d1a211e473cf2eed96603d91b581a52e9062d7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63272735"
---
# <a name="kpitrend-mdx"></a>KPITrend (MDX)


  會傳回正規化值，代表指定之關鍵效能指標 (KPI) 的趨勢部分。  
  
## <a name="syntax"></a>語法  
  
```  
  
KPITrend(KPI_Name)  
```  
  
## <a name="arguments"></a>引數  
 *KPI_Name*  
 指定 KPI 名稱的有效字串運算式。  
  
## <a name="remarks"></a>備註  
 趨勢值一般是介於 -1 和 1 之間的正規化值。  
  
## <a name="example"></a>範例  
 下列範例會為 [會計年度] 屬性階層的三位成員下階傳回通路營收量值的 KPI 值、KPI 目標、KPI 狀態及 KPI 趨勢：  
  
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
  
  
