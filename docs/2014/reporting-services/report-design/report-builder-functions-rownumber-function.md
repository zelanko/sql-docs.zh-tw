---
title: RowNumber 函式 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 9d718ba8-d323-49fb-aac8-e7013a117b75
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 181670ab62d31fbb7b6815518129dd5b4e8a1b1d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63216197"
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
 (`String`) 資料集、資料區域或群組的名稱，或為 Null (在 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 中為 `Nothing`)，指定要在其中評估資料列數的內容。 `Nothing` 指定最外層的內容，這通常為報表資料集。  
  
## <a name="remarks"></a>備註  
 `RowNumber` 傳回指定的範圍內的資料列的計數執行值，就如同[RunningValue](report-builder-functions-runningvalue-function.md)傳回彙總函式的執行中的值。 當您指定範圍時，可以指定何時要將資料列計數重設為 1。  
  
 *scope* 不可為運算式。 *scope* 必須是包含範圍。 就一般範圍而言，從最外層到最內層的內含項目依序為報表資料集、資料區域、資料列群組或資料行群組。  
  
 若要在全部資料行中累加值，請將範圍指定為資料行群組的名稱。 若要在資料列中向下累加數目，請將範圍指定為資料列群組的名稱。  
  
> [!NOTE]  
>  不支援在單一運算式中包含同時指定資料列群組和資料行群組的彙總。  
  
 如需詳細資訊，請參閱[彙總函式參考 &#40;報表產生器及 SSRS&#41;](report-builder-functions-aggregate-functions-reference.md) 和[總計、彙總與內建集合的運算式範圍 &#40;報表產生器及 SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)。  
  
## <a name="code-example"></a>程式碼範例  
 下列的運算式可用於 Tablix 資料區域詳細資料列的 `BackgroundColor` 屬性，以改變每個群組的詳細資料列色彩 (永遠從白色開始)。  
  
```  
=IIF(RowNumber("GroupbyCategory") Mod 2, "White", "PaleGreen")  
```  
  
## <a name="see-also"></a>另請參閱  
 [報表中的運算式用法 &#40;報表產生器及 SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [運算式範例 &#40;報表產生器及 SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [運算式中的資料類型 &#40;報表產生器及 SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [總計、彙總與內建集合的運算式範圍 &#40;報表產生器及 SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
