---
title: "相容性層級 1200年的表格式模型程式設計 |Microsoft 文件"
ms.custom: 
ms.date: 05/30/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d343f693-c800-42fe-bb4f-2c38a10919f1
caps.latest.revision: "15"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 2a2b814f4944c0e135c345d8f78970a1d08c8918
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="tabular-model-programming-for-compatibility-level-1200-and-higher"></a>表格式模型程式設計相容性層級 1200年針對和更新版本

[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

從開始相容性層級 1200年時，表格式中繼資料用來描述模型建構，為表格式模型物件的描述元取代歷程記錄的多維度中繼資料。 資料表、 資料行及關聯性的中繼資料是資料表、 資料行和關聯性，而非對應的多維度 （維度和屬性）。  
  
您可以建立新模型相容性層級 1200年或更高藉由使用 Microsoft.AnalysisServices.Tabular Api，最新版本的 SQL Server Data Tools (SSDT)，或變更**CompatibilityLevel**的現有表格式若要升級它 （也可以在 SSDT 中） 的模型。 這樣的模型繫結至較新版本的伺服器、 工具和程式設計介面。   
  
升級現有的表格式方案，建議使用但非必要。 現有的指令碼的存取或管理表格式模型或資料庫的自訂方案，以及可用來當作-是。 使用提供的功能層級的 SQL Server 2016 中完全支援舊版的相容性層級。 Azure Analysis Services 僅支援相容性層級 1200年 （含） 以上。
  
 新的表格式模型會需要不同的程式碼和指令碼，以下摘要說明。  
  
## <a name="object-model-definitions-as-tabular-metadata-constructs"></a>為表格式中繼資料建構的物件模型定義  
 表格式物件模型為 1200年或更高的模型會公開在 JSON 中透過[表格式模型指令碼語言](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)和透過新的命名空間中透過 AMO 資料定義語言[Microsoft.AnalysisServices.Tabular](http://msdn.microsoft.com/library/microsoft.analysisservices.tabular.aspx)

## <a name="script-for-tabular-models-and-databases"></a>表格式模型與資料庫的指令碼  
 TMSL 是 JSON 指令碼語言的表格式模型，以支援建立、 讀取、 更新、 刪除作業。 您可以重新整理資料透過 TMSL 和叫用的資料庫作業的附加、 detatch、 備份、 還原和同步處理。  
  
 AMO PowerShell 接受 TMSL 指令碼做為輸入。  
  
 請參閱[表格式模型指令碼語言 &#40;TMSL &#41;參考](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)和[Analysis Services PowerShell Reference](../../analysis-services/powershell/analysis-services-powershell-reference.md)如需詳細資訊。  
  
## <a name="query-languages"></a>查詢語言  
 所有的表格式模型支援 DAX 和 MDX。  
  
## <a name="expression-language"></a>運算式語言  
 篩選和運算式可用來建立導出的物件，包括量值和 Kpi，DAX 中所構成。 請參閱[了解表格式模型中的 DAX](../../analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular.md)和[Data Analysis Expressions &#40; DAX &#41; 中 Analysis Services](http://msdn.microsoft.com/library/abb336c9-3346-4cab-b91b-90f93f4575e5)。  
  
## <a name="managed-code-for-tabular-models-and-databases"></a>表格式模型以及資料庫的 managed 程式碼  
 AMO 包含新的命名空間中 Microsoft.AnalysisServices.Tabular，以程式設計方式使用模型。 請參閱[Microsoft.AnalysisServices 命名空間](https://msdn.microsoft.com/library/ms146720\(SQL.130\).aspx)如需詳細資訊。  
  
> [!NOTE]  
>  Analysis Services 管理物件 (AMO)、 ADOMD.NET 和表格式物件模型 (TOM) 用戶端程式庫現在 runtime 為目標的.NET 4.0。   
  
## <a name="see-also"></a>請參閱＜  
 [Analysis Services 開發人員文件](../../analysis-services/analysis-services-developer-documentation.md)   
 [表格式模型設計程式的相容性層級 1050年透過 1103](../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/tabular-model-programming-for-compatibility-levels-1050-through-1103.md)   
 [技術參考 &#40;Ssas&#41;](../../analysis-services/powershell/technical-reference-ssas.md)[升級 Analysis Services](../../database-engine/install-windows/upgrade-analysis-services.md)  
 [相容性層級的表格式模型和資料庫](../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/tabular-model-programming-for-compatibility-levels-1050-through-1103.md)  
  
  
