---
title: 群組運算式範例 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data [Reporting Services], grouping
- grouping data
- expressions [Reporting Services], adding
- groups [Reporting Services], expressions
ms.assetid: 34cd0249-fc74-4cf2-ba11-7b072992bfd2
caps.latest.revision: 23
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: e1f8a5b296c51a5123013e8f961cf518684f27e5
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37323796"
---
# <a name="group-expression-examples-report-builder-and-ssrs"></a>群組運算式範例 (報表產生器及 SSRS)
  在資料區域中，您可以依據單一欄位來分組資料，或是建立較為複雜的運算式來識別分組的資料。 複雜運算式包含了多個欄位或參數、條件陳述式或自訂程式碼的參考。 當您為資料區定義群組時，您會將這些運算式加入到 **[群組]** 屬性。 如需詳細資訊，請參閱 [在資料區中加入或刪除群組 &#40;報表產生器及 SSRS&#41;](add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md)。  
  
 若要合併根據簡單欄位運算式的兩個或多個群組，請將每一個欄位加入到群組定義中的群組運算式清單。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="examples-of-group-expressions"></a>群組運算式的範例  
 下表提供您可用來定義群組的群組運算式範例。  
  
|描述|運算式|  
|-----------------|----------------|  
|依 `Region` 欄位分組。|`=Fields!Region.Value`|  
|依姓名分組。|`=Fields!LastName.Value`<br /><br /> `=Fields!FirstName.Value`|  
|依姓氏的第一個字母分組。|`=Fields!LastName.Value.Substring(0,1)`|  
|依使用者選取的參數分組。<br /><br /> 在此範例中， `GroupBy` 參數必須根據提供有效分組選擇的可用值清單。|`=Fields(Parameters!GroupBy.Value).Value`|  
|依三個不同的年齡範圍分組：<br /><br /> 「21 歲以下」、「21 歲到 50 歲之間」及「超過 50 歲」|`=IIF(First(Fields!Age.Value)<21,"Under 21",(IIF(First(Fields!Age.Value)>=21 AND First(Fields!Age.Value)<=50,"Between 21 and 50","Over 50")))`|  
|依多個年齡範圍分組。 此範例會示範可針對下列範圍傳回字串的自訂程式碼 (以 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] .NET 所撰寫)：<br /><br /> 25 歲或 25 歲以下<br /><br /> 26 歲到 50 歲<br /><br /> 51 歲到 75 歲<br /><br /> 超過 75 歲|`=Code.GetRangeValueByAge(Fields!Age.Value)`<br /><br /> 自訂程式碼：<br /><br /> `Function GetRangeValueByAge(ByVal age As Integer) As String`<br /><br /> `Select Case age`<br /><br /> `Case 0 To 25`<br /><br /> `GetRangeValueByByAge = "25 or Under"`<br /><br /> `Case 26 To 50`<br /><br /> `GetRangeValueByByAge = "26 to 50"`<br /><br /> `Case 51 to 75`<br /><br /> `GetRangeValueByByAge = "51 to 75"`<br /><br /> `Case Else`<br /><br /> `GetRangeValueByByAge = "Over 75"`<br /><br /> `End Select`<br /><br /> `Return GetRangeValueByByAge`<br /><br /> `End Function`|  
  
## <a name="see-also"></a>另請參閱  
 [篩選、分組和排序資料 &#40;報表產生器及 SSRS&#41;](filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [運算式範例 &#40;報表產生器及 SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [自訂程式碼及組件 References in Expressions in 報表設計工具&#40;SSRS&#41;](custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md)  
  
  
