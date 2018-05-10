---
title: 在指令碼工作中使用變數 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: extending-packages-scripting
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
helpviewer_keywords:
- Foreach Loop containers
- Script task [Integration Services], variables
- scripts [Integration Services], variables
- Variables property
- Variable object
- SSIS Script task, variables
- variables [Integration Services], Script task
ms.assetid: 593b5961-4bfa-4ce1-9531-a251c34e89d3
caps.latest.revision: 63
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 11c545c6307512cb6196fd9e97d7e87dd0fd2294
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="using-variables-in-the-script-task"></a>在指令碼工作中使用變數
  變數讓指令碼工作可以和封裝中的其他物件交換資料。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 變數](../../../integration-services/integration-services-ssis-variables.md)。  
  
 指令碼工作使用 **Dts** 物件的 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Variables%2A> 屬性，讀取和寫入套件的 <xref:Microsoft.SqlServer.Dts.Runtime.Variable> 物件。  
  
> [!NOTE]  
>  <xref:Microsoft.SqlServer.Dts.Runtime.Variable> 類別的 <xref:Microsoft.SqlServer.Dts.Runtime.Variable.Value%2A> 屬性其類型為**物件**。 因為指令碼工作已啟用 **Option Strict**，所以您必須在使用它之前將 <xref:Microsoft.SqlServer.Dts.Runtime.Variable.Value%2A> 屬性轉換為適當的類型。  
  
 您將現有的變數新增至 [指令碼工作編輯器] 的 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptTask.ReadOnlyVariables%2A> 與 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptTask.ReadWriteVariables%2A> 清單中，讓它們可供自訂指令碼使用。 請記住變數名稱有區分大小寫。 在指令碼中，您可以透過 **Dts** 物件的 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Variables%2A> 屬性存取兩種類型的變數。 使用 **Value** 屬性讀取和寫入個別變數。 指令碼工作會以透明的方式管理鎖定，因為指令碼會讀取和修改變數值。  
  
 您可以在程式碼中使用變數之前，先透過 <xref:Microsoft.SqlServer.Dts.Runtime.Variables.Contains%2A> 屬性傳回的 <xref:Microsoft.SqlServer.Dts.Runtime.Variables> 集合之 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Variables%2A> 方法，檢查變數是否存在。  
  
 您也可以使用 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.VariableDispenser%2A> 屬性 (Dts.VariableDispenser) 使用指令碼工作中的變數。 在使用 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.VariableDispenser%2A>時，您必須在自己的程式碼中處理變數值的鎖定語意和資料類型的轉換。 如果您想要使用在設計階段無法使用，但是會在執行階段以程式設計方式建立的變數，可能需要使用 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.VariableDispenser%2A> 屬性，而不是 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Variables%2A> 屬性。  
  
## <a name="using-the-script-task-within-a-foreach-loop-container"></a>使用 Foreach 迴圈容器中的指令碼工作  
 當在 Foreach 迴圈容器中重複地執行指令碼工作時，指令碼通常需要使用列舉值中目前項目的內容。 例如，在使用 Foreach 檔案列舉值時，指令碼需要知道目前的檔案名稱；在使用 Foreach ADO 列舉值時，指令碼需要知道目前資料列中的資料行內容。  
  
 變數使得在 Foreach 迴圈容器與指令碼工作之間的此通訊變得可能。 在 [Foreach 迴圈編輯器] 的 [變數對應] 頁面上，將變數指派給單一列舉項目所傳回的每個資料項目。 例如，Foreach 檔案列舉值只會傳回在索引 0 的檔案名稱，因此只需要一個變數對應，然而傳回每個資料列中數個資料行的列舉值，需要您將不同的變數對應到在指令碼工作中要使用的每個資料行。  
  
 在將列舉項目對應到變數之後，就必須將對應的變數新增至 [指令碼工作編輯器] 中 [指令碼] 頁面上的 **ReadOnlyVariables** 屬性，使其可供指令碼使用。 如需處理資料夾中影像檔之 Foreach 迴圈容器中指令碼工作的範例，請參閱[以指令碼工作處理影像](../../../integration-services/extending-packages-scripting-task-examples/working-with-images-with-the-script-task.md)。  
  
## <a name="variables-example"></a>變數範例  
 下列範例示範如何存取和使用指令碼工作中的變數，以決定封裝工作流程的路徑。 此範例假設您已建立名為 `CustomerCount` 與 `MaxRecordCount` 的整數變數，並將它們新增至 [指令碼工作編輯器] 中的 **ReadOnlyVariables** 集合。 `CustomerCount` 變數包含要匯入的客戶記錄數目。 如果其值大於 `MaxRecordCount` 的值，指令碼工作會報告失敗。 當因為已超過 `MaxRecordCount` 臨界值而發生失敗時，工作流程的錯誤路徑可以實作任何所需的清除。  
  
 若要成功地編譯範例，您需要加入 Microsoft.SqlServer.ScriptTask 組件的參考。  
  
```vb  
Public Sub Main()  
  
    Dim customerCount As Integer  
    Dim maxRecordCount As Integer  
  
    If Dts.Variables.Contains("CustomerCount") = True AndAlso _  
        Dts.Variables.Contains("MaxRecordCount") = True Then  
  
        customerCount = _  
            CType(Dts.Variables("CustomerCount").Value, Integer)  
        maxRecordCount = _  
            CType(Dts.Variables("MaxRecordCount").Value, Integer)  
  
    End If  
  
    If customerCount > maxRecordCount Then  
            Dts.TaskResult = ScriptResults.Failure  
    Else  
            Dts.TaskResult = ScriptResults.Success  
    End If  
  
End Sub  
```  
  
```csharp  
using System;  
using System.Data;  
using Microsoft.SqlServer.Dts.Runtime;  
  
public class ScriptMain  
{  
  
    public void Main()  
    {  
        int customerCount;  
        int maxRecordCount;  
  
        if (Dts.Variables.Contains("CustomerCount")==true&&Dts.Variables.Contains("MaxRecordCount")==true)  
  
        {  
            customerCount = (int) Dts.Variables["CustomerCount"].Value;  
            maxRecordCount = (int) Dts.Variables["MaxRecordCount"].Value;  
  
        }  
  
        if (customerCount>maxRecordCount)  
        {  
            Dts.TaskResult = (int)ScriptResults.Failure;  
        }  
        else  
        {  
            Dts.TaskResult = (int)ScriptResults.Success;  
        }  
  
    }  
  
}  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services &#40;SSIS&#41; 變數](../../../integration-services/integration-services-ssis-variables.md)   
 [在封裝中使用變數](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)  
  
  
