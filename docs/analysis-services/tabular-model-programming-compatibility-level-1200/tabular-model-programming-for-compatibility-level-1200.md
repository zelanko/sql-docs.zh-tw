---
title: Analysis Services 表格式模型程式設計相容性層級 1200年 |Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f7493c09964db2e0a8cbd17c6a2278dd554a2dcc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "68207890"
---
# <a name="tabular-model-programming-for-compatibility-level-1200-and-higher"></a>相容性層級 1200 及以上的表格式模型程式設計
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
開始相容性層級 1200年時，表格式中繼資料用來描述模型建構，為表格式模型物件的描述元來取代歷程記錄的多維度中繼資料。 資料表、 資料行和關聯性的中繼資料是資料表、 資料行和關聯性，而非對應的多維度 （維度和屬性）。  
  
您可以建立新模型相容性層級 1200年或更高版本使用 Microsoft.AnalysisServices.Tabular Api，最新版本的 SQL Server Data Tools (SSDT)，或藉由變更**CompatibilityLevel**的現有表格式若要升級它 （也可以在 SSDT 中） 的模型。 這樣的模型繫結至較新版本的伺服器、 工具和程式設計介面。   
  
升級現有的表格式解決方案會建議但非必要。 現有的指令碼，以及存取或管理表格式模型或資料庫的自訂解決方案可用來做為是。 使用提供的功能層級的 SQL Server 2016 中完全支援舊版的相容性層級。 Azure Analysis Services 僅支援相容性層級 1200年及更高版本。
  
 新的表格式模型會需要不同的程式碼和指令碼中，以下摘要說明。  
  
## <a name="object-model-definitions-as-tabular-metadata-constructs"></a>為表格式中繼資料建構的物件模型定義  
 表格式物件模型為 1200年或更高的模型會在透過 JSON[表格式模型指令碼語言](https://docs.microsoft.com/bi-reference/tmsl/tabular-model-scripting-language-tmsl-reference)和 AMO 資料定義語言，透過新的命名空間，透過[Microsoft.AnalysisServices.Tabular](http://msdn.microsoft.com/library/microsoft.analysisservices.tabular.aspx)

## <a name="script-for-tabular-models-and-databases"></a>表格式模型和資料庫的指令碼  
 TMSL 是 JSON 指令碼語言為表格式模型，支援建立、 讀取、 更新、 刪除作業。 您可以重新整理資料透過 TMSL 和叫用的資料庫作業的連結、 做、 備份、 還原和同步處理。  
  
 AMO PowerShell 接受 TMSL 指令碼做為輸入。  
  
 請參閱[表格式模型指令碼語言&#40;TMSL&#41;參考](https://docs.microsoft.com/bi-reference/tmsl/tabular-model-scripting-language-tmsl-reference)並[Analysis Services PowerShell Reference](../../analysis-services/powershell/analysis-services-powershell-reference.md)如需詳細資訊。  
  
## <a name="query-languages"></a>查詢語言  
 所有的表格式模型支援 DAX 和 MDX。  
  
## <a name="expression-language"></a>運算式語言  
 篩選條件和運算式用來建立導出的物件，包括量值和 Kpi，構成在 DAX 中。 請參閱[了解表格式模型中的 DAX](../../analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular.md)並[Data Analysis Expressions &#40;DAX&#41;在 Analysis Services](http://msdn.microsoft.com/library/abb336c9-3346-4cab-b91b-90f93f4575e5)。  
  
## <a name="managed-code-for-tabular-models-and-databases"></a>表格式模型和資料庫的 managed 程式碼  
 AMO 會包含新的命名空間，Microsoft.AnalysisServices.Tabular，適用於以程式設計方式使用模型。 請參閱[Microsoft.AnalysisServices 命名空間](https://msdn.microsoft.com/library/ms146720\(SQL.130\).aspx)如需詳細資訊。  
  
> [!NOTE]  
>  Analysis Services 管理物件 (AMO)、 ADOMD.NET 和表格式物件模型 (TOM) 用戶端程式庫現在.NET 4.0 執行階段為目標。   
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 開發人員文件](../../analysis-services/analysis-services-developer-documentation.md)   
 [表格式模型程式設計相容性層級 1050年到 1103](../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/tabular-model-programming-for-compatibility-levels-1050-through-1103.md)   
 [技術參考](../../analysis-services/powershell/technical-reference-ssas.md)[升級 Analysis Services](../../database-engine/install-windows/upgrade-analysis-services.md)  
 [相容性層級的表格式模型和資料庫](../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/tabular-model-programming-for-compatibility-levels-1050-through-1103.md)  
  
  
