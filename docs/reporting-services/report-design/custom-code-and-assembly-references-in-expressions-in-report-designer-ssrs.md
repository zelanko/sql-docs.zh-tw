---
title: "自訂程式碼和組件 References in Expressions in Report Designer (SSRS) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- items [Reporting Services], expressions
- data [Reporting Services], expressions
- expressions [Reporting Services], about expressions
- expressions [Reporting Services]
- SSRS, expressions
- formulas [Reporting Services]
- data manipulation [Reporting Services]
- SQL Server Reporting Services, expressions
ms.assetid: ae8a0166-2ccc-45f4-8d28-c150da7b73de
caps.latest.revision: 77
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: dc8491006425de79f8e96be1affb10687a1553f9
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs"></a>報表產生器中運算式的自訂程式碼及組件參考 (SSRS)
  您可以加入內嵌於報表之自訂程式碼的參考，或是建置並儲存至電腦以及部署至報表伺服器之自訂組件的參考。 請將內嵌程式碼用在自訂常數、複雜函數或在單一報表內重複使用的函數上。 請使用自訂程式碼組件，將程式碼維護在單一位置並共用程式碼，讓多份報表使用。 自訂程式碼可能會包含新的自訂常數、變數、函數或副程式。 您可以包含內建集合 (例如 Parameters 集合) 的唯讀參考， 但是不能將報表資料值集傳遞至自訂函數 (尤其是不支援自訂彙總)。  
  
> [!IMPORTANT]  
>  對於時間緊迫的計算 (在執行階段時會評估一次，而您想在整個報表處理期間維持相同的值)，則請考慮是否要使用報表變數或群組變數。 如需詳細資訊，請參閱[報表和群組變數集合參考 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/built-in-collections-report-and-group-variables-references-report-builder.md)。  
  
 報表設計師是將自訂程式碼加入至報表的慣用撰寫環境。 報表產生器支援處理具有有效運算式的報表，或是包含報表伺服器上自訂組件之參考的報表。 報表產生器不會提供加入自訂組件之參考的方式。  
  
> [!NOTE]  
>  請注意，在升級報表伺服器期間，相依於自訂組件的報表可能需要進行其他步驟，才能完成升級。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="RB3"></a> 在報表產生器中使用自訂程式碼  
 在報表產生器中，您可以從報表伺服器開啟包含自訂組件之參考的報表。 例如，您可以編輯在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中使用報表設計師所建立和部署的報表。 自訂組件必須部署至報表伺服器。  
  
 您無法執行下列工作：  
  
1.  將參考或類別成員執行個體加入至報表。  
  
2.  在本機模式中預覽含有自訂組件之參考的報表。  
  
##  <a name="Common"></a> 包含常用函數的參考  
 **[運算式]** 對話方塊可用來檢視 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]一般內建函數的分類清單。 當您展開 **[一般函數]** 並按一下類別目錄時， **[項目]** 窗格就會顯示您包含在運算式中的函數清單。 一般函數包含的類別[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]<xref:System.Math>和<xref:System.Convert>命名空間和[!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]執行階段程式庫函式。 為了方便起見，您可以在 **[運算式]** 對話方塊中檢視最常用的函數，這些函數會依類別目錄列出：文字、日期和時間、數學、檢閱、程式流程、彙總、財務、轉換和其他。 較不常用的函數則不會顯示在清單中，但仍可用於運算式。  
  
 若要使用內建函數，請在 [項目] 窗格中的函數名稱上按兩下。 函數的描述會顯示在 [描述] 窗格中，函數呼叫的範例則顯示在 [範例] 窗格中。 當您在程式碼窗格中輸入函數名稱，且其後接著左括號 **(**時，IntelliSense 會協助顯示該函數呼叫的每個有效語法。 例如，若要計算資料表中名為 `Quantity` 欄位的最大值，請將簡單運算式 `=Max(` 加入至 [程式碼] 窗格，然後使用智慧標籤來檢視該函數呼叫的所有有效語法。 若要完成此範例，請輸入 `=Max(Fields!Quantity.Value)`。  
  
 如需有關每個函式的詳細資訊，請參閱<xref:System.Math>， <xref:System.Convert>，和[Visual Basic 執行階段程式庫成員](http://go.microsoft.com/fwlink/?LinkId=198941)MSDN 上。  
  
##  <a name="NotCommon"></a> 包含較少使用函數的參考  
 若要包含其他較不常使用的 CLR 命名空間的參考，您必須，例如使用完整的參考， <xref:System.Text.StringBuilder>。 在這些較少使用函數的 **[運算式]** 對話方塊的程式碼窗格中，不支援 IntelliSense。  
  
 如需詳細資訊，請參閱 MSDN 上的 [Visual Basic 執行階段程式庫成員](http://go.microsoft.com/fwlink/?LinkId=198941) 。  
  
##  <a name="External"></a> 包含外部組件的參考  
 若要包含外部組件中類別的參考，您必須為報表處理器識別組件。 請使用 **[報表屬性]** 對話方塊的 **[參考]** 頁面來指定報表中要加入之組件的完整名稱。 您必須在運算式中使用組件中類別的完整名稱。 外部組件中的類別並不會顯示在 **[運算式]** 對話方塊中，您必須提供正確的類別名稱。 完整名稱包含命名空間、類別名稱和成員名稱。  
  
##  <a name="Embedded"></a> 加入內嵌程式碼  
 若要將內嵌程式碼加入至報表，請使用 **[報表屬性]** 對話方塊的 [程式碼] 索引標籤。 您建立的程式碼區塊可以包含多個方法。 內嵌程式碼中的方法必須用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 來撰寫，且必須以執行個體為基礎。 報表處理器會自動加入 System.Convert 和 System.Math 命名空間的參考。 請使用 **[報表屬性]** 對話方塊的 **[參考]** 頁面來加入其他的組件參考。 如需詳細資訊，請參閱 [將組件參考加入至報表 &#40;SSRS&#41;](../../reporting-services/report-design/add-an-assembly-reference-to-a-report-ssrs.md)。  
  
 內嵌程式碼裡的方法，可透過全域定義的 **Code** 成員使用。 您可藉由參考 **Code** 成員與方法名稱，來存取這些方法。 下列範例會呼叫 **ToUSD**方法，這個方法會將 `StandardCost` 欄位的值轉換成美金值：  
  
```  
=Code.ToUSD(Fields!StandardCost.Value)  
```  
  
 若要參考自訂程式碼中的內建集合，請加入內建 **Report** 物件的參考：  
  
```  
=Report.Parameters!Param1.Value  
```  
  
 下列範例顯示定義部分自訂常數及變數的方法。  
  
```  
Public Const MyNote = "Authored by Bob"  
Public Const NCopies As Int32 = 2  
Public Dim  MyVersion As String = "123.456"  
Public Dim MyDoubleVersion As Double = 123.456  
```  
  
 雖然自訂常數不會出現在 **[運算式]** 對話方塊的 **[常數]** 類別目錄中 (這個類別目錄只會顯示內建常數)，但是您可以從任何運算式加入自訂常數的參考，如下列範例所示。 在運算式中，會將自訂常數視為 **Variant**。  
  
```  
=Code.MyNote  
=Code.NCopies  
=Code.MyVersion  
=Code.MyDoubleVersion  
```  
  
 下列範例包含 **FixSpelling**函數的程式碼參考和程式碼實作，這個函數會將 `"Bicycle"` 欄位中所有出現的 "Bike" 文字取代成 `SubCategory` 文字。  
  
 `=Code.FixSpelling(Fields!SubCategory.Value)`  
  
 將下列程式碼內嵌在報表定義程式碼區塊之後，會顯示 **FixSpelling** 方法的實作。 此範例示範如何使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] **StringBuilder** 類別的完整參考。  
  
```vb  
Public Function FixSpelling(ByVal s As String) As String  
   Dim strBuilder As New System.Text.StringBuilder(s)  
   If s.Contains("Bike") Then  
      strBuilder.Replace("Bike", "Bicycle")  
      Return strBuilder.ToString()  
      Else : Return s  
   End If  
End Function  
```  
  
 如需內建物件集合和初始化的詳細資訊，請參閱[內建的全域和使用者參考 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/built-in-collections-built-in-globals-and-users-references-report-builder.md) 和[初始化自訂組件物件](../../reporting-services/custom-assemblies/initializing-custom-assembly-objects.md)。  
  
##  <a name="Parameters"></a> 加入程式碼中參數的參考  
 您可以透過報表定義之程式碼區塊內或您所提供之自訂組件內的自訂程式碼，參考全域參數集合。 此參數集合是唯讀的，而且沒有任何公用 Iterator。 您不能使用 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] **For Each** 建構來逐步執行此集合。 您必須先知道報表定義中所定義的參數名稱，才可以在程式碼中參考它。 但是，您可以逐一查看多重值參數的所有值。  
  
 下表包含從自訂程式碼參考內建 `Parameters` 集合的範例：  
  
 **將整個全域參數集合傳遞給自訂程式碼。**這個函數會傳回特定報表參數 *MyParameter*的值。  
  
 運算式中的參考 `=Code.DisplayAParameterValue(Parameters)`  
  
 自訂程式碼定義  
  
```  
Public Function DisplayAParameterValue(ByVal parameters as Parameters) as Object  
Return parameters("MyParameter").Value  
End Function  
```  
  
 **將個別參數傳遞給自訂程式碼。**  
  
 運算式中的參考 `=Code.ShowParametersValues(Parameters!DayOfTheWeek)`  
  
 這個範例會傳回所傳入的參數值。 如果該參數為多重值參數，則傳回字串會是所有值的串連。  
  
 自訂程式碼定義  
  
```  
Public Function ShowParameterValues(ByVal parameter as Parameter)  
 as String  
   Dim s as String   
   If parameter.IsMultiValue then  
      s = "Multivalue: "   
      For i as integer = 0 to parameter.Count-1  
         s = s + CStr(parameter.Value(i)) + " "   
      Next  
   Else  
      s = "Single value: " + CStr(parameter.Value)  
   End If  
   Return s  
End Function  
```  
  
##  <a name="Custom"></a> 加入自訂組件中程式碼的參考  
 若要在報表中使用自訂組件，您必須先建立組件，並設定報表設計師可以使用該組件，在報表中加入對該組件的參考，然後在報表中使用運算式來參考該組件內含的方法。 報表部署至報表伺服器時，您也必須將自訂組件部署至報表伺服器。  
  
 如需建立自訂組件，並讓 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]可以使用組件的資訊，請參閱 [將自訂組件與報表搭配使用](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)。  
  
 若要在運算式中參考自訂程式碼，您必須在組件中呼叫類別的成員。 該如何完成，取決於此方法為靜態或以執行個體為基礎。 報表內的全域都可以使用自訂組件內的靜態方法。 您可以藉著指定命名空間、類別和方法名稱，來存取運算式中的靜態方法。 下列範例會呼叫 **ToGBP**方法，這個方法會將 **StandardCost** 欄位值從美元轉換為英鎊：  
  
```  
=CurrencyConversion.DollarCurrencyConversion.ToGBP(Fields!StandardCost.Value)  
```  
  
 以執行個體為基礎的方法，可透過全域定義的 **Code** 成員來使用。 您可以藉由參考 **Code** 成員，然後參考執行個體與方法名稱，來存取這些方法。 下列範例會呼叫 **ToEUR**執行個體方法，這個方法會將 **StandardCost** 欄位值從美元轉換為歐元：  
  
```  
=Code.m_myDollarCoversion.ToEUR(Fields!StandardCost.Value)  
```  
  
> [!NOTE]  
>  在 [報表設計師] 中，自訂組件會載入一次，然後在關閉 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]之前，都不會卸載。 如果您要預覽報表，請變更報表中使用的自訂組件，然後再次預覽報表，在第二次預覽中將不會顯示變更。 若要重新載入組件，請關閉再重新開啟 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ，再預覽報表。  
  
 如需有關存取程式碼的詳細資訊，請參閱＜ [Accessing Custom Assemblies Through Expressions](../../reporting-services/custom-assemblies/accessing-custom-assemblies-through-expressions.md)＞。  
  
##  <a name="collections"></a> 將內建集合傳給自訂組件  
 若要將內建集合 (例如 *Globals* 或 *Parameters* 集合) 傳給自訂組件處理，必須將程式碼專案中的組件參考加入定義內建集合的組件，並且存取正確的命名空間。 根據您是針對在報表伺服器上執行的報表 (伺服器報表) 還是以本機方式在 .NET 應用程式中執行的報表 (本機報表) 開發自訂組件，您需要參考的組件會有所不同。 如需詳細資訊，請參閱後文。  
  
-   **命名空間** ：Microsoft.ReportingServices.ReportProcessing.ReportObjectModel  
  
-   **組件 (本機報表)** ：Microsoft.ReportingServices.ProcessingObjectModel.dll  
  
-   **組件 (伺服器報表)** ：Microsoft.ReportViewer.ProcessingObjectModel.dll  
  
 由於 *Fields* 和 *ReportItems* 集合的內容可能會在執行階段動態變更，因此您不應將這些不同的呼叫內容保留在自訂組件之中 (例如保留在成員變數中)。 此項建議適用於所有的內建集合。  
  
## <a name="see-also"></a>請參閱＜  
 [將程式碼加入至報表 &#40;SSRS&#41;](../../reporting-services/report-design/add-code-to-a-report-ssrs.md)   
 [將自訂組件與報表搭配使用](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)   
 [將組件參考加入至報表 &#40;SSRS&#41;](../../reporting-services/report-design/add-an-assembly-reference-to-a-report-ssrs.md)   
 [Reporting Services 教學課程 &#40;SSRS&#41;](../../reporting-services/reporting-services-tutorials-ssrs.md)   
 [運算式範例 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [報表範例 (報表產生器和 SSRS)](http://go.microsoft.com/fwlink/?LinkId=198283)  
  
  
