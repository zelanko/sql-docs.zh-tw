---
title: 初始化自訂組件物件 | Microsoft Docs
ms.date: 03/03/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: custom-assemblies
ms.suite: pro-bi
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- initializing custom assemblies [Reporting Services]
- custom assemblies [Reporting Services], initializing
- OnInit method
ms.assetid: 26fd74dc-d02f-40f7-aeb3-50ce05e9e6b9
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 8f2b0db93d96c88fede36acba3b04999a08ca737
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/30/2018
ms.locfileid: "43280315"
---
# <a name="initializing-custom-assembly-objects"></a>初始化自訂組件物件
  在某些情況下，您可能需要在初始化自訂組件類別時，初始化其中的屬性與欄位值。 您很可能需要使用報表全域物件集合中可用的值，來初始化自訂類別。 您可以透過覆寫報表之 **Code** 物件的 **OnInit** 方法來完成。 若要存取 **OnInit**，請使用報表定義的 **Code** 項目。 有兩個技術可初始化您計劃在報表中使用的自訂組件中類別之屬性或欄位值。您可以使用 **OnInit** 來宣告和建立類別的新執行個體，或者您可以使用 **OnInit** 來呼叫公開可用的方法。  
  
## <a name="global-object-collections-and-initialization"></a>全域物件集合與初始化  
 有幾個集合可供您初始化自訂類別變數。 您可以使用 **Globals** 和 **User** 集合。 叫用 **OnInit** 方法時，無法在報表生命週期內使用 **Parameters**、**Fields** 和 **ReportItems** 集合。 若要使用共用集合 **Globals** 或 **User**，您需要加入 **Report** 物件參考。 例如，若要根據存取報表之使用者的目前語言來初始化您的自訂類別，您的 **Code** 項目可能看起來如下所示：  
  
```  
<Code>  
   Dim m_myClass As MyClass  
  
   Protected Overrides Sub OnInit()  
      m_myClass = new MyClass(Report.User!Language, _  
         Report.Globals!ExecutionTime)  
   End Sub  
</Code>  
```  
  
 如前所示，有一種方法可以初始化類別的屬性和欄位值，就是呼叫覆寫的建構函式，以宣告類別並建立該類別的新執行個體。  
  
 在自訂組件中初始化類別之屬性與欄位值的另一種方法，是呼叫從 **OnInit** 方法定義之公開可用的方法。 您必須先為報表定義檔案中的類別加入執行個體名稱。 一旦您加入適當的組件參考與執行個體名稱，就可以呼叫初始化方法以初始化類別的屬性與欄位值。 您的 **OnInit** 方法可能如下所示：  
  
```  
<Code>  
   Protected Overrides Sub OnInit()  
      m_myClass.MyInitializationMethod(Report.User!Language, _  
         Report.Globals!ExecutionTime)  
   End Sub  
</Code>  
```  
  
 如需新增自訂類別的組件參考與執行個體名稱的詳細資訊，請參閱[將組件參考新增至報表 &#40;SSRS&#41;](../../reporting-services/report-design/add-an-assembly-reference-to-a-report-ssrs.md)。  
  
 如需全域物件集合的詳細資訊，請參閱[運算式中的內建集合 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/built-in-collections-in-expressions-report-builder.md)。  
  
## <a name="see-also"></a>另請參閱  
 [將自訂組件與報表搭配使用](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)  
  
  
