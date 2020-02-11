---
title: IsTestCase （DMX） |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 050ceeaa8eb5700f108b7135616817e09c0031cb
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68889032"
---
# <a name="istestcase-dmx"></a>IsTestCase (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  指示案例是否會當做測試案例用於指定的資料採礦模型或採礦結構。  
  
## <a name="syntax"></a>語法  
  
```  
  
IsTestCase()  
```  
  
## <a name="result-type"></a>結果類型  
 如果案例是測試資料集的一部分，則傳回**true** ;否則**為 false**。  
  
## <a name="remarks"></a>備註  
 如果您使用資料採礦精靈建立採礦結構和相關的採礦模型，則預設會將百分之 30 的案例擱置一旁，當做測試資料集使用。 其餘案例會用於定型資料採礦模型。 可以搭配以該結構為基礎的所有模型來使用相同的資料集。 但是，如果您使用 DMX 建立採礦模型，則預設會使用所有資料來定型此模型，而且不會建立測試集。 若要啟用測試資料集的建立，您必須設定 WITH HOLDOUT 子句的參數。  
  
 您可以藉由檢視 <xref:Microsoft.AnalysisServices.MiningStructure.HoldoutMaxCases%2A> 和 <xref:Microsoft.AnalysisServices.MiningStructure.HoldoutMaxPercent%2A> 屬性的值，判斷是否已經在特定的採礦結構上建立測試集。  
  
> [!NOTE]  
>  如果您想要使用 IsTrainingCase 或 IsTestCase 函數傳回特定模型中案例的詳細資料，則必須在模型上啟用鑽取。 如需詳細資訊，請參閱 [針對採礦模型啟用鑽研](https://docs.microsoft.com/analysis-services/data-mining/enable-drillthrough-for-a-mining-model)。  
  
 若要傳回屬於訓練資料集一部分的案例，請使用[IsTrainingCase &#40;DMX&#41;](../dmx/istrainingcase-dmx.md)函數。  
  
## <a name="examples"></a>範例  
 下列範例會使用在`Targeted Mailing` 「[基本資料採礦」教學](https://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c)課程中建立的「採礦結構」。 此查詢會傳回此結構中用於測試的所有案例。  
  
```  
SELECT *  
FROM [Targeted Mailing].CASES  
WHERE IsTestCase()  
```  
  
 如需如何查詢資料採礦中使用之案例的詳細資訊，請參閱[SELECT FROM &#60;model&#62;。&#40;DMX&#41;的案例](../dmx/select-from-model-cases-dmx.md)，並[從 &#60;結構&#62; 中選取。案例](../dmx/select-from-structure-cases.md)。  
  
## <a name="see-also"></a>另請參閱  
 [DMX&#41;的函數 &#40;](../dmx/functions-dmx.md)   
 [資料採礦查詢](https://docs.microsoft.com/analysis-services/data-mining/data-mining-queries)   
 [定型和測試資料集](https://docs.microsoft.com/analysis-services/data-mining/training-and-testing-data-sets)  
  
  
