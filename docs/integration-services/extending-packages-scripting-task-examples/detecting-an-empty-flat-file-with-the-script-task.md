---
title: "以指令碼工作偵測空的一般檔案 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-scripting-task-examples
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- flat files
- Script task [Integration Services], empty flat files
- SSIS Script task, empty flat files
- Script task [Integration Services], examples
ms.assetid: 1b4defb8-886a-483d-8056-d1b91d37bc90
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a722343ed2a7cc0afcdb62d9871efeb26945ffd4
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="detecting-an-empty-flat-file-with-the-script-task"></a>以指令碼工作偵測空的一般檔案
  一般檔案來源不會在嘗試處理一般檔案之前，判斷它是否包含資料列。 您可能會想要略過不包含任何資料列的檔案，藉以改善封裝的效率，尤其是逐一查看許多一般檔案的封裝。 指令碼工作可以在封裝開始處理資料流程之前，尋找空白的一般檔案。  
  
> [!NOTE]  
>  如果您想要建立可更輕鬆地在多個封裝之間重複使用的工作，請考慮使用此指令碼工作範例中的程式碼做為自訂工作的起點。 如需詳細資訊，請參閱 [開發自訂工作](../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md)。  
  
## <a name="description"></a>描述  
 下列範例會使用 **System.IO** 命名空間的方法來測試一般檔案連線管理員中指定的一般檔案，以便判斷此檔案是否空白，或者它是否僅包含預期的非資料列，例如資料行標頭或空白的行。 此指令碼會先檢查檔案的大小。如果大小為零個位元組，表示檔案是空白的。 如果檔案大小大於零，此指令碼就會從檔案中讀取各行，直到沒有其他行為止，或者直到行數超過預期的非資料列數目為止。 如果檔案中的行數小於或等於預期的非資料列數目，此檔案就會被視為空白。 結果會以布林值的形式傳入使用者變數中，而這個變數的值可用於在封裝的控制流程中分支。 **FireInformation** 方法也會在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA) 的 [輸出] 視窗中顯示結果。  
  
#### <a name="to-configure-this-script-task-example"></a>設定此指令碼工作範例  
  
1.  建立並設定名為 **EmptyFlatFileTest** 的一般檔案連線管理員。  
  
2.  建立名為 `FFNonDataRows` 的整數變數並將其值設定為一般檔案中預期的非資料列數目。  
  
3.  建立名為 `FFIsEmpty` 的布林值變數。  
  
4.  將 `FFNonDataRows` 變數新增至指令碼工作的 **ReadOnlyVariables** 屬性。  
  
5.  將 `FFIsEmpty` 變數新增至指令碼工作的 **ReadWriteVariables** 屬性。  
  
6.  在您的程式碼中，匯入 **System.IO** 命名空間。  
  
 如果您要使用 Foreach 檔案列舉值 (而非使用單一一般檔案連接管理員) 來逐一查看檔案，就必須修改下列範例程式碼，以便從儲存列舉值的變數 (而非從連接管理員) 中取得檔案名稱和路徑。  
  
### <a name="code"></a>程式碼  
  
```vb  
Public Sub Main()  
  
  Dim nonDataRows As Integer = _  
      DirectCast(Dts.Variables("FFNonDataRows").Value, Integer)  
  Dim ffConnection As String = _  
      DirectCast(Dts.Connections("EmptyFlatFileTest").AcquireConnection(Nothing), _  
      String)  
  Dim flatFileInfo As New FileInfo(ffConnection)  
  ' If file size is 0 bytes, flat file does not contain data.  
  Dim fileSize As Long = flatFileInfo.Length  
  If fileSize > 0 Then  
    Dim lineCount As Integer = 0  
    Dim line As String  
    Dim fsFlatFile As New StreamReader(ffConnection)  
    Do Until fsFlatFile.EndOfStream  
      line = fsFlatFile.ReadLine  
      lineCount += 1  
      ' If line count > expected number of non-data rows,  
      '  flat file contains data (default value).  
      If lineCount > nonDataRows Then  
        Exit Do  
      End If  
      ' If line count <= expected number of non-data rows,  
      '  flat file does not contain data.  
      If lineCount <= nonDataRows Then  
        Dts.Variables("FFIsEmpty").Value = True  
      End If  
    Loop  
  Else  
    Dts.Variables("FFIsEmpty").Value = True  
  End If  
  
  Dim fireAgain As Boolean = False  
  Dts.Events.FireInformation(0, "Script Task", _  
      String.Format("{0}: {1}", ffConnection, _  
      Dts.Variables("FFIsEmpty").Value.ToString), _  
      String.Empty, 0, fireAgain)  
  
  Dts.TaskResult = ScriptResults.Success  
  
End Sub  
```  
  
```csharp  
public void Main()  
        {  
  
            int nonDataRows = (int)(Dts.Variables["FFNonDataRows"].Value);  
            string ffConnection = (string)(Dts.Connections["EmptyFlatFileTest"].AcquireConnection(null) as String);  
            FileInfo flatFileInfo = new FileInfo(ffConnection);  
            // If file size is 0 bytes, flat file does not contain data.  
            long fileSize = flatFileInfo.Length;  
            if (fileSize > 0)  
            {  
  
                int lineCount = 0;  
                string line;  
                StreamReader fsFlatFile = new StreamReader(ffConnection);  
                while (!(fsFlatFile.EndOfStream))  
                {  
                    Console.WriteLine (fsFlatFile.ReadLine());  
                    lineCount += 1;  
                    // If line count > expected number of non-data rows,  
                    //  flat file contains data (default value).  
                    if (lineCount > nonDataRows)  
                    {  
                        break;  
                    }  
                    // If line count <= expected number of non-data rows,  
                    //  flat file does not contain data.  
                    if (lineCount <= nonDataRows)  
                    {  
                        Dts.Variables["FFIsEmpty"].Value = true;  
                    }  
                }  
            }  
            else  
            {  
                Dts.Variables["FFIsEmpty"].Value = true;  
            }  
  
            bool fireAgain = false;  
            Dts.Events.FireInformation(0, "Script Task", String.Format("{0}: {1}", ffConnection, Dts.Variables["FFIsEmpty"].Value), String.Empty, 0, ref fireAgain);  
  
            Dts.TaskResult = (int)ScriptResults.Success;  
  
        }  
```  
  
## <a name="see-also"></a>另請參閱  
 [指令碼工作範例](../../integration-services/extending-packages-scripting-task-examples/script-task-examples.md)  
  
  
