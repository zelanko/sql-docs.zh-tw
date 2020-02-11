---
title: Exists （DMX） |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 0197417dfef604f3cb90b5fa032dae892de272c7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68889043"
---
# <a name="exists-dmx"></a>Exists (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  如果指定的子查詢至少傳回一個資料列，則傳回**true** 。  
  
## <a name="syntax"></a>語法  
  
```  
  
EXISTS(<subquery>)  
```  
  
## <a name="arguments"></a>引數  
 *subquery*  
 [從\<資料行名稱] 表單 select * 的 select 語句> \<[WHERE 述詞清單>]。  
  
## <a name="result-type"></a>結果類型  
 如果子查詢所傳回的結果集至少包含一個資料列，則會傳回**true** ;否則，會傳回**false**。  
  
## <a name="remarks"></a>備註  
 您可以在 EXISTS 之前使用 NOT 關鍵字，例如 `WHERE NOT EXISTS (<subquery>)`。  
  
 您加入 EXISTS 之子查詢引數的資料行清單是不相關的；此函數只會檢查是否有符合條件的資料列存在。  
  
## <a name="examples"></a>範例  
 您可以使用 EXISTS 和 NOT EXISTS 來檢查巢狀資料表中的條件。 當您建立的篩選可控制用來定型或測試資料採礦模型的資料時，這樣的處理方式會很有用。 如需詳細資訊，請參閱[採礦模型的篩選 &#40;Analysis Services - 資料採礦&#41;](https://docs.microsoft.com/analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining)。  
  
 下列範例是以您在`[Association]` [基本資料採礦教學](https://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c)課程中建立的「採礦結構」和「採礦模型」為基礎。 此查詢只會傳回客戶至少購買一個修補套件的案例。  
  
```  
SELECT * FROM [Association].CASES  
WHERE EXISTS  
(  
SELECT * FROM [v Assoc Seq Line Numbers]  
WHERE [[Model] = 'Patch kit'  
)  
```  
  
 另一個查看此查詢所傳回之資料的方式，就是在關聯檢視器中開啟模型，以滑鼠右鍵按一下 [專案集**修補套件 = 現有**]，**選取 [向**下切入] 選項，然後選取 [**僅限模型案例**]。  
  
## <a name="see-also"></a>另請參閱  
 [DMX&#41;的函數 &#40;](../dmx/functions-dmx.md)   
 [模型篩選語法和範例 &#40;Analysis Services-資料採礦&#41;](https://docs.microsoft.com/analysis-services/data-mining/model-filter-syntax-and-examples-analysis-services-data-mining)  
  
  
