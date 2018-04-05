---
title: 存在 (DMX) |Microsoft 文件
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- Exists
dev_langs:
- DMX
helpviewer_keywords:
- Exists function
ms.assetid: 3b54dd93-f0a8-4f9a-96ae-a38bf977dda1
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 6f5fb5dccb91af6409c0ed91796ba5119475ccaf
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="exists-dmx"></a>Exists (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  傳回**true**如果指定的子查詢會傳回至少一個資料列。  
  
## <a name="syntax"></a>語法  
  
```  
  
EXISTS(<subquery>)  
```  
  
## <a name="arguments"></a>引數  
 *子查詢*  
 選取表單的 SELECT 陳述式 * FROM\<資料行名稱 > [其中\<述詞清單 >]。  
  
## <a name="result-type"></a>結果類型  
 傳回**true**如果子查詢所傳回的結果集包含至少一個資料列; 否則傳回**false**。  
  
## <a name="remarks"></a>備註  
 您可以在 EXISTS 之前使用 NOT 關鍵字，例如 `WHERE NOT EXISTS (<subquery>)`。  
  
 您加入 EXISTS 之子查詢引數的資料行清單是不相關的；此函數只會檢查是否有符合條件的資料列存在。  
  
## <a name="examples"></a>範例  
 您可以使用 EXISTS 和 NOT EXISTS 來檢查巢狀資料表中的條件。 當您建立的篩選可控制用來定型或測試資料採礦模型的資料時，這樣的處理方式會很有用。 如需詳細資訊，請參閱[採礦模型的篩選 &#40;Analysis Services - 資料採礦&#41;](../analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md)。  
  
 下列範例根據`[Association]`採礦結構和採礦模型中建立[基本資料採礦教學課程](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c)。 此查詢只會傳回客戶至少購買一個修補套件的案例。  
  
```  
SELECT * FROM [Association].CASES  
WHERE EXISTS  
(  
SELECT * FROM [v Assoc Seq Line Numbers]  
WHERE [[Model] = 'Patch kit'  
)  
```  
  
 若要檢視此查詢所傳回的相同資料的另一個方法是在關聯檢視器中開啟模型，以滑鼠右鍵按一下項目集**Patch kit = Existing**，選取**鑽研**選項，然後再選取**僅限模型案例**。  
  
## <a name="see-also"></a>請參閱  
 [函式 &#40; DMX &#41;](../dmx/functions-dmx.md)   
 [模型篩選語法和範例 &#40;Analysis Services-資料採礦 &#41;](../analysis-services/data-mining/model-filter-syntax-and-examples-analysis-services-data-mining.md)  
  
  
