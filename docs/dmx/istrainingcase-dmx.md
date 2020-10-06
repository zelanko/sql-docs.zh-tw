---
description: IsTrainingCase (DMX)
title: IsTrainingCase (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 5eb68d0aaa0d19fb903154b8d5c4d4135b57883e
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/05/2020
ms.locfileid: "91726142"
---
# <a name="istrainingcase-dmx"></a>IsTrainingCase (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  指示案例是否會當做定型案例用於指定的資料採礦模型或採礦結構。  
  
## <a name="syntax"></a>Syntax  
  
```  
  
IsTrainingCase()  
```  
  
## <a name="result-type"></a>結果類型  
 如果案例是訓練資料集的一部分，則傳回 **true** ;否則 **為 false**。  
  
## <a name="remarks"></a>備註  
 如果您使用資料採礦精靈建立採礦結構和相關的採礦模型，則預設會將百分之 30 的案例擱置一旁，當做測試資料集使用。 您指定之資料來源中的其餘案例會用來定型此模型。 但是，如果您使用資料採礦延伸模組 (DMX) 建立採礦模型，則預設會使用所有資料來定型此模型，而且不會建立測試集。 若要啟用測試資料集的建立，您必須設定 WITH HOLDOUT 子句的參數。  
  
 您可以藉由檢視 <xref:Microsoft.AnalysisServices.MiningStructure.HoldoutMaxCases%2A> 和 <xref:Microsoft.AnalysisServices.MiningStructure.HoldoutMaxPercent%2A> 屬性的值，判斷特定資料採礦結構中的資料是否已分割成測試集和定型集。  
  
> [!NOTE]  
>  如果您想要使用 IsTrainingCase 或 IsTestCase 函數來傳回有關模型中案例的詳細資料，則必須在模型上啟用「鑽取」。 如需詳細資訊，請參閱 [針對採礦模型啟用鑽研](/analysis-services/data-mining/enable-drillthrough-for-a-mining-model)。  
  
 若要傳回屬於測試資料集一部分的案例，請使用 [IsTestCase &#40;DMX&#41;](../dmx/istestcase-dmx.md)的函數。  
  
## <a name="examples"></a>範例  
 下列範例會在 [基本資料採礦教學](/previous-versions/sql/sql-server-2016/ms167167(v=sql.130))課程中，使用來自目標郵寄案例的群集資料採礦模型。 此查詢只會傳回用於定型採礦模型的案例。 此外，定型案例限制為 40 歲以下的客戶。  
  
```  
SELECT *  
FROM [TM Clustering].CASES  
WHERE IsTrainingCase()  
AND [Age] <40  
```  
  
 如需如何查詢資料採礦中使用之案例的其他範例，請參閱 [從 &#60;模型&#62; 選取。&#40;DMX&#41;的案例 ](../dmx/select-from-model-cases-dmx.md) ，並 [從 &#60;結構&#62; 進行選取。案例](../dmx/select-from-structure-cases.md)。  
  
## <a name="see-also"></a>另請參閱  
 [定型和測試資料集](/analysis-services/data-mining/training-and-testing-data-sets)   
 [DMX&#41;函數 &#40;](../dmx/functions-dmx.md)   
 [資料採礦查詢](/analysis-services/data-mining/data-mining-queries)  
  
