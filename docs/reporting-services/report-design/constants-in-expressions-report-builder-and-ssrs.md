---
title: 運算式中的常數 (報表產生器) | Microsoft Docs
description: 了解報表產生器內報表運算式中常值文字或常數的預先定義文字。
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: b8ae650b-0f46-4848-b62b-15f8a40751b8
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 8737057e0e4b291abf6530f5f6f74ce145dc84d7
ms.sourcegitcommit: e572f1642f588b8c4c75bc9ea6adf4ccd48a353b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2020
ms.locfileid: "84779106"
---
# <a name="constants-in-expressions-report-builder-and-ssrs"></a>運算式中的常數 (報表產生器及 SSRS)
  常數是由常值文字或預先定義的文字所組成。 報表處理器可以存取預先定義的常數，讓您在運算式中納入這些常數時，在系統評估運算式之前，就會將常數以其代表的值來取代。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="literal-text"></a>常值文字  
 在運算式中，常值文字是置於雙引號之間的文字。 如果文字是運算式的一部分，則您也可以直接在文字方塊中輸入文字，而不加上雙引號。 如果文字方塊的值不是以等號 (=) 開頭，就會將該文字當做常值文字。 下表顯示若干運算式中的常值文字範例。  
  
|持續性|顯示文字|運算式文字|  
|--------------|------------------|---------------------|  
|報表執行於：|<\<Expr>>|`="Report run at: " & Globals!ExecutionTime`|  
|Adventure Works Cycles|Adventure Works Cycles|Adventure Works Cycles|  
|[加上括號的顯示文字]|\\[加上括號的顯示文字\\]|[加上括號的顯示文字]|  
  
## <a name="rdl-constants"></a>RDL 常數  
 您可以在運算式中使用以報表定義語言 (RDL) 所定義的常數。 當您為報表屬性建立只接受特定有效的運算式時，常數就會顯示在 **[運算式]** 對話方塊中 (也稱為列舉型別)。 下表顯示兩個範例。  
  
|屬性|描述|值|  
|--------------|-----------------|------------|  
|TextAlign|用來對齊文字方塊中文字的有效。|一般、靠左、置中、靠右|  
|BorderStyle|加入至報表的線條有效。|預設值、無、點線、虛線、實線、雙線、虛線點、虛線點點|  
  
## <a name="visual-basic-constants"></a>Visual Basic 常數  
 您可以在運算式中使用以 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 執行階段程式庫所定義的常數。 例如，您可以使用常數 **DateInterval.Day**。 如果日期為 2008 年 1 月 10 日，則下列運算式會傳回數字 10：  
  
 `=DatePart("d",Globals!ExecutionTime)`  
  
## <a name="clr-constants"></a>CLR 常數  
 您可以在運算式中使用以 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] Common Language Runtime (CLR) 類別所定義的常數。 下表顯示系統定義色彩的範例。  
  
|持續性|描述|  
|--------------|-----------------|  
|MistyRose|當您為以背景色彩為基礎的報表屬性建立運算式時，可以依名稱指定色彩。 有效的名稱會列在 **[運算式]** 對話方塊中。|  
  
## <a name="see-also"></a>另請參閱  
 [運算式對話方塊](https://msdn.microsoft.com/library/e6c74ccb-4594-4d4f-b958-618d710e34eb)   
 [運算式 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [運算式範例 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [運算式中的資料類型 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [運算式對話方塊 &#40;報表產生器&#41;](https://msdn.microsoft.com/library/e89c4d97-5d41-4b55-8695-79329edac15d)  
  
  
