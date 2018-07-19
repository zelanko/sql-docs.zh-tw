---
title: RowNumber 函式 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 9d718ba8-d323-49fb-aac8-e7013a117b75
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: bb6025b8cf196d45fe0a6c9ac5cf0c19aa54013e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37276274"
---
# <a name="rownumber-function-report-builder-and-ssrs"></a>RowNumber 函數 (報表產生器及 SSRS)
  傳回指定範圍中資料列數的執行計數。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>語法  
  
```  
  
RowNumber(scope)  
```  
  
#### <a name="parameters"></a>參數  
 *範圍 (scope)*  
 (`String`) 的資料集、 資料區域或群組或 null 名稱 (`Nothing`在[!INCLUDE[vbprvb](../../includes/vbprvb-md.md)])，指定要在其中評估資料列數目的內容。 `Nothing` 指定最外層的內容，通常為報表資料集。  
  
## <a name="remarks"></a>備註  
 `RowNumber` 傳回指定的範圍內的資料列的計數執行值，就如同[RunningValue](report-builder-functions-runningvalue-function.md)傳回彙總函式的執行中的值。 當您指定範圍時，可以指定何時要將資料列計數重設為 1。  
  
 *scope* 不可為運算式。 *scope* 必須是包含範圍。 就一般範圍而言，從最外層到最內層的內含項目依序為報表資料集、資料區域、資料列群組或資料行群組。  
  
 若要在全部資料行中累加值，請將範圍指定為資料行群組的名稱。 若要在資料列中向下累加數目，請將範圍指定為資料列群組的名稱。  
  
> [!NOTE]  
>  不支援在單一運算式中包含同時指定資料列群組和資料行群組的彙總。  
  
 如需詳細資訊，請參閱[彙總函式參考 &#40;報表產生器及 SSRS&#41;](report-builder-functions-aggregate-functions-reference.md) 和[總計、彙總與內建集合的運算式範圍 &#40;報表產生器及 SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)。  
  
## <a name="code-example"></a>程式碼範例  
 以下是您可以使用運算式`BackgroundColor`Tablix 資料區域詳細資料列以改變每個群組，永遠從白色開始的詳細資料列的色彩屬性。  
  
```  
=IIF(RowNumber("GroupbyCategory") Mod 2, "White", "PaleGreen")  
```  
  
## <a name="see-also"></a>另請參閱  
 [在報表中的運算式會使用&#40;報表產生器及 SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [運算式範例 &#40;報表產生器及 SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [運算式中的資料類型 &#40;報表產生器及 SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [Expression Scope for Totals，Aggregates，and Built-in Collections&#40;報表產生器及 SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
