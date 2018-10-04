---
title: 透過運算式存取自訂組件 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.topic: reference
helpviewer_keywords:
- expressions [Reporting Services], custom assemblies
- static member calls
- instance member calls [Reporting Services]
- calling class members
- custom assemblies [Reporting Services], expressions
ms.assetid: 917c4d47-1a95-4f54-98b1-e8cb2165d90f
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: b8870f37741a26f99065f41f0231cea8b22b2770
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48102658"
---
# <a name="accessing-custom-assemblies-through-expressions"></a>透過運算式存取自訂組件
  一旦您建立自訂組件，請將它提供給報表設計師或是報表伺服器、加入適當的安全性原則，以及將參考加入報表定義中的自訂組件，這樣您就可以使用報表運算式來存取組件中的類別成員。 若要在運算式中參考自訂程式碼，您必須在組件中呼叫類別的成員。 該如何完成，取決於此方法為靜態或以執行個體為基礎。  
  
## <a name="calling-static-members-from-a-report-definition-file"></a>呼叫報表定義檔案中的靜態成員  
 靜態成員屬於類別或是類型本身，而且不屬於具現化物件。 存取這些成員的方式是從類別直接呼叫它們。 您應該盡可能使用靜態成員呼叫報表中的自訂涵數，因為靜態成員的表現最好。 若要呼叫靜態成員，您需要以運算式的形式加以參考，其格式為 =*Namespace.Class.Method*。  
  
#### <a name="to-call-static-members"></a>呼叫靜態成員  
  
-   若要呼叫靜態成員，請將運算式設定為等於成員的完整名稱，它包含命名空間、類別名稱和成員名稱。 下列範例會呼叫 **ToGBP** 方法，這個方法會將 **StandardCost** 欄位值從美元轉換為英鎊，並將其顯示在報表中：  
  
    ```  
    =CurrencyConversion.DollarCurrencyConversion.ToGBP(Fields!StandardCost.Value)  
    ```  
  
### <a name="important-information-regarding-static-fields-and-properties"></a>有關靜態欄位與屬性的重要資訊  
 目前，會在相同的應用程式網域中執行所有的報表。 這表示含有使用者特定的靜態資料會向相同報表的其他執行個體公開此資料。 這個情況可能會使一個使用者的靜態資料，可供目前執行特定報表的所有使用者使用。 基於這個理由，強烈建議您不要在自訂組件或是在 **Code** 元素中使用靜態欄位或是屬性；請改在報表中用執行個體欄位或是屬性。 靜態方法仍然可以使用，因為它們不會儲存狀態或是資料。  
  
## <a name="calling-instance-members-from-a-report-definition-file"></a>呼叫報表定義檔案中的執行個體成員  
 如果您的自訂組件包含需要在報表定義中存取的執行個體成員，則必須將類別的執行個體名稱加入報表。 您可以使用 [報表屬性] 對話方塊的 [程式碼] 索引標籤，來為類別新增執行個體名稱。 如需詳細資訊，請參閱[報表設計師中運算式的自訂程式碼及組件參考 &#40;SSRS&#41;](../report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md)。  
  
 若要呼叫靜態成員，您需要以運算式的形式加以參考，其格式為 =Code *.InstanceName.Method*。  
  
#### <a name="to-call-instance-members"></a>呼叫執行個體成員  
  
-   若要呼叫自訂組件的執行個體成員，您必須參考 **Code** 關鍵字，加上執行個體名稱及方法。 下列範例會呼叫 **ToEUR** 執行個體方法，這個方法會將 **StandardCost** 欄位值從美元轉換為歐元，並將其顯示在報表中：  
  
    ```  
    =Code.m_myDollarCoversion.ToEUR(Fields!StandardCost.Value)  
    ```  
  
## <a name="see-also"></a>另請參閱  
 [將自訂組件與報表搭配使用](using-custom-assemblies-with-reports.md)  
  
  
