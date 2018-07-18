---
title: IsTrainingCase (DMX) |Microsoft 文件
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 00344eeb38f3aae5cae7ac25c1b65b403cc85cb9
ms.sourcegitcommit: 8f0faa342df0476884c3238e36ae3d9634151f87
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2018
ms.locfileid: "34842341"
---
# <a name="istrainingcase-dmx"></a>IsTrainingCase (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  指示案例是否會當做定型案例用於指定的資料採礦模型或採礦結構。  
  
## <a name="syntax"></a>語法  
  
```  
  
IsTrainingCase()  
```  
  
## <a name="result-type"></a>結果類型  
 傳回**true**如果案例是訓練資料集的一部分; 否則**false**。  
  
## <a name="remarks"></a>備註  
 如果您使用資料採礦精靈建立採礦結構和相關的採礦模型，則預設會將百分之 30 的案例擱置一旁，當做測試資料集使用。 您指定之資料來源中的其餘案例會用來定型此模型。 但是，如果您使用資料採礦延伸模組 (DMX) 建立採礦模型，則預設會使用所有資料來定型此模型，而且不會建立測試集。 若要啟用測試資料集的建立，您必須設定 WITH HOLDOUT 子句的參數。  
  
 您可以藉由檢視 <xref:Microsoft.AnalysisServices.MiningStructure.HoldoutMaxCases%2A> 和 <xref:Microsoft.AnalysisServices.MiningStructure.HoldoutMaxPercent%2A> 屬性的值，判斷特定資料採礦結構中的資料是否已分割成測試集和定型集。  
  
> [!NOTE]  
>  如果您想要使用 IsTrainingCase 或 IsTestCase 函數來傳回模型中案例的相關詳細資料，必須在模型上啟用鑽研。 如需詳細資訊，請參閱 [針對採礦模型啟用鑽研](../analysis-services/data-mining/enable-drillthrough-for-a-mining-model.md)。  
  
 若要傳回屬於測試資料集的情況下，使用函數[IsTestCase &#40;DMX&#41;](../dmx/istestcase-dmx.md)。  
  
## <a name="examples"></a>範例  
 下列範例會使用群集的資料採礦模型，從 目標郵寄案例中[基本資料採礦教學課程](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c)。 此查詢只會傳回用於定型採礦模型的案例。 此外，定型案例限制為 40 歲以下的客戶。  
  
```  
SELECT *  
FROM [TM Clustering].CASES  
WHERE IsTrainingCase()  
AND [Age] <40  
```  
  
 如需如何查詢資料採礦中使用的情況下的其他範例，請參閱[SELECT FROM&#60;模型&#62;。案例&#40;DMX&#41; ](../dmx/select-from-model-cases-dmx.md)和[SELECT FROM&#60;結構&#62;。案例](../dmx/select-from-structure-cases.md)。  
  
## <a name="see-also"></a>另請參閱  
 [定型和測試資料集](../analysis-services/data-mining/training-and-testing-data-sets.md)   
 [函式&#40;DMX&#41;](../dmx/functions-dmx.md)   
 [資料採礦查詢](../analysis-services/data-mining/data-mining-queries.md)  
  
  
