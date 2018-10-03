---
title: 撰寫自訂 Foreach 列舉值的程式碼 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- integration-services
ms.topic: reference
helpviewer_keywords:
- custom foreach enumerators [Integration Services], coding
ms.assetid: 279cf6de-d06f-40e7-b8ca-569310449f36
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 7451a7d6cdb93e4c5ab6d66e240d3a5c14ff4b59
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48134768"
---
# <a name="coding-a-custom-foreach-enumerator"></a>撰寫自訂 Foreach 列舉值的程式碼
  建立繼承自 <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator> 基底類別的類別，並將 <xref:Microsoft.SqlServer.Dts.Runtime.DtsForEachEnumeratorAttribute> 屬性 (attribute) 套用到類別之後，必須覆寫基底類別的屬性 (properties) 與方法的實作，才可提供自訂功能。  
  
 如需自訂列舉值的工作範例，請參閱[開發自訂 ForEach 列舉值的使用者介面](developing-a-user-interface-for-a-custom-foreach-enumerator.md)。  
  
## <a name="initializing-the-enumerator"></a>初始化列舉值  
 您可以覆寫 <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator.InitializeForEachEnumerator%2A> 方法，以快取定義在封裝中的連接管理員參考，並快取可用以引發錯誤、警告和參考用訊息的事件介面參考。  
  
## <a name="validating-the-enumerator"></a>驗證列舉值  
 您覆寫 <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator.Validate%2A> 方法，以驗證已正確設定的列舉值。 如果該方法傳回 `Failure`，將不會執行列舉值和含有列舉值的封裝。 這個方法的實作會隨每個列舉值而有所不同，但是如果列舉值依賴 <xref:Microsoft.SqlServer.Dts.Runtime.Variable> 或 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 物件，就應該加入程式碼以確認提供給該方法之集合中有這些物件。  
  
 下列程式碼範例將示範 <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator.Validate%2A> 的實作，以檢查列舉值屬性中所指定的變數。  
  
```csharp  
private string variableNameValue;  
  
public string VariableName  
{  
    get{ return this.variableNameValue; }  
    set{ this.variableNameValue = value; }  
}  
  
public override DTSExecResult Validate(Connections connections, VariableDispenser variableDispenser, IDTSInfoEvents infoEvents, IDTSLogging log)  
{  
    if (!variableDispenser.Contains(this.variableNameValue))  
    {  
        infoEvents.FireError(0, "MyEnumerator", "The Variable " + this.variableNameValue + " does not exist in the collection.", "", 0);  
            return DTSExecResult.Failure;  
    }  
    return DTSExecResult.Success;  
}  
```  
  
```vb  
Private variableNameValue As String  
  
Public Property VariableName() As String  
    Get   
         Return Me.variableNameValue  
    End Get  
    Set (ByVal Value As String)   
         Me.variableNameValue = value  
    End Set  
End Property  
  
Public Overrides Function Validate(ByVal connections As Connections, ByVal variableDispenser As VariableDispenser, ByVal infoEvents As IDTSInfoEvents, ByVal log As IDTSLogging) As DTSExecResult  
    If Not variableDispenser.Contains(Me.variableNameValue) Then  
        infoEvents.FireError(0, "MyEnumerator", "The Variable " + Me.variableNameValue + " does not exist in the collection.", "", 0)  
            Return DTSExecResult.Failure  
    End If  
    Return DTSExecResult.Success  
End Function  
```  
  
## <a name="returning-the-collection"></a>傳回集合  
 在執行期間，<xref:Microsoft.SqlServer.Dts.Runtime.ForEachLoop> 容器會呼叫自訂列舉值的 <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator.GetEnumerator%2A> 方法。 在此方法中，列舉值會建立和擴展其項目集合，然後傳回該集合。 <xref:Microsoft.SqlServer.Dts.Runtime.ForEachLoop> 接著會反覆運算集合中的項目，並為集合中的每個項目執行其控制流程。  
  
 下列程式碼範例顯示會傳回隨機整數陣列的 <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator.GetEnumerator%2A> 實作。  
  
```csharp  
public override object GetEnumerator()  
{  
    ArrayList numbers = new ArrayList();  
  
    Random randomNumber = new Random(DateTime.Now);  
  
    for( int x=0; x < 100; x++ )  
        numbers.Add( randomNumber.Next());  
  
    return numbers;  
}  
```  
  
```vb  
Public Overrides Function GetEnumerator() As Object  
    Dim numbers As ArrayList =  New ArrayList()   
  
    Dim randomNumber As Random =  New Random(DateTime.Now)   
  
        Dim x As Integer  
        For  x = 0 To  100- 1  Step  x + 1  
        numbers.Add(randomNumber.Next())  
        Next  
  
    Return numbers  
End Function  
```  
  
![Integration Services 圖示 （小）](../../media/dts-16.gif "Integration Services 圖示 （小）")**保持最多包含 Integration Services 的日期** <br /> 若要取得 Microsoft 的最新下載、文件、範例和影片以及社群中的精選解決方案，請瀏覽 MSDN 上的 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 頁面：<br /><br /> [瀏覽 MSDN 上的 Integration Services 頁面](http://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要得到這些更新的自動通知，請訂閱該頁面上所提供的 RSS 摘要。  
  
## <a name="see-also"></a>另請參閱  
 [建立自訂的 Foreach 列舉值](creating-a-custom-foreach-enumerator.md)   
 [開發自訂 Foreach 列舉程式的使用者介面](developing-a-user-interface-for-a-custom-foreach-enumerator.md)  
  
  
