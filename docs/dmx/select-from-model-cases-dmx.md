---
title: "SELECT FROM&lt;模型&gt;。案例 (DMX) |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SELECT
- CASES
- FROM
dev_langs: DMX
helpviewer_keywords:
- SELECT FROM <model>.CASES statement
- drillthrough [DMX]
ms.assetid: d58acb47-aaa6-40b7-b8c4-6a6700fbc1dd
caps.latest.revision: "55"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 1a02b3f56bd56fd7b86bbf3a998b7fdfd7316e9d
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="select-from-ltmodelgtcases-dmx"></a>SELECT FROM&lt;模型&gt;。案例 (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  支援鑽研，並傳回用於培訓模型的案例。 如果已經在採礦結構和採礦模型上啟用鑽研，而且有適當的權限，您也可以傳回不包含在模型中的結構資料行。  
  
 如果採礦模型上未啟用鑽研，此陳述式將會失敗。  
  
> [!NOTE]  
>  在資料採礦延伸模組 (DMX) 中，唯有建立模型時才能啟用鑽研。 您可以使用 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]，將鑽研加入到現有的模型，但是在檢視或查詢案例之前，必須先重新處理模型。  
  
 如需如何啟用鑽研的詳細資訊，請參閱[CREATE MINING MODEL &#40; DMX &#41;](../dmx/create-mining-model-dmx.md)， [SELECT INTO &#40; DMX &#41;](../dmx/select-into-dmx.md)，和[ALTER MINING STRUCTURE &#40; DMX &#41;](../dmx/alter-mining-structure-dmx.md)。  
  
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
 如果有同時在採礦模型和採礦結構上啟用鑽研，對於模型和結構具有鑽研權限之角色成員的使用者可以存取不包含在採礦模型中的採礦結構資料行。 因此，若要保護敏感性資料或個人資訊，您應該建構您的資料來源檢視來遮罩個人資訊，並授與**AllowDrillthrough**只在必要時在採礦結構上的權限。  
  
 [延隔時間 &#40; DMX &#41;](../dmx/lag-dmx.md)函式可以搭配時間序列模型用來傳回或篩選每個案例與初始時間之間的延遲時間。  
  
 使用[IsInNode &#40; DMX &#41;](../dmx/isinnode-dmx.md)函式在**其中**子句會傳回與結構描述資料列集之 NODE_UNIQUE_NAME 資料行所指定的節點相關聯的案例。  
  
## <a name="examples"></a>範例  
 下列範例以採礦結構目標郵寄 」 為基礎[!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]資料庫和其相關聯的採礦模型。 如需詳細資訊，請參閱[基本資料採礦教學課程](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c)。  
  
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
>  並非所有的採擷模型類型都支援鑽研。 如需支援鑽研之模型的資訊，請參閱[鑽研查詢 &#40; 資料採礦 &#41;](../analysis-services/data-mining/drillthrough-queries-data-mining.md)。  
  
## <a name="see-also"></a>請參閱＜  
 [SELECT &#40; DMX &#41;](../dmx/select-dmx.md)   
 [資料採礦延伸模組 &#40; DMX &#41;資料定義陳述式](../dmx/dmx-statements-data-definition.md)   
 [資料採礦延伸模組 &#40; DMX &#41;資料操作陳述式](../dmx/dmx-statements-data-manipulation.md)   
 [資料採礦延伸模組 &#40; DMX &#41;陳述式參考](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
