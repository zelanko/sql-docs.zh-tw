---
title: 選取 [ &lt;從&gt;模型]。SAMPLE_CASES （DMX） |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: e0838c688b0518bf1fc7ed6c5d65c3ef03d0a7aa
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67928315"
---
# <a name="select-from-ltmodelgtsample_cases-dmx"></a>選取 [ &lt;從&gt;模型]。SAMPLE_CASES （DMX）
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  傳回代表用於培訓資料採礦模型之案例的範例案例。  
  
 若要使用這個陳述式，您必須在建立採礦模型時啟用鑽研。 如需有關啟用「鑽取」的詳細資訊，請參閱[&#40;dmx&#41;建立採礦模型](../dmx/create-mining-model-dmx.md)、[選取 &#40;dmx&#41;](../dmx/select-into-dmx.md)，以及[改變 &#40;dmx&#41;的採礦結構](../dmx/alter-mining-structure-dmx.md)。  
  
## <a name="syntax"></a>語法  
  
```  
  
SELECT [FLATTENED] [TOP <n>] <expression list> FROM <model>.SAMPLE_CASES  
[WHERE <condition list>] ORDER BY <expression> [DESC|ASC]]  
```  
  
## <a name="arguments"></a>引數  
 *n*  
 選擇性。 指定要傳回多少資料列的整數。  
  
 *運算式清單*  
 相關資料行識別碼的逗號分隔清單。  
  
 *模型*  
 模型識別碼。  
  
 *條件清單*  
 選擇性。 限制從資料行清單傳回之值的條件。  
  
 *expression*  
 選擇性。 傳回純量值的運算式。  
  
## <a name="remarks"></a>備註  
 可能會產生範例案例，而且可能未實際存在於培訓資料中。 傳回的案例是指定之內容節點的代表。  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)]雖然時序群集演算法是唯一[!INCLUDE[msCoName](../includes/msconame-md.md)]支援使用 SELECT FROM \<model> 的演算法。SAMPLE_CASES，協力廠商演算法也可能支援它。  
  
## <a name="examples"></a>範例  
 下列範例會傳回用於培訓 Target Mail 採礦模型的範例案例。 在**WHERE**子句中使用[IsInNode &#40;DMX&#41;](../dmx/isinnode-dmx.md)函數，只會傳回與 ' 000000003 ' 節點相關聯的案例。 節點字串可以在結構描述資料列集的 NODE_UNIQUE_NAME 資料行中找到。  
  
```  
Select * from [Sequence Clustering].SAMPLE_Cases  
WHERE IsInNode('000000003')  
```  
  
## <a name="see-also"></a>另請參閱  
 [選取 &#40;DMX&#41;](../dmx/select-dmx.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 資料定義語句](../dmx/dmx-statements-data-definition.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 資料動作陳述式](../dmx/dmx-statements-data-manipulation.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 陳述式參考](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
