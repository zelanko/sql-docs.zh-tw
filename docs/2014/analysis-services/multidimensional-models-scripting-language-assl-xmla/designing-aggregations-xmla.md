---
title: 設計彙總 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- statistical information [XML for Analysis]
- batches [XML for Analysis]
- aggregations [Analysis Services], XML for Analysis
- XMLA, aggregations
- queries [XMLA]
- XML for Analysis, aggregations
- iterative aggregation process [XMLA]
ms.assetid: 4dd27afa-10c7-408d-bc24-ca74217ddbcb
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 71abb7339a45e86e39329f6f5e9478d03889c71b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48094758"
---
# <a name="designing-aggregations-xmla"></a>設計彙總 (XMLA)
  彙總設計會與特定量值群組的資料分割關聯，以確保資料分割在儲存彙總時會使用相同的結構。 資料分割使用相同的儲存體結構可讓您輕鬆地定義 合併資料分割可以稍後使用[MergePartitions](../xmla/xml-elements-commands/mergepartitions-element-xmla.md)命令。 如需有關彙總設計的詳細資訊，請參閱[彙總及彙總設計](../multidimensional-models-olap-logical-cube-objects/aggregations-and-aggregation-designs.md)。  
  
 若要定義的彙總設計的彙總，您可以使用[DesignAggregations](../xmla/xml-elements-commands/designaggregations-element-xmla.md) XML for Analysis (XMLA) 命令。 `DesignAggregations` 命令具有一些屬性，可識別要使用哪個彙總設計做為參考，以及如何根據該參考控制設計程序。 使用 `DesignAggregations` 命令及其屬性，您可以反覆或用批次方式設計彙總，然後檢視產生的設計統計資料以評估設計程序。  
  
## <a name="specifying-an-aggregation-design"></a>指定彙總設計  
 [物件](../xmla/xml-elements-properties/object-element-xmla.md)屬性`DesignAggregations`命令必須包含現有的彙總設計的物件參考。 物件參考包含資料庫識別碼、Cube 識別碼、量值群組識別碼以及彙總設計識別碼。 如果彙總設計尚未存在，就會發生錯誤。  
  
## <a name="controlling-the-design-process"></a>控制設計程序  
 您可以使用 `DesignAggregations` 命令的下列屬性來控制為彙總設計定義彙總的演算法。  
  
-   [步驟](../xmla/xml-elements-properties/steps-element-xmla.md)屬性會決定多少反覆項目`DesignAggregations`命令應該花費，它將控制權還給用戶端應用程式。  
  
-   [時間](../xmla/xml-elements-properties/time-element-xmla.md)屬性會決定多少毫秒`DesignAggregations`命令應該花費，它將控制權還給用戶端應用程式。  
  
-   [最佳化](../xmla/xml-elements-properties/optimization-element-xmla.md)屬性會決定的效能改善估計的百分比`DesignAggregations`命令應該嘗試達成。 如果您反覆設計彙總，只需要在第一個命令上傳送此屬性。  
  
-   [儲存體](../xmla/xml-elements-properties/storage-element-xmla.md)屬性會決定磁碟儲存體，以位元組為單位，所使用的預估的量`DesignAggregations`命令。 如果您反覆設計彙總，只需要在第一個命令上傳送此屬性。  
  
-   [具體化](../xmla/xml-elements-properties/materialize-element-xmla.md)屬性會決定是否`DesignAggregations`命令應該建立在設計程序期間所定義的彙總。 如果您反覆地設計彙總，此屬性應該設定為 False，直到您準備儲存設計的彙總為止。 當設定為 True 時，目前的設計程序會結束，而定義的彙總會加入指定的彙總設計。  
  
## <a name="specifying-queries"></a>指定查詢  
 DesignAggregations 命令包含一或多個支援基於使用方式的最佳化命令`Query`中的項目[查詢](../xmla/xml-elements-properties/queries-element-xmla.md)屬性。 `Queries`屬性可包含一或多個[查詢](../xmla/xml-elements-properties/query-element-xmla.md)項目。 如果 `Queries` 屬性不包含任何 `Query` 元素，在 `Object` 元素中指定的彙總設計，會使用包含一組一般彙總的預設結構。 這組一般彙總的設計，是為了符合在 `Optimization` 命令的 `Storage` 與 `DesignAggregations` 屬性中所指定的準則。  
  
 每個`Query`項目代表一個目標查詢，使用定義目標最常用的查詢的彙總設計程序。 您可以指定您自己的目標查詢，或者您可以使用的執行個體所儲存的資訊[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]來擷取有關最常用的查詢記錄中使用的查詢。 「基於使用方式的最佳化精靈」會在傳送 `DesignAggregations` 命令時，依據時間、使用方式或是指定的使用者，使用查詢記錄擷取目標查詢。 如需詳細資訊，請參閱 <<c0> [ 基於使用方式的最佳化精靈 F1 說明](../usage-based-optimization-wizard-f1-help.md)。  
  
 如果您反覆設計彙總，您只需要將目標查詢傳入第一個`DesignAggregations`命令即可，因為[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]執行個體儲存這些目標查詢，並在後續的期間使用這些查詢`DesignAggregations`命令。 當您將目標查詢傳入反覆處理序的第一個 `DesignAggregations` 命令之後，任何在 `DesignAggregations` 屬性中包含目標查詢的後續 `Queries` 命令就會產生錯誤。  
  
 `Query` 元素包含具有下列引數的逗號分隔值：  
  
 *Frequency*,*Dataset*[,*Dataset*...]  
  
 *頻率*  
 對應至查詢先前執行次數的加權因數。 如果`Query`項目代表新的查詢中，*頻率*值代表設計處理序用來評估查詢的加權因數。 當頻率值變大時，在設計處理序期間放置於查詢的加權就會增加。  
  
 *資料集*  
 指定維度的哪些屬性要包含在查詢中的數值字串。 這個字串必須與維度中的屬性數目具有相同的字元數目。 零 (0) 表示指定之序數位置中的屬性沒有包含在指定維度的查詢中，而一 (1) 則表示指定之序數位置中的屬性已包含在指定維度的查詢中。  
  
 例如，字串 "011" 是指涉及含有三個屬性之維度的查詢，其中第二和第三個屬性包含在查詢中。  
  
> [!NOTE]  
>  某些屬性會從資料集的考量中排除。 如需有關排除屬性的詳細資訊，請參閱 <<c0> [ 查詢項目&#40;XMLA&#41;](../xmla/xml-elements-properties/query-element-xmla.md)。</c0>  
  
 在包含彙總設計的量值群組中的每個維度由*資料集*中的值`Query`項目。 *Dataset* 值的順序必須與量值群組中包含維度的順序相符。  
  
## <a name="designing-aggregations-using-iterative-or-batch-processes"></a>使用反覆或批次程序來設計彙總  
 您可以在反覆程序或是批次程序中使用 `DesignAggregations` 命令，端視設計程序所需的互動性而定。  
  
### <a name="designing-aggregations-using-an-iterative-process"></a>使用反覆程序來設計彙總  
 若要反覆設計彙總，您可以傳送多個 `DesignAggregations` 命令，以提供設計程序的良好控制。 「彙總設計精靈」使用這個相同的方法來提供設計程序的良好控制。 如需詳細資訊，請參閱 <<c0> [ 彙總設計精靈 F1 說明](../aggregation-design-wizard-f1-help.md)。  
  
> [!NOTE]  
>  需要明確的工作階段，以反覆設計彙總。 如需有關明確工作階段的詳細資訊，請參閱[管理連接和工作階段&#40;XMLA&#41;](managing-connections-and-sessions-xmla.md)。  
  
 若要開始反覆程序，請先傳送包含下列資訊的 `DesignAggregations` 命令：  
  
-   以整個設計程序為目標的 `Storage` 與 `Optimization` 屬性值。  
  
-   限制設計程序之第一個步驟的 `Steps` 與 `Time` 屬性值。  
  
-   如果您想要基於使用方式的最佳化，還要提供 `Queries` 屬性，其中包含整個設計程序的目標查詢。  
  
-   設定為 False 的 `Materialize` 屬性。 將此屬性設定為 False，表示設計程序不會在命令完成時將定義的彙總儲存至彙總設計。  
  
 當第一個 `DesignAggregations` 命令完成時，命令會傳回包含設計統計資料的資料列集。 您可以評估這些設計統計資料，以判斷設計程序是否應該繼續或者設計程序是否已完成。 如果程序應該繼續，則請傳送另一個 `DesignAggregations` 命令，以包含限制設計程序此步驟的 `Steps` 與 `Time` 值。 您可以評估產生的統計資料，然後判斷設計程序是否應該繼續。 傳送 `DesignAggregations` 命令與評估結果的反覆程序會繼續，直到您達成目標並且有一組適當定義的彙總為止。  
  
 在您達到所需的彙總之後，傳送最後一次的 `DesignAggregations` 命令。 這個最後的 `DesignAggregations` 命令應該將 `Steps` 屬性設定為 1，並將其 `Materialize` 屬性設定為 True。 透過使用這些設定，這個最後的 `DesignAggregations` 命令會完成設計程序，並將定義的彙總儲存到彙總設計。  
  
### <a name="designing-aggregations-using-a-batch-process"></a>使用批次程序來設計彙總  
 您也可以透過傳送單一 `DesignAggregations` 命令，以包含以整個設計程序為目標並使其受限的 `Steps`、`Time`、`Storage` 和 `Optimization` 屬性值，從而在批次程序中設計彙總。 如果您想要基於使用方式的最佳化，以設計程序為目標的目標查詢也應該包含在 `Queries` 屬性中。 另外請確定 `Materialize` 屬性是設定為 True，這樣設計程序就會在命令完成時，將定義的彙總儲存到彙總設計。  
  
 您可以在隱含或明確的工作階段中使用批次程序來設計彙總。 如需有關隱含和明確工作階段的詳細資訊，請參閱 <<c0> [ 管理連接和工作階段&#40;XMLA&#41;](managing-connections-and-sessions-xmla.md)。</c0>  
  
## <a name="returning-design-statistics"></a>傳回設計統計資料  
 當 `DesignAggregations` 命令將控制權還給用戶端應用程式時，命令會傳回包含單一資料列的資料列集，該資料列代表命令的設計統計資料。 資料列集包含下表中列出的資料行。  
  
|「資料行」|資料類型|描述|  
|------------|---------------|-----------------|  
|步驟|Integer|在將控制權還給用戶端應用程式之前，命令所使用的步驟數目。|  
|Time|長整數|在將控制權還給用戶端應用程式之前，命令所花費的毫秒數目。|  
|Optimization|Double|在將控制權還給用戶端應用程式之前，命令所達成的效能改善估計百分比。|  
|Storage|長整數|在將控制權還給用戶端應用程式之前，命令所使用的位元組估計數目。|  
|Aggregations|長整數|在將控制權還給用戶端應用程式之前，命令所定義的彙總數目。|  
|LastStep|布林|指出在資料列集中的資料是否代表設計程序中的最後一個步驟。 如果命令的 `Materialize` 屬性設定為 True，就會將這個資料行值設定為 True。|  
  
 您可以將每一個 `DesignAggregations` 命令之後傳回的資料列集內所含的設計統計資料用在反覆設計或批次設計。 在反覆設計中，您可以使用設計統計資料以判斷和顯示進度。 當您以批次方式設計彙總時，可以使用設計統計資料來判斷命令所建立的彙總數目。  
  
## <a name="see-also"></a>另請參閱  
 [在 Analysis Services 中使用 XMLA 進行開發](developing-with-xmla-in-analysis-services.md)  
  
  
