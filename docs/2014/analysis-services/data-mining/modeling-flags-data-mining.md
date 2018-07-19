---
title: 模型旗標 （資料採礦） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- attributes [data mining]
- data types [data mining]
- REGRESSOR flag
- MODEL_EXISTENCE_ONLY flag
- REGRESSOR column
- columns [data mining], modeling flags
- NOT NULL modeling flag
- modeling flags [data mining]
- null values [Analysis Services]
- MODEL_EXISTENCE_ONLY column
- coding [Data Mining]
ms.assetid: 8826d5ce-9ba8-4490-981b-39690ace40a4
caps.latest.revision: 48
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 85abe1acb2fa12208ebf83541bd030646c67ddbc
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37155409"
---
# <a name="modeling-flags-data-mining"></a>模型旗標 (資料採礦)
  您可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中的模型旗標，為資料採礦演算法提供案例資料表中所定義資料的其他資訊。 演算法可以使用此一資訊建立更精確的資料採礦模型。  
  
 有些模型旗標會定義於採礦結構層級，有些則會定義於採礦模型資料行的層級。 比方說，`NOT NULL`模型旗標用於採礦結構資料行。 您可以根據您用來建立模型的演算法，在採礦模型資料行上定義其他模型旗標。  
  
> [!NOTE]  
>  除了 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]預先定義的模型旗標外，協力廠商外掛程式也可能擁有其他的模型旗標。  
  
## <a name="list-of-modeling-flags"></a>模型旗標的清單  
 下列清單描述 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中支援的模型旗標。 如需有關特定演算法所支援之模型旗標的詳細資訊，請參閱之前用來建立模型之演算法的技術參考主題。  
  
 `NOT NULL`  
 表示屬性資料行的值絕對不能包含 Null 值。 如果 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 在模型培訓處理過程中遇到這個屬性資料行的 Null 值，將會產生錯誤。  
  
 **MODEL_EXISTENCE_ONLY**  
 表示將資料行視為有兩個狀態：`Missing` 和 `Existing`。 如果值為`NULL`，它會被視為遺漏。 MODEL_EXISTENCE_ONLY 旗標會套用到可預測的屬性，而且受到大多數的演算法所支援。  
  
 作用中，將 MODEL_EXISTENCE_ONLY 旗標設定為`True`變更值的表示，因此有兩個狀態：`Missing`和`Existing`。 所有非遺漏狀態都會結合到單一`Existing`值。  
  
 此模型旗標的一般用法是 `NULL` 狀態具有隱含意義的屬性，而 `NOT NULL` 狀態的明確值則可能不如資料行擁有任何值來得重要。 例如，[DateContractSigned] 資料行可能`NULL`如果永遠不會簽署合約和`NOT NULL`如果已簽署的合約。 因此，如果模型的用途是預測是否會簽署合約，您可以使用 MODEL_EXISTENCE_ONLY 旗標來忽略中的精確日期值`NOT NULL`情況下，並僅區分合約所在的情況下`Missing`或`Existing`.  
  
> [!NOTE]  
>  「遺漏」是演算法所使用的特殊狀態，與資料行中的文字值「遺漏」不同。 如需詳細資訊，請參閱[遺漏值 &#40;Analysis Services - 資料採礦&#41;](missing-values-analysis-services-data-mining.md)。  
  
 `REGRESSOR`  
 指出資料行是處理期間做為迴歸輸入變數使用的候選選項。 這個旗標是在採礦模型資料行上定義，並且只能套用至採用連續數值資料類型的資料行。 如需有關使用這個旗標的詳細資訊，請參閱本主題的 [使用 REGRESSOR 模型旗標](#bkmk_UseRegressors)一節。  
  
## <a name="viewing-and-changing-modeling-flags"></a>檢視和變更模型旗標  
 在資料採礦設計師中，您可以藉由檢視結構或模型的屬性來檢視與採礦結構資料行或模型資料行相關聯的模型旗標。  
  
 若要判斷哪些模型旗標已經套用至目前的採礦結構，您可以使用類似以下的查詢，針對傳回結構資料行之模型旗標的資料採礦結構描述資料列集來建立查詢：  
  
```  
SELECT COLUMN_NAME, MODELING_FLAG  
FROM $system.DMSCHEMA_MINING_STRUCTURE_COLUMNS  
WHERE STRUCTURE_NAME = '<structure name>'  
```  
  
 您可以加入或變更模型中所使用的模型旗標，方法是使用資料採礦設計師及編輯關聯資料行的屬性。 這類變更需要重新處理結構或模型。  
  
 您可以使用 DMX 或是 AMO 或 XMLA 指令碼，在新的採礦結構或採礦模型中指定模型旗標。 但是，您不能使用 DMX 變更在現有採礦模型和結構中使用的模型旗標。 您必須使用 `ALTER MINING STRUCTURE….ADD MINING MODEL`語法建立新的採礦模型。  
  
##  <a name="bkmk_UseRegressors"></a> 使用 REGRESSOR 模型旗標  
 在資料行上設定 REGRESSOR 模型旗標亦即向演算法表示，該資料行包含潛在的迴歸輸入變數。 模型中使用的實際迴歸輸入變數是依照演算法而定。 如果潛在的迴歸輸入變數無法將可預測屬性模型化，則可能會遭到捨棄。  
  
 使用資料採礦精靈建立模型時，所有連續的輸入資料行都會標記為可能的迴歸輸入變數。 因此，即使未在資料行上明確地設定 REGRESSOR 旗標，也可能會在模型中將該資料行當做迴歸輸入變數使用。  
  
 您可以針對採礦模型的結構描述資料列集執行查詢來判斷實際用於已處理模型的迴歸輸入變數，如下列範例所示：  
  
```  
SELECT COLUMN_NAME, MODELING_FLAG  
FROM $system.DMSCHEMA_MINING_COLUMNS  
WHERE MODEL_NAME = '<model name>'  
```  
  
 **注意** ：如果您修改採礦模型並將資料行的內容類型從連續變更為離散，則必須手動變更採礦資料行上的旗標，然後重新處理模型。  
  
### <a name="regressors-in-linear-regression-models"></a>線性迴歸模型中的迴歸輸入變數  
 線性迴歸模型是以 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 決策樹演算法為基礎。 即使您不使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 線性迴歸演算法，任何決策樹模型仍可能包含代表連續屬性迴歸的樹狀結構或節點。  
  
 因此您在這些模型中，不需要指定代表迴歸輸入變數的連續資料行。 即使未在資料行上設定 REGRESSOR 旗標， [!INCLUDE[msCoName](../../includes/msconame-md.md)] 決策樹演算法也會將資料集分割成具備有意義之模式的區域。 其差異是當您設定模型旗標時，演算法會嘗試尋找以下形式的迴歸方程式，在樹狀結構的節點中比對模式。  
  
 a*C1 + b\*C2 + ...  
  
 然後會計算剩餘數的總和，如果差異過大，就會在樹狀結構中強制進行分割。  
  
 例如，如果您使用 **Income** 做為屬性來預測客戶購買行為，且在資料行上設定 REGRESSOR 模型旗標，則演算法首先會使用標準迴歸公式來比對 **Income** 值。 如果差異過大，就會放棄迴歸公式，且根據其他的屬性分割樹狀結構。 在分割之後，決策樹演算法就會接著嘗試在每個分支中比對迴歸輸入變數與收入。  
  
 您可以使用 FORCE_REGRESSOR 參數來確保演算法會使用特定的迴歸輸入變數。 這個參數可用於決策樹演算法及線性迴歸演算法。  
  
## <a name="related-tasks"></a>相關工作  
 使用下列連結，深入了解如何使用模型旗標。  
  
|工作|主題|  
|----------|-----------|  
|使用資料採礦設計師來編輯模型旗標|[檢視或變更模型旗標&#40;資料採礦&#41;](modeling-flags-data-mining.md)|  
|為演算法指定提示，以建議可能的迴歸輸入變數|[在模型中指定當做迴歸輸入變數使用的資料行](specify-a-column-to-use-as-regressor-in-a-model.md)|  
|請參閱特定演算法所支援的模型旗標 (在每一個演算法參考主題的＜模型旗標＞一節內)。|[資料採礦演算法&#40;Analysis Services-資料採礦&#41;](data-mining-algorithms-analysis-services-data-mining.md)|  
|深入了解採礦結構資料行以及您可以在資料行上設定的屬性|[採礦結構資料行](mining-structure-columns.md)|  
|深入了解採礦模型資料行以及可以在模型層級套用的模型旗標|[採礦模型資料行](mining-model-columns.md)|  
|請參閱在 DMX 陳述式中搭配模型旗標使用的語法|[模型旗標&#40;DMX&#41;](/sql/dmx/modeling-flags-dmx)|  
|了解遺漏的值以及如何處理這些值|[遺漏值&#40;Analysis Services-資料採礦&#41;](missing-values-analysis-services-data-mining.md)|  
|了解如何管理模型和結構以及設定使用屬性|[移動資料採礦物件](moving-data-mining-objects.md)|  
  
  
