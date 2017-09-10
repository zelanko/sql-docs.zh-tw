---
title: "AMO 資料採礦類別 |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- data mining [AMO]
- AMO, data mining
- Analysis Management Objects, data mining
ms.assetid: e4108825-b722-417c-9647-ab30ce35e549
caps.latest.revision: 22
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a4eeb92697ce1a6a8475fa973a51ee6bdf9536b0
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="amo-data-mining-classes"></a>AMO 資料採礦類別
  資料採礦類別可協助您建立、修改、刪除和處理資料採礦物件。 處理資料採礦物件包括建立資料採礦結構、建立資料採礦模型和處理模型。  
  
 如需有關如何設定環境，以及大約<xref:Microsoft.AnalysisServices.Server>， <xref:Microsoft.AnalysisServices.Database>， <xref:Microsoft.AnalysisServices.DataSource>，和<xref:Microsoft.AnalysisServices.DataSourceView>物件，請參閱[AMO 基礎類別](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-fundamental-classes.md)。  
  
 定義分析管理物件 (AMO) 中的物件需要在每個物件上設定一些屬性，才能設定正確的內容。 複雜的物件 (例如 OLAP 與資料採礦物件) 需要較長且詳盡的程式碼。  
  
 本主題包含下列幾節：  
  
-   [MiningStructure 物件](#MiningStructure)  
  
-   [MiningModel 物件](#MiningModel)  
  
 下圖顯示在本主題中說明的類別關聯性。  
  
 ![AMO 資料採礦類別](../../../analysis-services/multidimensional-models/analysis-management-objects/media/amo-dataminingclasses.gif "AMO 資料採礦類別")  
  
##  <a name="MiningStructure"></a>MiningStructure 物件  
 採礦結構是採礦模型的容器。 此結構會定義採礦模型會使用的所有可能資料行。 每個採礦模型都會從結構中定義的資料行集合定義自己的資料行。  
  
 簡單的 <xref:Microsoft.AnalysisServices.MiningStructure> 物件是由下列項目所組成的：基本資訊、資料來源檢視、一或多個 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>、零個或多個 <xref:Microsoft.AnalysisServices.TableMiningStructureColumn> 以及 <xref:Microsoft.AnalysisServices.MiningModelCollection>。  
  
 基本資訊包括 <xref:Microsoft.AnalysisServices.MiningStructure> 物件的名稱與識別碼 (內部識別碼)。  
  
 <xref:Microsoft.AnalysisServices.DataSourceView> 物件會保存採礦結構的基礎資料模型。  
  
 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn> 是具有單一值的資料行或屬性。  
  
 <xref:Microsoft.AnalysisServices.TableMiningStructureColumn> 是每個案例具有多個值的資料行或屬性。  
  
 <xref:Microsoft.AnalysisServices.MiningModelCollection> 包含在相同的資料上建立的所有採礦模型。  
  
 建立 <xref:Microsoft.AnalysisServices.MiningStructure> 物件的方法是將它加入資料庫的 <xref:Microsoft.AnalysisServices.MiningStructureCollection>，並使用 Update 方法將 <xref:Microsoft.AnalysisServices.MiningStructure> 物件更新到伺服器。  
  
 若要移除 <xref:Microsoft.AnalysisServices.MiningStructure> 物件，必須使用 <xref:Microsoft.AnalysisServices.MiningStructure> 物件的 Drop 方法來卸除它。 從集合移除 <xref:Microsoft.AnalysisServices.MiningStructure>物件並不會影響伺服器。  
  
 <xref:Microsoft.AnalysisServices.MiningStructure> 可以使用自己的處理方法進行處理，或者也可以在父物件使用其處理方法自行處理時，一併加以處理。  
  
### <a name="columns"></a>資料行  
 資料行會保存模型的資料，而且視用法而定，可屬於不同的類型：Key、Input、Predictable 或是 InputPredictable。 可預測的資料行是建立採礦模型的目標。  
  
 單一值資料行在 AMO 中稱為 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>。 多個值資料行則稱為 <xref:Microsoft.AnalysisServices.TableMiningStructureColumn>。  
  
#### <a name="scalarminingstructurecolumn"></a>ScalarMiningStructureColumn  
 簡單的 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn> 物件是由基本資訊、類型、內容和資料繫結所組成。  
  
 基本資訊包括 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn> 的名稱與識別碼 (內部識別碼)。  
  
 類型是值的資料類型：LONG、BOOLEAN、TEXT、DOUBLE、DATE。  
  
 內容會告訴引擎如何為資料行建立模型。 值可以是：Discrete、Continuous、Discretized、Ordered、Cyclical、Probability、Variance、StdDev、ProbabilityVariance、ProbabilityStdDev、Support、Key。  
  
 資料繫結會使用資料來源檢視元素，將資料採礦資料行與基礎資料模型連結。  
  
 建立 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn> 物件的方法是將它加入父 <xref:Microsoft.AnalysisServices.MiningStructureCollection>，並使用 Update 方法將父 <xref:Microsoft.AnalysisServices.MiningStructure> 物件更新到伺服器。  
  
 若要移除 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>，必須從父 <xref:Microsoft.AnalysisServices.MiningStructure> 的集合移除它，而且必須使用 Update 方法將父 <xref:Microsoft.AnalysisServices.MiningStructure> 物件更新到伺服器。  
  
#### <a name="tableminingstructurecolumn"></a>TableMiningStructureColumn  
 簡單的 <xref:Microsoft.AnalysisServices.TableMiningStructureColumn> 物件是由基本資訊與純量資料行所組成。  
  
 基本資訊包括 <xref:Microsoft.AnalysisServices.TableMiningStructureColumn> 的名稱與識別碼 (內部識別碼)。  
  
 純量資料行是 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>。  
  
 建立 <xref:Microsoft.AnalysisServices.TableMiningStructureColumn> 的方法是將它加入父 <xref:Microsoft.AnalysisServices.MiningStructure> 集合，並使用 Update 方法將父 <xref:Microsoft.AnalysisServices.TableMiningStructureColumn> 物件更新到伺服器。  
  
 若要移除 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>，必須從父 <xref:Microsoft.AnalysisServices.MiningStructure> 的集合移除它，而且必須使用 Update 方法將父 <xref:Microsoft.AnalysisServices.MiningStructure> 物件更新到伺服器。  
  
##  <a name="MiningModel"></a>MiningModel 物件  
 <xref:Microsoft.AnalysisServices.MiningModel> 這個物件可讓您從結構中選擇要使用的資料行、要使用的演算法，以及 (選擇性) 要調整模型的特定參數。 例如，您可能需要在使用相同演算法的相同採礦結構中定義幾個採礦模型，但是要忽略來自某個模型之採礦結構的一些資料行，在其他模型中將它們做為輸入，並在第三個模型中將它們做為輸入並進行預測。 如果在某個採礦模型中，您想要將資料行視為連續，但是在其他模型中，卻想要將資料行視為離散化，這可能會非常有用。  
  
 簡單的 <xref:Microsoft.AnalysisServices.MiningModel> 物件是由以下項目所組成：基本資訊、演算法定義和資料行。  
  
 基本資訊包括採礦模型的名稱與識別碼 (內部識別碼)。  
  
 演算法定義會參考在 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 中提供的任何一種標準演算法，或是在伺服器上啟用的任何自訂演算法。  
  
 資料行是演算法及其用法定義所使用的資料行集合。  
  
 建立 <xref:Microsoft.AnalysisServices.MiningModel> 的方法是將它加入資料庫的 <xref:Microsoft.AnalysisServices.MiningModelCollection>，並使用 Update 方法將 <xref:Microsoft.AnalysisServices.MiningModel> 物件更新到伺服器。  
  
 若要移除 <xref:Microsoft.AnalysisServices.MiningModel>，必須使用 <xref:Microsoft.AnalysisServices.MiningModel> 的 Drop 方法來卸除它。 從集合移除 <xref:Microsoft.AnalysisServices.MiningModel> 並不會影響伺服器。  
  
 建立完成後，<xref:Microsoft.AnalysisServices.MiningModel> 可以使用自己的處理方法進行處理，或者也可以在父物件使用其處理方法自行處理時，一併加以處理。  
  
## <a name="see-also"></a>另請參閱  
 <xref:Microsoft.AnalysisServices>   
 [AMO 基礎類別](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-fundamental-classes.md)   
 [程式設計 AMO 資料採礦物件](../../../analysis-services/multidimensional-models/analysis-management-objects/programming-amo-data-mining-objects.md)   
 [AMO 類別簡介](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-classes-introduction.md)   
 [邏輯架構 &#40;Analysis Services-多維度資料 &#41;](../../../analysis-services/multidimensional-models/olap-logical/understanding-microsoft-olap-logical-architecture.md)   
 [資料庫物件 &#40;Analysis Services-多維度資料 &#41;](../../../analysis-services/multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md)  
  
  
