---
title: "初始化自訂組件物件 |Microsoft 文件"
ms.custom: 
ms.date: 03/03/2017
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
- initializing custom assemblies [Reporting Services]
- custom assemblies [Reporting Services], initializing
- OnInit method
ms.assetid: 26fd74dc-d02f-40f7-aeb3-50ce05e9e6b9
caps.latest.revision: 36
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: dd3f6682e6297f86fbc4e67b98f5df48c7e94281
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="initializing-custom-assembly-objects"></a>初始化自訂組件物件
  在某些情況下，您可能需要在初始化自訂組件類別時，初始化其中的屬性與欄位值。 您很可能需要使用報表全域物件集合中可用的值，來初始化自訂類別。 您可以覆寫**OnInit**方法**程式碼**報表的物件。 若要存取**OnInit**，使用**程式碼**報表定義的項目。 有兩個技術可初始化您打算在報表中使用的自訂組件中的類別屬性或欄位值： 您可以宣告並建立您的類別使用的新執行個體**OnInit**，或您可以呼叫公開可用的方法，使用**OnInit**。  
  
## <a name="global-object-collections-and-initialization"></a>全域物件集合與初始化  
 有幾個集合可供您初始化自訂類別變數。 您可以使用**Globals**和**使用者**集合。 **參數**，**欄位**和**ReportItems**集合不是可供您使用的報表生命週期中的點時**OnInit**叫用方法。 若要使用共用的集合、 **Globals**或**使用者**，您需要包含**報表**物件參考。 比方說，來初始化自訂類別依據的目前語言的使用者存取報表，您**程式碼**項目可能如下所示：  
  
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
  
 初始化自訂組件中類別的屬性和欄位值的另一種方式是呼叫公開可用的方法，您定義從**OnInit**方法。 您必須先為報表定義檔案中的類別加入執行個體名稱。 一旦您加入適當的組件參考與執行個體名稱，就可以呼叫初始化方法以初始化類別的屬性與欄位值。 您**OnInit**方法可能看起來如下所示：  
  
```  
<Code>  
   Protected Overrides Sub OnInit()  
      m_myClass.MyInitializationMethod(Report.User!Language, _  
         Report.Globals!ExecutionTime)  
   End Sub  
</Code>  
```  
  
 如需新增自訂類別的組件參考與執行個體名稱的詳細資訊，請參閱[將組件參考加入報表 &#40;SSRS &#41;](../../reporting-services/report-design/add-an-assembly-reference-to-a-report-ssrs.md).  
  
 如需全域物件集合的詳細資訊，請參閱[運算式 &#40; 中的內建集合報表產生器及 SSRS &#41;](../../reporting-services/report-design/built-in-collections-in-expressions-report-builder.md).  
  
## <a name="see-also"></a>另請參閱  
 [報表中使用自訂組件](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)  
  
  
