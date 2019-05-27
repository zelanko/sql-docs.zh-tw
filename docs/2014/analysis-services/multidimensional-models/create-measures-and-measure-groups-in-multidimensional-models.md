---
title: 多維度模型中建立量值和量值群組 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- measure groups [Analysis Services], defining
ms.assetid: 1018bb2e-b89b-489e-aead-450dec5dca3b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2883a9092f7b84e8dd18954cec631b90a8bbe0e9
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66076244"
---
# <a name="create-measures-and-measure-groups-in-multidimensional-models"></a>在多維度模型中建立量值和量值群組
  *「量值」* (measure) 是數值資料值的彙總，包括總和、計數、最小值、最大值、平均值或您建立的自訂 MDX 運算式。 *「量值群組」* (measure group) 是包含一個或多個量值的容器。 所有量值都存在量值群組中，即使只有一個量值。 Cube 必須具有至少一個量值與量值群組。  
  
 本主題包含下列各節：  
  
-   [建立量值的方法](#bkmk_create)  
  
-   [量值的元件](#bkmk_comps)  
  
-   [模型化代表事實和事實資料表的量值與量值群組](#bkmk_modeling)  
  
-   [量值群組的資料粒度](#bkmk_grain)  
  
##  <a name="bkmk_create"></a> 建立量值的方法  
 量值可以是 Cube 的靜態項目，於設計階段建立，而且無論何時存取 Cube，都會一直存在。 您也可以使用多維度運算式 (MDX)，將量值定義為 *「導出成員」* (calculated member)，以根據 Cube 中的其他量值，提供量值的導出值。 導出成員可以限定在工作階段或使用者。  
  
 若要建立量值或量值群組，可使用其中一種方法：  
  
|||  
|-|-|  
|Cube 精靈|在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中執行 [Cube 精靈]，以建立 Cube。<br /><br /> 在方案總管中，以滑鼠右鍵按一下 [Cube]，然後選擇 [新增 Cube]。 如需這些步驟的說明，請參閱[多維度模型化 &#40;Adventure Works 教學課程&#41;](../multidimensional-modeling-adventure-works-tutorial.md)。<br /><br /> 當您以現有之資料倉儲的資料表為基礎建立 Cube 時，量值和量值群組會在建立 Cube 時具體化。 您會在精靈中選擇事實及事實資料表，以用為 Cube 中之量值及量值群組物件的基礎。|  
|[新增量值] 對話方塊|假設 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中已有此 Cube，在 [方案總管] 中按兩下此 Cube 的名稱，即可在 Cube 設計師中開啟此 Cube。 在 [量值] 窗格中，於最上層節點上按一下滑鼠右鍵，以建立新的量值群組，或指定來源資料表、資料行及彙總類型，以建立新的量值。 使用這種方法必須從預先建置的函數固定清單中選擇彙總方法。 如需更常用之彙總方法的討論，請參閱＜ [Use Aggregate Functions](use-aggregate-functions.md) ＞。|  
|「導出成員」|因為您可以控制導出成員的建立時機及方式，所以導出成員可為 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中的 Cube 增加彈性及分析功能。 有時候您可能只是暫時需要量值，在使用者工作階段或調查期間的 Management Studio 階段中使用。<br /><br /> 在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中開啟 [計算] 索引標籤，以建立新的導出成員。<br /><br /> 當基礎為 MDX 運算式中的量值時，請選擇此方法。 請參閱這些主題，如需詳細資訊：[建置在 MDX 中的量值](mdx/mdx-building-measures.md)，[計算](../multidimensional-models-olap-logical-cube-objects/calculations.md)，[多維度模型中的計算](calculations-in-multidimensional-models.md)並[MDX 指令碼基礎觀念&#40;Analysis Services&#41;](mdx/mdx-scripting-fundamentals-analysis-services.md).|  
|MDX 或 XMLA|在 SQL Server Management Studio 中，您可以執行 MDX 或 XMLA 來更改資料庫，以加入新的導出量值。 這種方法可在解決方案部署到伺服器之後，於特定的資料測試時使用。 請參閱 [Document and Script an Analysis Services Database](document-and-script-an-analysis-services-database.md)。|  
  
##  <a name="bkmk_comps"></a> 量值的元件  
 量值是具有屬性的物件。 除了名稱，量值還必須具備彙總類型和來源資料行，或是用於載入包含資料之量值的運算式。 您可以藉由設定屬性來修改量值定義。  
  
|||  
|-|-|  
|**來源**|大部分量值來自於外部資料倉儲中之事實資料表中的數值資料行，例如 AdventureWorks 資料倉儲中「網際網路銷售」和「轉售商銷售」資料表中的「銷售量」資料行；但您也可以完全依據您所定義的計算來建立新的量值。<br /><br /> 維度資料表中的屬性資料行也可以用來定義量值，但從其彙總行為上來看，這類量值通常為局部加總或不加總。 如需局部加總行為的詳細資訊，請參閱 [Define Semiadditive Behavior](define-semiadditive-behavior.md)(定義局部加總行為)。|  
|**彙總 (aggregation)**|依預設，會沿著每個維度來加總量值。 然而，`AggregateFunction` 屬性可讓您修改這個行為。 如需清單，請參閱＜ [Use Aggregate Functions](use-aggregate-functions.md) ＞。|  
|**屬性**|如需其他屬性說明，請參閱＜ [Configure Measure Properties](configure-measure-properties.md) ＞。|  
  
##  <a name="bkmk_modeling"></a> 模型化代表事實和事實資料表的量值與量值群組  
 執行精靈之前，請務必先了解量值定義背後的模型化原則。  
  
 量值和量值群組是代表外部資料倉儲中之事實和事實資料表的多維度物件。 在大多數情況下，量值和量值群組會以資料來源檢視中的物件為基礎，而這些物件會依序從基礎資料倉儲建立。  
  
 下圖代表 **FactSalesQuota** 事實資料表和相關的兩個維度資料表 ( **DimTime** 和 **DimEmployee**)。 在 Adventure Works 範例 Cube 中，這些資料表會作為「銷售配額」量值群組與「時間」及「員工」維度的根據。  
  
 ![具有兩個維度資料表的 FactSalesQuota 資料表](../media/factsalesquota.gif "具有兩個維度資料表的 FactSalesQuota 資料表")  
  
 事實資料表包含兩個基本類型的資料行：屬性資料行和量值資料行。  
  
-   屬性資料行是用來建立外部索引鍵與維度資料表的關聯性，因此，量值資料行中的可量化資料，可由維度資料表包含的資料加以組織。 屬性資料行也可用來定義事實資料表及其量值群組的資料粒度。  
  
-   量值資料行定義量值群組包含的量值。  
  
 當您執行 [Cube 精靈] 時，外部索引鍵會被篩選掉。在剩餘可選之資料行的清單中，除了會顯示量值資料行之外，還會顯示未對應外部索引鍵的屬性資料行。 在 **FactSalesQuote** 範例中，精靈不只會提供除了 **SalesAmountQuota** ，還會提供 **CalendarYear** 及 **CalendarQuarter**。 只有 **SalesAmountQuota** 量值資料行會產生可供您多維度模型使用的量值。 其他日期資料行的用途，只在限定每個配額量。 您應從 [Cube 精靈] 的量值清單中，排除其他資料行 **CalendarYear** 和 **CalendarQuarter**(或稍後透過設計工具從從量值群組中移除)。  
  
 這個討論所要強調的重點是，並非精靈所提供的所有資料行都可用為量值。 這取決於您決定要用為量值的資料行時，對於資料的了解及其之後的用法。 請注意，您可以在資料來源檢視中的資料表上按一下滑鼠右鍵來探索資料，以協助您了解哪些資料行可以用為量值。 如需詳細資訊，請參閱 [Explore Data in a Data Source View &#40;Analysis Services&#41;](explore-data-in-a-data-source-view-analysis-services.md) (在資料來源檢視中瀏覽資料 (Analysis Services))。  
  
> [!NOTE]  
>  並非所有量值都是直接衍生自事實資料表的資料行所儲存的值。 例如，Adventure Works 範例 Cube 之 **Sales Quota** 量值群組中所定義的 **Sales Person Count** 量值，實際上會以 **FactSalesQuota** 事實資料表之 **EmployeeKey** 資料行中的唯一值 (或相異計數) 為基礎。  
  
##  <a name="bkmk_grain"></a> 量值群組的資料粒度  
 量值群組的資料粒度與事實資料表所支援的詳細資料層級相關聯。 資料粒度必須透過維度的外部索引鍵關聯性進行設定。  
  
 例如 **FactSalesQuota** 事實資料表具有 **DimEmployee** 資料表的外部索引鍵關聯性，而 **FactSalesQuota** 資料表中的每筆記錄都會關聯到一位員工；如此情況下，當從「員工」維度檢視此量值群組的資料粒度時，所見內容皆為個別員工的層級。  
  
 量值群組的資料粒度絕不可設定為小於用來檢視量值群組之維度的最低層級，但可使用其他屬性將資料粒度設定為更粗一點。 例如， **FactSalesQuota** 事實資料表使用 **TimeKey**、 **CalendarYear**和 **CalendarQuarter**這三個資料行來建立與 **DimTime** 資料表之關聯性的資料粒度。 因此，從 [時間] 維度檢視之量值群組的資料粒度是依據日曆季，而不是依據 [時間] 維度的最低層級：日。  
  
 您可以使用 Cube 設計師的 **[維度使用方式]** 索引標籤，來指定與特定維度相關之量值群組的資料粒度。 如需有關維度關聯性的詳細資訊，請參閱＜ [Dimension Relationships](../multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)＞。  
  
## <a name="see-also"></a>另請參閱  
 [多維度模型中的 Cube](cubes-in-multidimensional-models.md)   
 [量值和量值群組](measures-and-measure-groups.md)  
  
  
