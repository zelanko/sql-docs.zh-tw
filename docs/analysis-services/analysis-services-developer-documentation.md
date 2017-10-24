---
title: "Analysis Services 開發人員文件 |Microsoft 文件"
ms.custom: 
ms.date: 03/24/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- multidimensional data [Analysis Services], developer's guide
- developer's guide [Analysis Services - multidimensional data]
ms.assetid: 0a6eda76-1c5e-487e-9c8b-1feb09f1a34c
caps.latest.revision: 22
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4694fd3def6dea209929f99559fcc61fe833972a
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="analysis-services-developer-documentation"></a>Analysis Services Developer 文件
在 Analysis Services 中，幾乎每個物件和工作負載可程式化，而且通常沒有可從中選擇的多個方法。  選項包括撰寫 managed 程式碼、 指令碼，或使用 XMLA 和 MSOLAP 開放標準，如果方案需求致使使用.NET framework。

## <a name="what-you-can-accomplish-in-code"></a>您可以在程式碼中完成的作業
一般程式設計案例包括伺服器和資料庫部署、 管理、 模型和資料庫建立和資料存取，從您的自訂應用程式和取用 Analysis Services 資料的報表。 通用於所有這些情況下是一個固定的架構與物件定義階層架構，非常清楚跨越資料定義、 處理和查詢工作負載的作業。

雖然物件和工作負載都可程式化，但它們並非可延伸。 具體來說，您無法建立自訂資料的卡匣不支援的資料來源擷取資料、 自訂或取代公式或儲存引擎的行為，也可以在伺服器、 資料庫或模型上建立新類型的物件中繼資料。

若要進一步詳細說明有關建立新的物件類型的最後一個點： 雖然您無法建立新物件類型，您可以建立在執行階段從運算式或程式碼所建立的導出的物件。 不在模型中所有項目必須是預先定義的而且對應至現有的資料結構。 此外，您可以擴充透過 AMO 將特定物件的資訊傳遞至用戶端應用程式中的註解的結構描述。

## <a name="choose-a-platform-or-approach-to-development"></a>選擇 平台或開發方法
Analysis Services 提供許多方式可以自訂的解決方案，透過程式碼，但大部分的開發人員使用受管理的應用程式開發介面或指令碼。

- 受管理的 Api 包括[AMO 和 TOM](http://msdn.microsoft.com/library/mt436122.aspx)資料定義和管理工作，和[ADOMD.NET](http://msdn.microsoft.com/library/mt465769.aspx)以支援查詢用戶端程式碼。 SQL Server 2016，AMO 會更新為使用新的表格式中繼資料的模型建立或升級至 1200年 （含） 以上的相容性層級。

- 指令碼通常可以達到相同的結果當做可執行檔，可能是較少的工作與程式。

  - 您可以撰寫使用直接呼叫 AMO 類型的 Analysis Services PowerShell 元件的 PowerShell 指令碼。 在 PowerShell 中，您也可以建立及執行 ASSL/XMLA 或 TMSL （JSON) 中的指令碼。

  - ASSL 和 TMSL 是提供使用物件的指令碼語言探索及執行作業。 您所使用的指令碼的類型取決於基礎的伺服器、 資料庫或模型。

  - 表格式模型或相容性層級 1200年 （含） 以上的資料庫使用表格式模型指令碼語言 (TMSL)，也就是在 JSON 中。

  - 多維度模型和相容性層級 1050年-1103年的表格式模型使用 Analysis Services 指令碼語言 (ASSL)，也就是 Analysis Services 延伸模組的 XMLA 開放標準。

  - 您可以在 Management Studio 中產生 ASSL 或 TMSL 指令碼。 您也可以使用**檢視程式碼**ASSL 或 TMSL 中檢視模型定義的 SQL Server Data Tools 中。

- 雖然可以建置 MDX 的 XMLA 開放標準為基礎的解決方案，它是相當罕見，若要這樣做。 XMLA 以外沒有文件，以協助您，和大部分社群和支援論壇 MDX 參考繪製從.NET 或原生 (MSOLAP) 技術的體驗。

## <a name="programming-in-analysis-services"></a>在 Analysis Services 中程式設計
[資料採礦程式設計](../analysis-services/data-mining-programming.md)描述建置方案，包括資料採礦物件的方法。

[多維度模型程式設計](../analysis-services/multidimensional-models/multidimensional-model-programming.md)描述的開發工作和以整合自訂方案中的多維度模型物件的方法。

[表格式模型程式設計相容性層級 1200年針對和更新版本](../analysis-services/tabular-model-programming-compatibility-level-1200/tabular-model-programming-for-compatibility-level-1200.md)
**的新功能 SQL Server 2016**。  摘要說明的介面和指令碼語言，用於以程式設計方式使用表格式 1200年和更高版本的模型。

[表格式模型的程式設計透過 1103年相容性層級 1050年](../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/tabular-model-programming-for-compatibility-levels-1050-through-1103.md)這份文件僅供開發人員支援在舊版的相容性層級的表格式模型。 它會描述 XML 語法定義表格式模型的 CSDL 延伸模組。 其中也包括有關表格式物件模型定義和語法的資訊。

[Analysis Services 管理物件 (AMO)](https://msdn.microsoft.com/library/mt436122.aspx)開發人員參考文件的 managed 提供者，Analysis Services 管理物件 (AMO)，資料定義和管理，包括處理。

[ADOMD.NET](http://msdn.microsoft.com/library/mt465769.aspx)開發人員參考文件的受管理的提供者，ADOMD.NET 中，用來以程式設計方式的資料存取和查詢工作負載。

[Analysis Services 結構描述資料列集](../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md)描述提供有關伺服器狀態、 伺服器作業和資料庫物件的結構描述資料列集。

[XML for Analysis &#40;XMLA &#41;參考](../analysis-services/xmla/xml-for-analysis-xmla-reference.md)描述 XMLA 概念可幫助您了解 XMLA 如何提供給您的自訂方案。 也會描述符合 XMLA 1.1 規格的層級。

[Analysis Services 指令碼語言 &#40;ASSL XMLA &#41;](../analysis-services/scripting/analysis-services-scripting-language-assl-for-xmla.md)描述 XMLA 之 ASSL 延伸模組。 ASSL 針對補充 XMLA 規格的 Analysis Services 多維度模型提供資料定義和操作語言。

[表格式模型指令碼語言 &#40;TMSL &#41;參考](../analysis-services/tabular-model-scripting-language-tmsl-reference.md)TMSL 是 1200年或更高的相容性層級的表格式模型的 JSON 表示法。 物件定義根據表格式中繼資料建構，例如資料表、 資料行和關聯性，而可能不熟悉，如果您是在表格式模式的 Analysis Services 資料模型化新的多維度中繼資料。

[Analysis Services PowerShell Reference](../analysis-services/powershell/analysis-services-powershell-reference.md)用於系統管理功能，加上一般用途的 cmdlet 文件**Invoke-ascmd**指令程式可接受任何指令碼或做為輸入的查詢。

## <a name="see-also"></a>另請參閱
[技術參考 &#40;Ssas&#41;](../analysis-services/powershell/technical-reference-ssas.md) 
[查詢及運算式語言參考 &#40;Analysis Services &#41;](http://msdn.microsoft.com/library/gg492188.aspx)

