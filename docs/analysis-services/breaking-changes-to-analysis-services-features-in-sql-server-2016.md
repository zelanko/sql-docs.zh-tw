---
title: "SQL Server 2016 中 Analysis Services 功能的重大變更 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "重大變更 [Analysis Services]"
  - "升級 Analysis Services"
ms.assetid: aeb02542-5a6c-458c-a110-13413dd3e9d9
caps.latest.revision: 55
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 53
---
# SQL Server 2016 中 Analysis Services 功能的重大變更
  「重大變更」會導致資料模型、應用程式程式碼或指令碼在升級模型或伺服器之後無法運作。  
  
> [!NOTE]  
>  相反地，「行為變更」的特性是程式碼變更不會中斷模型或應用程式，但會引進與先前版本不同的行為。  行為變更的範例可能包括變更預設值，或不允許先前允許的屬性或選項設定。 若要深入了解此版本中的行為變更，請參閱 [SQL Server 2016 中 Analysis Services 功能的行為變更](../analysis-services/behavior-changes-to-analysis-services-features-in-sql-server-2016.md)。  
  
## .NET 4.0 版本升級  
 [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)] 中的 Analysis Services 管理物件 (AMO)、ADOMD.NET 和表格式物件模型 (TOM) 用戶端程式庫現在會以 .NET 4.0 執行階段為目標。 這可能是以 .NET 3.5 為目標之應用程式的重大變更。 使用這些組件之更新版本的應用程式現在必須以 .NET 4.0 或更新版本為目標。  
  
## AMO 版本升級  
 [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)] 是 [Analysis Services 管理物件 &#40;AMO&#41;](../Topic/Analysis%20Services%20Management%20Objects%20\(AMO\).md) 的版本升級，而且在某些情況下為重大變更。  現有可呼叫 AMO 的程式碼和指令碼將會繼續執行，就和從舊版升級之前一樣。 不過，如果您需要「重新編譯」應用程式和將 [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)] 執行個體作為目標的話，您必須加入下列命名空間，以讓程式碼或指令碼正常運作：  
  
```  
  
using Microsoft.AnalysisServices;  
using Microsoft.AnalysisServices.Core;  
  
```  
  
 每當您參考程式碼中的 Microsoft.AnalysisServices 組件，就會需要 [Microsoft.AnalysisServices.Core](../Topic/Microsoft.AnalysisServices.Core.md) 命名空間。 如果物件在表格式和多維度狀況中依相同的方式使用，則先前僅存在於 **Microsoft.AnalysisServices** 命名空間內的物件，在此版本中將會移至核心命名空間。  例如，與伺服器相關的 API 將重新放置到核心命名空間。  
  
 雖然現在有多個命名空間，且都存在於相同的組件中 (Microsoft.AnalysisServices.dll)。  
  
## XEvent DISCOVER 變更  
 為了更有效地支援 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 之 SSMS 中的 XEvent DISCOVER 資料流，`DISCOVER_XEVENT_TRACE_DEFINITION` 已取代成下列 XEvent 追蹤：  
  
-   DISCOVER_XEVENT_PACKAGES  
  
-   DISCOVER_XEVENT_OBJECT  
  
-   DISCOVER_XEVENT_OBJECT_COLUMNS  
  
-   DISCOVER_XEVENT_SESSION_TARGETS  
  
## 請參閱＜  
 [Analysis Services Backward Compatibility](../analysis-services/analysis-services-backward-compatibility.md)  
  
  