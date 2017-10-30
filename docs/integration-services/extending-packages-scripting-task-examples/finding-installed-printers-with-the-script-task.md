---
title: "尋找安裝的印表機 with the Script Task |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
helpviewer_keywords:
- System.Drawing.Printing namespace
- printers [Integration Services]
- SSIS Script task, printers
- locating printers
- Printing namespace
- Script task [Integration Services], examples
- finding printers [SQL Server]
- Script task [Integration Services], printers
ms.assetid: 50a55014-e2c3-4ecd-84e1-3e877c55a260
caps.latest.revision: 32
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 4a8ade977c971766c8f716ae5f33cac606c8e22d
ms.openlocfilehash: 1de1fae5c30648eba7cb62840ef3ff9f9aac13f9
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="finding-installed-printers-with-the-script-task"></a>以指令碼工作尋找安裝的印表機
  由 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝轉換的資料通常有列印的報表，做為其最終的目的地。 **System.Drawing.Printing**命名空間中的[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]提供使用印表機的類別。  
  
> [!NOTE]  
>  如果您想要建立可更輕鬆地在多個封裝之間重複使用的工作，請考慮使用此指令碼工作範例中的程式碼做為自訂工作的起點。 如需詳細資訊，請參閱 [開發自訂工作](../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md)。  
  
## <a name="description"></a>Description  
 下列範例找到安裝在伺服器上支援 Legal Size 紙張 (用於美國) 的印表機。 檢查支援紙張大小的程式碼是封裝在私用函數中。 為了讓您在指令碼檢查每台印表機的設定時，追蹤指令碼的進度，指令碼使用 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Log%2A> 方法，來針對使用 Legal Size 紙張的印表機引發參考用訊息，並為沒有 Legal Size 紙張的印表機引發警告。 這些訊息會出現在**輸出**視窗[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA) IDE，當您在設計工具中執行封裝。  
  
#### <a name="to-configure-this-script-task-example"></a>設定此指令碼工作範例  
  
1.  建立名為的變數`PrinterList`類型**物件**。  
  
2.  在**指令碼**頁面**指令碼工作編輯器**，將此變數加入至 [readwritevariables] 屬性。  
  
3.  在指令碼專案中，加入的參考**System.Drawing**命名空間。  
  
4.  在程式碼中，使用**匯入**陳述式匯入**System.Collections**和**System.Drawing.Printing**命名空間。  
  
### <a name="code"></a>程式碼  
  
```vb  
Public Sub Main()  
  
    Dim printerName As String  
    Dim currentPrinter As New PrinterSettings  
    Dim size As PaperSize  
  
    Dim printerList As New ArrayList  
    For Each printerName In PrinterSettings.InstalledPrinters  
        currentPrinter.PrinterName = printerName  
        If PrinterHasLegalPaper(currentPrinter) Then  
            printerList.Add(printerName)  
            Dts.Events.FireInformation(0, "Example", _  
                "Printer " & printerName & " has legal paper.", _  
                String.Empty, 0, False)  
        Else  
            Dts.Events.FireWarning(0, "Example", _  
                "Printer " & printerName & " DOES NOT have legal paper.", _  
                String.Empty, 0)  
        End If  
    Next  
  
    Dts.Variables("PrinterList").Value = printerList  
  
    Dts.TaskResult = ScriptResults.Success  
  
End Sub  
  
Private Function PrinterHasLegalPaper( _  
    ByVal thisPrinter As PrinterSettings) As Boolean  
  
    Dim size As PaperSize  
    Dim hasLegal As Boolean = False  
  
    For Each size In thisPrinter.PaperSizes  
        If size.Kind = PaperKind.Legal Then  
            hasLegal = True  
        End If  
    Next  
  
    Return hasLegal  
  
End Function  
```  
  
```csharp  
public void Main()  
        {  
  
            PrinterSettings currentPrinter = new PrinterSettings();  
            PaperSize size;  
            Boolean Flag = false;  
  
            ArrayList printerList = new ArrayList();  
            foreach (string printerName in PrinterSettings.InstalledPrinters)  
            {  
                currentPrinter.PrinterName = printerName;  
                if (PrinterHasLegalPaper(currentPrinter))  
                {  
                    printerList.Add(printerName);  
                    Dts.Events.FireInformation(0, "Example", "Printer " + printerName + " has legal paper.", String.Empty, 0, ref Flag);  
                }  
                else  
                {  
                    Dts.Events.FireWarning(0, "Example", "Printer " + printerName + " DOES NOT have legal paper.", String.Empty, 0);  
                }  
            }  
  
            Dts.Variables["PrinterList"].Value = printerList;  
  
            Dts.TaskResult = (int)ScriptResults.Success;  
  
        }  
  
        private bool PrinterHasLegalPaper(PrinterSettings thisPrinter)  
        {  
  
            bool hasLegal = false;  
  
            foreach (PaperSize size in thisPrinter.PaperSizes)  
            {  
                if (size.Kind == PaperKind.Legal)  
                {  
                    hasLegal = true;  
                }  
            }  
  
            return hasLegal;  
  
        }  
```  
  
## <a name="see-also"></a>另請參閱  
 [指令碼工作範例](../../integration-services/extending-packages-scripting-task-examples/script-task-examples.md)  
  
  

