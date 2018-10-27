---
title: 設計彙總 (XMLA) |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b9f681b3c99bd0e8351a844f28b16be6249de199
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/26/2018
ms.locfileid: "50147183"
---
# <a name="designing-aggregations-xmla"></a>設計彙總 (XMLA)
  彙總設計會與特定量值群組的資料分割關聯，以確保資料分割在儲存彙總時會使用相同的結構。 資料分割使用相同的儲存體結構可讓您輕鬆地定義 合併資料分割可以稍後使用[MergePartitions](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/mergepartitions-element-xmla)命令。 如需有關彙總設計的詳細資訊，請參閱[彙總及彙總設計](../../analysis-services/multidimensional-models-olap-logical-cube-objects/aggregations-and-aggregation-designs.md)。  
  
 若要定義的彙總設計的彙總，您可以使用[DesignAggregations](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/designaggregations-element-xmla) XML for Analysis (XMLA) 命令。 **DesignAggregations**命令具有識別哪一個彙總設計，以做為參考，以及如何控制設計程序，根據該參考的屬性。 使用**DesignAggregations**命令和其屬性，您可以反覆或批次中設計彙總，然後檢視 產生的設計統計資料，以評估設計程序。  
  
## <a name="specifying-an-aggregation-design"></a>指定彙總設計  
 [物件](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla)屬性**DesignAggregations**命令必須包含現有的彙總設計的物件參考。 物件參考包含資料庫識別碼、Cube 識別碼、量值群組識別碼以及彙總設計識別碼。 如果彙總設計尚未存在，就會發生錯誤。  
  
## <a name="controlling-the-design-process"></a>控制設計程序  
 您可以使用的下列屬性**DesignAggregations**命令，以控制用來彙總設計定義彙總的演算法：  
  
-   [步驟](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/steps-element-xmla)屬性會決定多少反覆項目**DesignAggregations**命令應該花費，它將控制權還給用戶端應用程式。  
  
-   [時間](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/time-element-xmla)屬性會決定多少毫秒**DesignAggregations**命令應該花費，它將控制權還給用戶端應用程式。  
  
-   [最佳化](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/optimization-element-xmla)屬性會決定的效能改善估計的百分比**DesignAggregations**命令應該嘗試達成。 如果您反覆設計彙總，只需要在第一個命令上傳送此屬性。  
  
-   [儲存體](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/storage-element-xmla)屬性會決定磁碟儲存體，以位元組為單位，所使用的預估的量**DesignAggregations**命令。 如果您反覆設計彙總，只需要在第一個命令上傳送此屬性。  
  
-   [具體化](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/materialize-element-xmla)屬性會決定是否**DesignAggregations**命令應該建立在設計程序期間所定義的彙總。 如果您反覆地設計彙總，此屬性應該設定為 False，直到您準備儲存設計的彙總為止。 當設定為 True 時，目前的設計程序會結束，而定義的彙總會加入指定的彙總設計。  
  
## <a name="specifying-queries"></a>指定查詢  
 DesignAggregations 命令包含一或多個支援基於使用方式的最佳化命令**查詢**中的項目[查詢](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/queries-element-xmla)屬性。 **查詢**屬性可包含一或多個[查詢](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/query-element-xmla)項目。 如果**查詢**屬性不包含任何**查詢**中指定的項目，彙總設計**物件**項目會使用預設的結構，其中包含組一般彙總。 這組一般彙總的設計符合中指定的準則**最佳化**並**儲存體**的屬性**DesignAggregations**命令。  
  
 每個 **Query** 元素都代表一個目標查詢，而且設計處理序會使用此查詢來定義以最常用查詢為目標的彙總。 您可以指定自己的目標查詢，也可以使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體在查詢記錄中儲存的資訊來擷取有關最常用查詢的資訊。 「 基於使用方式的最佳化精靈 」 會使用查詢記錄擷取目標查詢，會在傳送時，根據時間、 使用方式或指定的使用者**DesignAggregations**命令。 如需詳細資訊，請參閱 <<c0> [ 基於使用方式的最佳化精靈 F1 說明](http://msdn.microsoft.com/library/e5f5a938-ae7c-4f4e-9416-a7f94ac82763)。  
  
 如果您要反覆地設計彙總，只需要將目標查詢傳入第一個 **DesignAggregations** 命令即可，因為 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體會儲存這些目標查詢，然後在後續的 **DesignAggregations** 命令執行期間使用這些查詢。 當您將目標查詢傳入反覆處理序的第一個 **DesignAggregations** 命令之後，任何在 **DesignAggregations** 屬性中包含目標查詢的後續 **Queries** 命令就會產生錯誤。  
  
 **Query** 元素包含具有下列引數的逗號分隔值：  
  
 *Frequency*,*Dataset*[,*Dataset*...]  
  
 *頻率*  
 對應至查詢先前執行次數的加權因數。 如果 **Query** 元素代表新的查詢， *Frequency* 值就代表設計處理序用來評估查詢的加權因數。 當頻率值變大時，在設計處理序期間放置於查詢的加權就會增加。  
  
 *資料集*  
 指定維度的哪些屬性要包含在查詢中的數值字串。 這個字串必須與維度中的屬性數目具有相同的字元數目。 零 (0) 表示指定之序數位置中的屬性沒有包含在指定維度的查詢中，而一 (1) 則表示指定之序數位置中的屬性已包含在指定維度的查詢中。  
  
 例如，字串 "011" 是指涉及含有三個屬性之維度的查詢，其中第二和第三個屬性包含在查詢中。  
  
> [!NOTE]  
>  某些屬性會從資料集的考量中排除。 如需有關排除屬性的詳細資訊，請參閱 <<c0> [ 查詢項目&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/query-element-xmla)。</c0>  
  
 量值群組中包含彙總設計的每個維度是由 *Query* 元素中的 **Dataset** 值代表。 *Dataset* 值的順序必須與量值群組中包含維度的順序相符。  
  
## <a name="designing-aggregations-using-iterative-or-batch-processes"></a>使用反覆或批次程序來設計彙總  
 您可以使用**DesignAggregations**命令為反覆的程序或批次程序，根據設計程序所需的互動功能的一部分。  
  
### <a name="designing-aggregations-using-an-iterative-process"></a>使用反覆程序來設計彙總  
 若要反覆設計彙總，您可以傳送多個**DesignAggregations**命令，以讓設計程序的良好控制。 「彙總設計精靈」使用這個相同的方法來提供設計程序的良好控制。 如需詳細資訊，請參閱 <<c0> [ 彙總設計精靈 F1 說明](http://msdn.microsoft.com/library/39e23cf1-6405-4fb6-bc14-ba103314362d)。  
  
> [!NOTE]  
>  需要明確的工作階段，以反覆設計彙總。 如需有關明確工作階段的詳細資訊，請參閱[管理連接和工作階段&#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)。  
  
 若要開始反覆程序，您必須先傳送**DesignAggregations**命令，以包含下列資訊：  
  
-   **儲存體**並**最佳化**屬性值在整個設計程序為目標。  
  
-   **步驟**並**時間**所在設計程序的第一個步驟是有限的屬性值。  
  
-   如果您想要基於使用方式的最佳化，**查詢**屬性，其中包含目標查詢，在整個設計程序為目標。  
  
-   **具體化**屬性設為 false。 將此屬性設定為 False，表示設計程序不會在命令完成時將定義的彙總儲存至彙總設計。  
  
 當第一個**DesignAggregations**命令完成時，此命令會傳回包含設計統計資料的資料列集。 您可以評估這些設計統計資料，以判斷設計程序是否應該繼續或者設計程序是否已完成。 如果應該繼續處理程序，您再傳送另一個**DesignAggregations**命令，以包含**步驟**並**時間**與其設計的這個步驟所處理的值會受到限制。 您可以評估產生的統計資料，然後判斷設計程序是否應該繼續。 此反覆的程序，傳送**DesignAggregations**命令與評估結果會繼續執行直到您達成目標並且有一組適當定義的彙總。  
  
 您已達到您想要的彙總的集合之後，您就會傳送最後一次**DesignAggregations**命令。 這個最後**DesignAggregations**命令應該有其**步驟**屬性設定為 1 且其**具體化**屬性設定為 true。 使用這些設定，這個最後**DesignAggregations**命令完成設計程序，並將彙總設計定義彙總。  
  
### <a name="designing-aggregations-using-a-batch-process"></a>使用批次程序來設計彙總  
 您也可以透過傳送單一設計批次程序中的彙總**DesignAggregations**命令，以包含**步驟**，**時間**，**儲存體**，並**最佳化**屬性值設為目標並受限於整個設計程序。 如果您想要基於使用方式的最佳化，在其設計程序為目標的目標查詢也應該包含在**查詢**屬性。 此外，請確定**具體化**屬性設為 true，以便設計程序會儲存到彙總設計定義彙總在命令完成時。  
  
 您可以在隱含或明確的工作階段中使用批次程序來設計彙總。 如需有關隱含和明確工作階段的詳細資訊，請參閱 <<c0> [ 管理連接和工作階段&#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)。</c0>  
  
## <a name="returning-design-statistics"></a>傳回設計統計資料  
 當**DesignAggregations**命令會將控制權還給用戶端應用程式，此命令會傳回包含單一資料列代表命令的設計統計資料的資料列集。 資料列集包含下表中列出的資料行。  
  
|「資料行」|資料類型|描述|  
|------------|---------------|-----------------|  
|步驟|Integer|在將控制權還給用戶端應用程式之前，命令所使用的步驟數目。|  
|Time|長整數|在將控制權還給用戶端應用程式之前，命令所花費的毫秒數目。|  
|Optimization|Double|在將控制權還給用戶端應用程式之前，命令所達成的效能改善估計百分比。|  
|Storage|長整數|在將控制權還給用戶端應用程式之前，命令所使用的位元組估計數目。|  
|Aggregations|長整數|在將控制權還給用戶端應用程式之前，命令所定義的彙總數目。|  
|LastStep|布林|指出在資料列集中的資料是否代表設計程序中的最後一個步驟。 如果**具體化**命令的屬性已設為此資料行的值設為 true，則為 true。|  
  
 您可以使用設計統計資料包含在每個傳回資料列集中**DesignAggregations**命令在反覆或批次設計。 在反覆設計中，您可以使用設計統計資料以判斷和顯示進度。 當您以批次方式設計彙總時，可以使用設計統計資料來判斷命令所建立的彙總數目。  
  
## <a name="see-also"></a>另請參閱  
 [在 Analysis Services 中使用 XMLA 進行開發](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
