---
title: KPIStatus （MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: aa07788bc00cc3317024d287f1054a67c6447356
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67905887"
---
# <a name="kpistatus-mdx"></a>KPIStatus (MDX)


  會傳回正規化值，代表指定之關鍵效能指標 (KPI) 的狀態部分。  
  
## <a name="syntax"></a>語法  
  
```  
  
KPIStatus(KPI_Name)  
```  
  
## <a name="arguments"></a>引數  
 *KPI_Name*  
 指定 KPI 名稱的有效字串運算式。  
  
## <a name="remarks"></a>備註  
 狀態值一般是介於 -1 和 1 之間的正規化值。  
  
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
 [Mdx 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
