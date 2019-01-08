---
title: 內容查詢 （資料採礦） |Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 20d730ed2fd975d800b27882ecc218f7ce1868b3
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52529056"
---
# <a name="content-queries-data-mining"></a>內容查詢 (資料採礦)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  內容查詢是一種擷取採礦模型之內部統計資料和結構相關資訊的方法。 內容查詢有時候可以提供檢視器中無法隨時取得的詳細資料。 您也可以使用內容查詢的結果，以程式設計的方式擷取其他用途的資訊。  
  
 本節提供有關可使用內容查詢擷取之資訊類型，以及內容查詢之一般 DMX 語法的一般資訊。  
  
 [基本內容查詢](#bkmk_ContentQuery)  
  
-   [結構和案例資料的查詢](#bkmk_Structure)  
  
-   [模型模式的查詢](#bkmk_Patterns)  
  
 [範例](#bkmk_Examples)  
  
-   [關聯模型的內容查詢](#bkmk_Assoc)  
  
-   [決策樹模型的內容查詢](#bkmk_DecTree)  
  
 [使用查詢結果](#bkmk_Results)  
  
##  <a name="bkmk_ContentQuery"></a> 基本內容查詢  
 您可以使用預測查詢產生器建立內容查詢、使用 SQL Server Management Studio 隨附的 DMX 內容查詢範本，或是直接以 DMX 撰寫查詢。 與預測查詢不同的是，您不需要聯結外部資料，因此可以輕鬆撰寫內容查詢。  
  
 本節提供您可以建立的內容查詢類型概觀。  
  
-   採礦結構或案例資料的查詢可讓您檢視用於定型的詳細資料。  
  
-   模型的查詢可以傳回模式、屬性清單、公式等。  
  
###  <a name="bkmk_Structure"></a> 結構和案例資料的查詢  
 DMX 支援對用來建立採礦結構和模型的快取資料進行查詢。 當您定義採礦結構時，預設會建立此快取，並在您處理結構或模型時擴展快取。  
  
> [!WARNING]  
>  如果您需要將資料分成定型集和測試集，請勿清除或刪除此快取。 如果清除快取，則無法查詢案例資料。  
  
 下列範例示範建立案例資料之查詢或是查詢採礦結構中之資料的常見模式：  
  
 **取得模型的所有案例**  
 `SELECT FROM <model>.CASES`  
  
 使用此陳述式可從用來建立模型的案例資料中，擷取指定的資料行。 您必須具有模型的鑽研權限，才能執行此查詢。  
  
 **檢視所有包含在結構中的資料。**  
 `SELECT FROM <structure>.CASES`  
  
 使用此陳述式可檢視所有包含在結構中的資料，包括未包含在特定採礦模型中的資料行。 您必須具有模型及結構的鑽研權限，才能從採礦結構中擷取資料。  
  
 **取得值範圍**  
 `SELECT DISTINCT RangeMin(<column>), RangeMax(<column>) FROM <model>`  
  
 使用此陳述式可尋找連續資料行或 DISCRETIZED 資料行值區的最小值、最大值及平均值。  
  
 **取得相異值**  
 `SELECT DISTINCT <column>FROM <model>`  
  
 使用此陳述式可擷取 DISCRETE 資料行的所有值。  不要對 DISCRETIZED 資料行使用這個陳述式，應改用 **RangeMin** 和 **RangeMax** 函數。  
  
 **尋找用來定型模型或結構的案例**  
 `SELECT  FROM <mining structure.CASES WHERE IsTrainingCase()`  
  
 使用此陳述式可取得一組用來定型模型的完整資料。  
  
 **尋找用來測試模型或結構的案例**  
 `SELECT  FROM <mining structure.CASES WHERE IsTestingCase()`  
  
 使用此陳述式可取得保留給與特定結構相關之測試採礦模型的資料。  
  
 **從特定模型模式鑽研到基礎案例資料**  
 `SELECT FROM <model>.CASESWHERE IsTrainingCase() AND IsInNode(<node>)`  
  
 使用此陳述式可從定型模型中擷取詳細的案例資料。 您必須指定特定節點：例如，您必須知道叢集的節點識別碼、決策樹的特定分支等。此外，您也必須擁有模型的鑽研權限，才能執行此查詢。  
  
###  <a name="bkmk_Patterns"></a> 模型模式、統計資料及屬性的查詢  
 資料採礦模型的內容有多種用途。 您可以使用模型內容查詢執行以下作業：  
  
-   擷取公式或機率來進行自己的計算。  
  
-   針對關聯模型，擷取用來產生預測的規則。  
  
-   擷取特定規則的描述，以便在自訂應用程式中使用規則。  
  
-   檢視時間序列模型偵測到的移動平均。  
  
-   取得趨勢線之某個線段的迴歸公式。  
  
-   擷取有關客戶識別為屬於特定叢集的可付諸行動之資訊。  
  
 下列範例顯示用來建立模型內容查詢的一些常見模式：  
  
 **取得模型中的模式**  
 `SELECT FROM <model>.CONTENT`  
  
 使用此陳述式可擷取模型中特定節點的詳細資訊。 視演算法類型而定，節點可以包含規則和公式、支援和變異數統計資料等等。  
  
 **擷取定型模型中所使用的屬性**  
 `CALL System.GetModelAttributes(<model>)`  
  
 使用此預存程序可擷取模型所使用的屬性清單。 例如，這項資訊可用於決定因特徵選取而刪除的屬性。  
  
 **擷取儲存在資料採礦維度中的內容**  
 `SELECT FROM <model>.DIMENSIONCONTENT`  
  
 使用此陳述式可從資料採礦維度中擷取資料。  
  
 這個查詢類型主要供內部使用。 但是，並非所有的演算法都支援這項功能。 支援是由 MINING_SERVICES 結構描述資料列集中的旗標所代表。  
  
 如果您開發自己的外掛程式演算法，可以使用此陳述式來確認用於測試的模型內容。  
  
 **取得模型的 PMML 表示**  
 `SELECT * FROM <model>.PMML`  
  
 取得以 PMML 格式表示模型的 XML 文件。 並非所有模型類型都受到支援。  
  
##  <a name="bkmk_Examples"></a> 範例  
 雖然在不同的演算法中會有一些標準的模型內容，但是內容的某些部分會因為用來建立模型的演算法而有很大的差異。 因此，當您建立內容查詢時，必須了解模型中有哪些資訊對於特定模型最有用。  
  
 本節提供幾個範例，以便說明演算法的選擇如何影響模型內所儲存的資訊類型。 如需採礦模型內容以及每一個模型類型特有之內容的詳細資訊，請參閱 [Mining Model Content &#40;Analysis Services - Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-analysis-services-data-mining.md)。  
  
###  <a name="bkmk_Assoc"></a> 範例 1:關聯模型的內容查詢  
 `SELECT FROM <model>.CONTENT`陳述式會根據您所查詢的模型類型傳回不同種類的資訊。 如果是關聯模型，資訊的主要片段為 *「節點類型」*(Node Type)。 節點類似於模型內容中資訊的容器。 在關聯模型中，代表規則之節點的 NODE_TYPE 值為 8，而代表項目集之節點的 NODE_TYPE 值則為 7。  
  
 因此，下列查詢會傳回前 10 個項目集，並依照支援排序 (預設的排序)。  
  
```  
SELECT TOP 10 NODE_DESCRIPTION, NODE_PROBABILITY, SUPPORT  
FROM <model>.CONTENT WHERE NODE_TYPE = 7  
```  
  
 下列查詢會根據這項資訊。 此查詢會傳回三個資料行： 節點、 完整的規則和項目集右側產品的識別碼-也就是預測為與某些其他產品相關聯的項目集一部分的產品。  
  
```  
SELECT FLATTENED NODE_UNIQUE_NAME, NODE_DESCRIPTION,  
     (SELECT RIGHT(ATTRIBUTE_NAME, (LEN(ATTRIBUTE_NAME)-LEN('Association model name')))   
FROM NODE_DISTRIBUTION  
WHERE LEN(ATTRIBUTE_NAME)>2  
)   
AS RightSideProduct  
FROM [<Association model name>].CONTENT  
WHERE NODE_TYPE = 8   
ORDER BY NODE_SUPPORT DESC  
```  
  
 FLATTENED 關鍵字代表巢狀資料列集應該轉換成扁平化資料表。 代表規則右側產品的屬性包含在 NODE_DISTRIBUTION 資料表中；因此，我們會加入長度必須大於 2 的需求，只擷取包含屬性名稱的資料列。  
  
 簡單字串函數是用來移除第三個資料行的模型名稱 (通常模型名稱會加到巢狀資料行值的前面)。  
  
 WHERE 子句指定 NODE_TYPE 的值應該為 8，以便只擷取規則。  
  
 如需詳細範例，請參閱 [關聯模型查詢範例](../../analysis-services/data-mining/association-model-query-examples.md)。  
  
###  <a name="bkmk_DecTree"></a> 範例 2:決策樹模型的內容查詢  
 決策樹模型可用於預測及分類。  此範例假設您正在使用模型預測結果，但是您也會想要查明哪些因素或規則可用來分類結果。  
  
 在決策樹模型中，節點是用來表示樹狀節點和分葉節點。 每一個節點的標題都會包含結果路徑的描述。 因此，若要追蹤任何特定結果的路徑，您需要識別包含該結果的節點，然後取得該節點的詳細資料。  
  
 在預測查詢中，您會加入預測函數 [PredictNodeId &#40;DMX&#41;](../../dmx/predictnodeid-dmx.md) 來取得相關節點的識別碼，如下列範例所示：  
  
```  
SELECT  Predict([Bike Buyer]), PredictNodeID([Bike Buyer])   
FROM [<decision tree model name>]  
PREDICTION JOIN   
<input rowset>   
```  
  
 您一旦取得包含結果之節點的識別碼之後，您可以擷取規則或路徑來說明預測，方法是建立包含 NODE_CAPTION 的內容查詢，如下所示：  
  
```  
SELECT NODE_CAPTION  
FROM [<decision tree model name>]   
WHERE NODE_UNIQUE_NAME= '<node id>'  
```  
  
 如需詳細範例，請參閱 [決策樹模型查詢範例](../../analysis-services/data-mining/decision-trees-model-query-examples.md)。  
  
##  <a name="bkmk_Results"></a> 使用查詢結果  
 如範例所示，內容查詢主要會傳回表格式資料列集，但也可能包含巢狀資料行中的資訊。 您可以扁平化傳回的資料列集，但是這麼做會讓結果使用起來更複雜。 特別是 NODE_DISTRIBUTION 節點的內容是以巢狀方式內嵌，但是包含了許多有關模型的有趣資訊。  
  
 如需有關如何使用階層式資料列集的詳細資訊，請參閱 MSDN 上的 OLEDB 規格。  
  
## <a name="see-also"></a>另請參閱  
 [了解 DMX Select 陳述式](../../dmx/understanding-the-dmx-select-statement.md)   
 [資料採礦查詢](../../analysis-services/data-mining/data-mining-queries.md)  
  
  
