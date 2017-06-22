---
title: "透過運算式存取自訂組件 |Microsoft 文件"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- expressions [Reporting Services], custom assemblies
- static member calls
- instance member calls [Reporting Services]
- calling class members
- custom assemblies [Reporting Services], expressions
ms.assetid: 917c4d47-1a95-4f54-98b1-e8cb2165d90f
caps.latest.revision: 32
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 70ff488827e5289d401bf62b67a82a08ecc25f70
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="accessing-custom-assemblies-through-expressions"></a>透過運算式存取自訂組件
  一旦您建立自訂組件，請將它提供給報表設計師或是報表伺服器、加入適當的安全性原則，以及將參考加入報表定義中的自訂組件，這樣您就可以使用報表運算式來存取組件中的類別成員。 若要在運算式中參考自訂程式碼，您必須在組件中呼叫類別的成員。 該如何完成，取決於此方法為靜態或以執行個體為基礎。  
  
## <a name="calling-static-members-from-a-report-definition-file"></a>呼叫報表定義檔案中的靜態成員  
 靜態成員屬於類別或是類型本身，而且不屬於具現化物件。 存取這些成員的方式是從類別直接呼叫它們。 您應該盡可能使用靜態成員呼叫報表中的自訂涵數，因為靜態成員的表現最好。 若要呼叫靜態成員，您需要以運算式的形式來參考它 =*Namespace.Class.Method*。  
  
#### <a name="to-call-static-members"></a>呼叫靜態成員  
  
-   若要呼叫靜態成員，請將運算式設定為等於成員的完整名稱，它包含命名空間、類別名稱和成員名稱。 下列範例會呼叫**ToGBP**方法，將轉換**StandardCost**欄位值從美元轉換為英鎊，並顯示在報表中：  
  
    ```  
    =CurrencyConversion.DollarCurrencyConversion.ToGBP(Fields!StandardCost.Value)  
    ```  
  
### <a name="important-information-regarding-static-fields-and-properties"></a>有關靜態欄位與屬性的重要資訊  
 目前，會在相同的應用程式網域中執行所有的報表。 這表示含有使用者特定的靜態資料會向相同報表的其他執行個體公開此資料。 這個情況可能會使一個使用者的靜態資料，可供目前執行特定報表的所有使用者使用。 基於這個理由，強烈建議您不要使用靜態欄位或屬性的自訂組件中或在**程式碼**項目; 相反地，在報表中使用的執行個體欄位或屬性。 靜態方法仍然可以使用，因為它們不會儲存狀態或是資料。  
  
## <a name="calling-instance-members-from-a-report-definition-file"></a>呼叫報表定義檔案中的執行個體成員  
 如果您的自訂組件包含需要在報表定義中存取的執行個體成員，則必須將類別的執行個體名稱加入報表。 您可以新增使用類別的執行個體名稱**程式碼** 索引標籤**報表屬性**對話方塊。 如需有關如何將類別的執行個體加入至報表的詳細資訊，請參閱[Code and Assembly References in Expressions 在報表設計工具 &#40;SSRS &#41;](../../reporting-services/report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md).  
  
 若要呼叫靜態成員，您要參考運算式，其格式為 = Code*。.Instancename.method*。  
  
#### <a name="to-call-instance-members"></a>呼叫執行個體成員  
  
-   若要呼叫自訂組件的執行個體成員，您必須參考**程式碼**關鍵字後面接著執行個體名稱和方法。 下列範例會呼叫執行個體方法**ToEUR**轉換**StandardCost**欄位值從美元，歐元，並顯示在報表中：  
  
    ```  
    =Code.m_myDollarCoversion.ToEUR(Fields!StandardCost.Value)  
    ```  
  
## <a name="see-also"></a>另請參閱  
 [報表中使用自訂組件](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)  
  
  
