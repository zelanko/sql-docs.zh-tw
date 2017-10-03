---
title: "Introduction to 中分析表格式物件模型 (TOM) 服務 AMO |Microsoft 文件"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 57a4a934-ecd0-4365-8147-d36899d86751
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: ab4bfb890124538878fd4d618dee05d393a4864c
ms.contentlocale: zh-tw
ms.lasthandoff: 09/27/2017

---
# <a name="introduction-to-the-tabular-object-model-tom-in-analysis-services-amo"></a>Analysis Services AMO 中表格式物件模型 (TOM) 簡介

[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

  表格式物件模型 (TOM) 是 Analysis Services 管理物件 (AMO) 用戶端程式庫，以支援建置在相容性層級 1200年 （含） 以上的表格式模型程式設計案例建立擴充功能。 如同 AMO，TOM 提供程式設計的方式來處理管理功能，例如建立模型、 匯入和重新整理資料，及指派角色和權限。  
  
TOM 公開原生的表格式中繼資料，例如**模型**，**資料表**，**資料行**，和**關聯性**物件。  物件模型樹狀結構，以下提供的概要說明之元件部分的關聯方式。  
  
 因為 TOM 是 AMO 的延伸，表示 SQL Server 2016 中引進新的表格式物件的所有類別會都實作新的 Microsoft.AnalysisServices.Tabular.dll 組件。 一般用途的 AMO 類別已移至 Microsoft.AnalysisServices.Core 組件。 您的程式碼必須參考兩個組件。
請參閱[安裝、 散佈及參考表格式物件模型 &#40;Microsoft.AnalysisServices.Tabular &#41;](../../analysis-services/tabular-model-programming-compatibility-level-1200/install-distribute-and-reference-the-tabular-object-model.md)如需詳細資訊。  
  
 目前應用程式開發介面透過.NET framework 是僅適用於 managed 程式碼。 若要檢閱的完整清單程式設計選項，包括指令碼和查詢語言支援，請參閱[的相容性層級 1200年的表格式模型程式設計](../../analysis-services/tabular-model-programming-compatibility-level-1200/tabular-model-programming-for-compatibility-level-1200.md)。  
  
## <a name="tabular-object-model-hierarchy"></a>表格式物件模型階層  
 邏輯的觀點而言，所有的表格式物件形成樹狀目錄中的根是**模型**、 descended 從資料庫。 **伺服器**和**資料庫**不會視為 「 表格式 」 因為這些物件也可以代表多維度模式中或在較低相容性層級的表格式模型中執行的伺服器上裝載的多維度資料庫層級，不會使用表格式中繼資料物件定義。 
  
 除了**AttributeHierarchy**， **KPI**，和**LinguisticMetadata**，每一個子物件可以是集合的成員。 例如，**模型**物件包含的集合**資料表**物件 (透過**資料表**屬性)，與每個**資料表**物件包含集合的**資料行**物件，依此類推。  
  
 最低層級之下階的這個階層中的任何父物件是**註解**可用來選擇性地延伸架構，只要提供處理它的程式碼的物件。  
  
 ![物件階層架構圖表](../../analysis-services/tabular-model-programming-compatibility-level-1200/media/ssastomobjectmodeldiagram.png "物件階層架構圖表")  
  
## <a name="tom-and-other-related-technologies"></a>TOM 和其他相關技術

TOM 建置 AMO 基礎結構，也適用於多維度和相容性層級低於 1200年的表格式資料庫的頂端。

這會有一些實際影響。
第一個是 all，當您管理表格式中繼資料中未指定的物件時 (例如**伺服器**或**資料庫**)，您必須利用現有的 AMO 堆疊的說明這些物件的組件。 舊版的 API 會提供更細微的說明，當作探索到的伺服器，或是儲存到伺服器時，物件狀態的主要和次要物件的概念。 Microsoft.AnalysisServices 命名空間之下的 MajorObject 類別公開的方法**重新整理**和**更新**。 次要物件是唯一的重新整理或儲存的主要物件透過包含它們。

相反地，當您管理屬於表格式中繼資料的物件 (例如**模型**或**資料表**)，您可以利用全新的表格式堆疊。 在此堆疊，更新是更細緻，這表示每個中繼資料物件 (衍生自**MetadataObject** Microsoft.AnalysisServices.Tabular 命名空間之下的類別) 可以個別儲存到伺服器。 一般而言，您會發現整個**模型**，然後針對個別的中繼資料物件，其下進行變更 (例如**資料表**或**資料行**)，然後呼叫**Model.SaveChanges()**方法 （了解更細緻的層級，您所做的變更），將命令傳送至伺服器，以更新這些變更的物件。

### <a name="tom-and-xmla"></a>TOM 和 XMLA

在線上，TOM 會使用 XMLA 通訊協定，通訊與 Analysis Services 伺服器，以及管理物件。 當管理非表格式物件時，會使用 TOM [ASSL](../scripting/analysis-services-scripting-language-assl-for-xmla.md)，Analysis Services 指令碼語言擴充功能的 XMLA。 當管理表格式物件，TOM 使用 SSAS 表格式通訊協定，也 XMLA 的延伸模組。 請參閱[MS-SSAS T SQL Server Analysis Services 表格式通訊協定文件](https://msdn.microsoft.com/library/mt719260.aspx)如需詳細資訊。

### <a name="tom-and-json"></a>TOM 和 JSON

表格式中繼資料，其中會結構化成 JSON 文件，都具有新命令和物件模型定義的語法透過表格式模型指令碼語言[TMSL](../tabular-model-scripting-language-tmsl-reference.md)。 指令碼語言使用 JSON 要求和回應的主體。

雖然 TMSL 和 TOM 公開 （expose） 相同的物件 (**資料表**，**資料行**等等) 和相同的作業 (**建立**，**刪除**， **重新整理**)，TOM 不會使用 （它會使用 MS SSAS 表格式的通訊協定，如先前所述） 在網路上的 TMSL。

身為使用者，您可以選擇是否要管理透過 TOM 程式庫，從您的 C# 程式或 PowerShell 指令碼，或透過 TMSL 指令碼，透過 PowerShell、 SQL Server Management Studio (SSMS) 或 SQL Server Agent 作業執行的表格式資料庫。

在決定来使用其中一個會您需求的細節。 TOM 程式庫提供更豐富的功能相較於 TMSL。 具體來說，而 TMSL 只提供了資料庫、 資料表、 資料分割或角色層級的廣泛作業，TOM 會允許作業更精細太多。 若要產生或以程式設計方式更新模型，您必須使用 TOM 文件庫中的應用程式開發介面的完整範圍。
  
## <a name="see-also"></a>另請參閱  
 [相容性層級 1200年的表格式模型程式設計](../../analysis-services/tabular-model-programming-compatibility-level-1200/tabular-model-programming-for-compatibility-level-1200.md)   
 [Analysis Services 中表格式模型的相容性層級](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)  
[Analysis Services PowerShell](../../analysis-services/powershell/analysis-services-powershell-reference.md)
  
