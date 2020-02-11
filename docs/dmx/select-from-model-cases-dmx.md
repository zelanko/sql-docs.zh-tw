---
title: 選取 [ &lt;從&gt;模型]。案例（DMX） |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 5f0334c37eeedafee7066f01d61745fcb82d1629
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68892838"
---
# <a name="select-from-ltmodelgtcases-dmx"></a>選取 [ &lt;從&gt;模型]。案例（DMX）
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  支援鑽研，並傳回用於培訓模型的案例。 如果已經在採礦結構和採礦模型上啟用鑽研，而且有適當的權限，您也可以傳回不包含在模型中的結構資料行。  
  
 如果採礦模型上未啟用鑽研，此陳述式將會失敗。  
  
> [!NOTE]  
>  在資料採礦延伸模組 (DMX) 中，唯有建立模型時才能啟用鑽研。 您可以使用 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]，將鑽研加入到現有的模型，但是在檢視或查詢案例之前，必須先重新處理模型。  
  
 如需如何啟用「鑽取」的詳細資訊，請參閱[&#40;dmx&#41;建立採礦模型](../dmx/create-mining-model-dmx.md)、[選取 &#40;dmx&#41;](../dmx/select-into-dmx.md)，以及[改變 &#40;dmx&#41;的採礦結構](../dmx/alter-mining-structure-dmx.md)。  
  
## <a name="syntax"></a>語法  
  
```  
  
SELECT [FLATTENED] [TOP <n>] <expression list> FROM <model>.CASES  
[WHERE <condition expression>][ORDER BY <expression> [DESC|ASC]]  
```  
  
## <a name="arguments"></a>引數  
 *n*  
 選擇性。 指定要傳回多少資料列的整數。  
  
 *運算式清單*  
 逗號分隔的運算式清單。 運算式可以包含資料行識別碼、使用者定義函數、UDF 以及 VBA 函數等等。  
  
 若要包含不包含在採礦模型中的結構資料行，請使用函數 `StructureColumn('<structure column name>')`。  
  
 *model*  
 模型識別碼。  
  
 *條件運算式*  
 限制從資料行清單傳回之值的條件。  
  
 *expression*  
 選擇性。 傳回純量值的運算式。  
  
## <a name="remarks"></a>備註  
 如果有同時在採礦模型和採礦結構上啟用鑽研，對於模型和結構具有鑽研權限之角色成員的使用者可以存取不包含在採礦模型中的採礦結構資料行。 因此，若要保護敏感性資料或個人資訊，您應該先建立您的資料來源 view 來遮罩個人資訊，並只在必要時，授與**AllowDrillthrough**許可權給某個採礦結構。  
  
 [&#40;DMX&#41;](../dmx/lag-dmx.md)函數的 Lag 可以與時間序列模型搭配使用，以傳回或篩選每個案例和初始時間之間的時間延遲。  
  
 在**WHERE**子句中使用[IsInNode &#40;DMX&#41;](../dmx/isinnode-dmx.md)函數，只會傳回與架構資料列集的 NODE_UNIQUE_NAME 資料行所指定的節點相關聯的案例。  
  
## <a name="examples"></a>範例  
 下列範例是根據以[!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]資料庫和其相關聯的採礦模型為依據的目標郵寄結構。 如需詳細資訊，請參閱[基本資料採礦教學](https://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c)課程。  
  
### <a name="example-1-drillthrough-to-model-cases-and-structure-columns"></a>範例 1：鑽研模型案例和結構資料行  
 下列範例會傳回用於測試「目標郵寄」模型之所有案例的資料行。 如果有建置模型的採礦結構不包含鑑效組測試資料集，此查詢會傳回 0 個案例。 您可以使用運算式清單，僅傳回您需要的資料行。  
  
```  
SELECT * FROM [TM Decision Tree].Cases  
WHERE IsTestCase();  
```  
  
### <a name="example-2-drillthrough-to-training-cases-in-a-specific-node"></a>範例 2：鑽研特定節點中的培訓案例  
 下列範例只會傳回用於培訓 Cluster 2 的案例。 Cluster 2 的節點之 NODE_UNIQUE_NAME 資料行的值為 '002'。 此範例也會傳回一個不屬於採礦模型一部分的結構資料行 [客戶索引鍵]，並提供該資料行的別名 `CustomerID`。 請注意，系統會將結構資料行的名稱傳遞為字串值，因此必須加上引號，而非方括號。  
  
```  
SELECT StructureColumn('Customer Key') AS CustomerID, *   
FROM [TM_Clustering].Cases  
WHERE IsTrainingCase()  
AND IsInNode('002')  
```  
  
 若要傳回結構資料行，必須同時在採礦模型和採礦結構上啟用鑽研權限。  
  
> [!NOTE]  
>  並非所有的採擷模型類型都支援鑽研。 如需有關支援「鑽取」之模型的詳細資訊，請參閱[&#40;資料採礦&#41;](https://docs.microsoft.com/analysis-services/data-mining/drillthrough-queries-data-mining)的「查詢」查詢。  
  
## <a name="see-also"></a>另請參閱  
 [選取 &#40;DMX&#41;](../dmx/select-dmx.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 資料定義語句](../dmx/dmx-statements-data-definition.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 資料動作陳述式](../dmx/dmx-statements-data-manipulation.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 語句參考](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
