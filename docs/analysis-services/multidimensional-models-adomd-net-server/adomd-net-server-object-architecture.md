---
title: "ADOMD.NET 伺服器物件架構 |Microsoft 文件"
ms.custom: 
ms.date: 02/14/2018
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- ADOMD.NET, object model
- object model [ADOMD.NET]
ms.assetid: bdc81de9-b390-4654-b62a-cd6c0c9ca10d
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 8f0cae374f2670228bbced569d81e87b34a350d2
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/15/2018
---
# <a name="adomdnet-server-object-architecture"></a>ADOMD.NET 伺服器物件架構
  ADOMD.NET 伺服器物件是可以用於建立使用者定義函數 (Udf) 或預存程序中的協助程式物件[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]。  
  
> [!NOTE]  
>  若要使用**Microsoft.AnalysisServices.AdomdServer**命名空間 （以及這些物件），必須將 msmgdsrv.dll 的參考加入 UDF 專案或是預存程序。  
  
 ![顯示 ADOMD.NET 伺服器物件關聯性](../../analysis-services/multidimensional-models-adomd-net-server/media/adomdnetserverobjectmodel.gif "顯示 ADOMD.NET 伺服器物件關聯性")  
ADOMD.NET 物件模型  
  
 與 ADOMD.NET 物件階層互動通常是從最頂層中的一或多個物件開始，如下表所述。  
  
|若要|使用此物件|  
|--------|---------------------|  
|評估多維度運算式 (MDX) 的運算式|<xref:Microsoft.AnalysisServices.AdomdServer.Expression><br /> <xref:Microsoft.AnalysisServices.AdomdServer.Expression> 物件提供執行 MDX 運算式的方法，並在指定的 Tuple 之下評估該運算式。|  
|提供執行 MDX 函數的支援，而無須建構完整的 MDX 陳述式。|<xref:Microsoft.AnalysisServices.AdomdServer.MDX><br /> <xref:Microsoft.AnalysisServices.AdomdServer.MDX> 物件方便您呼叫預先定義的 MDX 函數，而無須使用 <xref:Microsoft.AnalysisServices.AdomdServer.Expression> 物件。 <xref:Microsoft.AnalysisServices.AdomdServer.MDX> 物件的其他功能會在未來的版本中提供。|  
|表示 UDF 目前的執行內容|<xref:Microsoft.AnalysisServices.AdomdServer.Context><br /> <xref:Microsoft.AnalysisServices.AdomdServer.Context> 物件會公開目前 Cube 或是採礦模型以及各種中繼資料集合等資訊。 <xref:Microsoft.AnalysisServices.AdomdServer.Context> 物件的一個主要用法，是 <xref:Microsoft.AnalysisServices.AdomdServer.Hierarchy.CurrentMember%2A> 物件的 <xref:Microsoft.AnalysisServices.AdomdServer.Hierarchy> 屬性。 這個主要用法可讓 UDF 或是預存程序的作者，根據查詢的對象是來自某個維度的哪個成員來做決定。|  
|建立集合和 Tuple|<xref:Microsoft.AnalysisServices.AdomdServer.SetBuilder>, <xref:Microsoft.AnalysisServices.AdomdServer.TupleBuilder><br /> <xref:Microsoft.AnalysisServices.AdomdServer.SetBuilder> 提供建立不可變集合的方法，而 <xref:Microsoft.AnalysisServices.AdomdServer.TupleBuilder> 則提供建立不可變 Tuple 的方法。|  
|支援隱含轉換以及 MDX 語言的六個基本類型之間轉換。|<xref:Microsoft.AnalysisServices.AdomdServer.MDXValue><br /> <xref:Microsoft.AnalysisServices.AdomdServer.MDXValue> 物件提供隱含轉換以及在下列類型之間轉換：<br /><br /> <xref:Microsoft.AnalysisServices.AdomdServer.Hierarchy><br /><br /> <xref:Microsoft.AnalysisServices.AdomdServer.Level><br /><br /> <xref:Microsoft.AnalysisServices.AdomdServer.Member><br /><br /> <xref:Microsoft.AnalysisServices.AdomdServer.Tuple><br /><br /> <xref:Microsoft.AnalysisServices.AdomdServer.Set><br /><br /> 純量或值類型|  
  
## <a name="see-also"></a>另請參閱  
 [ADOMD.NET 伺服器程式設計](../../analysis-services/multidimensional-models-adomd-net-server/adomd-net-server-programming.md)  
  
  
