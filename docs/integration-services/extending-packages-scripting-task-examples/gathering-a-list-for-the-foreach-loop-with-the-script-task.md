---
title: "收集指令碼工作使用 「 ForEach 迴圈 」 清單 |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Foreach Loop containers
- Script task [Integration Services], Foreach loops
- Script task [Integration Services], examples
- SSIS Script task, Foreach loops
ms.assetid: 694f0462-d0c5-4191-b64e-821b1bdef055
caps.latest.revision: 34
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: b1bd133c2fdc8c500db9c07df9c54e954db327bf
ms.contentlocale: zh-tw
ms.lasthandoff: 09/26/2017

---
# <a name="gathering-a-list-for-the-foreach-loop-with-the-script-task"></a>以指令碼工作蒐集 ForEach 迴圈的清單
  Foreach from Variable 列舉值會透過以變數傳遞給它的清單中之項目來列舉，並針對每個項目執行相同的工作。 您可以在指令碼工作中使用自訂程式碼，針對此目的填入清單。 如需列舉值的詳細資訊，請參閱[Foreach 迴圈 」 容器](../../integration-services/control-flow/foreach-loop-container.md)。  
  
> [!NOTE]  
>  如果您想要建立可更輕鬆地在多個封裝之間重複使用的工作，請考慮使用此指令碼工作範例中的程式碼做為自訂工作的起點。 如需詳細資訊，請參閱 [開發自訂工作](../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md)。  
  
## <a name="description"></a>Description  
 下列範例會使用從方法**System.IO**還要新或是使用者在變數中指定的天數比舊的電腦上的 Excel 活頁簿清單蒐集的命名空間。 它會在磁碟 C 上以遞迴方式搜尋目錄中有 .xls 副檔名的檔案，並檢查檔案最後修改的日期，以判斷檔案是否應歸屬於清單中。 它會新增符合的檔案加入**ArrayList** ，並將儲存**ArrayList**供稍後使用 「 Foreach 迴圈 」 容器中的變數。 Foreach Loop 容器是設定為從 Variable 列舉值使用 Foreach。  
  
> [!NOTE]  
>  您可以使用 Foreach from Variable 列舉值的變數必須屬於型別**物件**。 您放置在變數中的物件必須實作下列介面的其中一個： **System.Collections.IEnumerable**， **System.Runtime.InteropServices.ComTypes.IEnumVARIANT**， **System.ComponentModel IListSource**，或**Microsoft.SqlServer.Dts.Runtime.Wrapper.ForEachEnumeratorHost**。 **陣列**或**ArrayList**常用。 **ArrayList**需要參考和**匯入**陳述式**System.Collections**命名空間。  
  
 您可以透過為 `FileAge` 封裝變數使用不同的正值與負值，來試驗這項工作。 例如，您可以輸入 5 以搜尋在過去五天內建立的檔案，或是輸入 3 搜尋已建立超過三天的檔案。 這項工作可能需要花費一兩分鐘，以搜尋磁碟機上的許多資料夾。  
  
#### <a name="to-configure-this-script-task-example"></a>設定此指令碼工作範例  
  
1.  建立名為 `FileAge` 且類型為整數的封裝孌數，並輸入正整數值或負整數值。 當值為正數時，程式碼會搜尋比指定天數還要新的檔案，當值為負數時，會搜尋比指定的天數還要舊的檔案。  
  
2.  建立名為的封裝變數`FileList`型別的**物件**接收蒐集指令碼工作，供稍後使用 Foreach from Variable 列舉值的檔案清單。  
  
3.  新增`FileAge`變數加入指令碼工作的**[readonlyvariables]**屬性，並加入`FileList`變數設為**[readwritevariables]**屬性。  
  
4.  在您的程式碼中，匯入**System.Collections**和**System.IO**命名空間。  
  
### <a name="code"></a>程式碼  
  
```vb  
Imports System  
Imports System.Data  
Imports System.Math  
Imports Microsoft.SqlServer.Dts.Runtime  
Imports System.Collections  
Imports System.IO  
  
Public Class ScriptMain  
  
  Private Const FILE_AGE As Integer = -50  
  
  Private Const FILE_ROOT As String = "C:\"  
  Private Const FILE_FILTER As String = "*.xls"  
  
  Private isCheckForNewer As Boolean = True  
  Dim fileAgeLimit As Integer  
  Private listForEnumerator As ArrayList  
  
  Public Sub Main()  
  
    fileAgeLimit = DirectCast(Dts.Variables("FileAge").Value, Integer)  
  
    ' If value provided is positive, we want files NEWER THAN n days.  
    '  If negative, we want files OLDER THAN n days.  
    If fileAgeLimit < 0 Then  
      isCheckForNewer = False  
    End If  
    ' Extract number of days as positive integer.  
    fileAgeLimit = Math.Abs(fileAgeLimit)  
  
    listForEnumerator = New ArrayList  
  
    GetFilesInFolder(FILE_ROOT)  
  
    ' Return the list of files to the variable  
    '  for later use by the Foreach from Variable enumerator.  
    System.Windows.Forms.MessageBox.Show("Matching files: " & listForEnumerator.Count.ToString, "Results", Windows.Forms.MessageBoxButtons.OK, Windows.Forms.MessageBoxIcon.Information)  
    Dts.Variables("FileList").Value = listForEnumerator  
  
    Dts.TaskResult = ScriptResults.Success  
  
  End Sub  
  
  Private Sub GetFilesInFolder(ByVal folderPath As String)  
  
    Dim localFiles() As String  
    Dim localFile As String  
    Dim fileChangeDate As Date  
    Dim fileAge As TimeSpan  
    Dim fileAgeInDays As Integer  
    Dim childFolder As String  
  
    Try  
      localFiles = Directory.GetFiles(folderPath, FILE_FILTER)  
      For Each localFile In localFiles  
        fileChangeDate = File.GetLastWriteTime(localFile)  
        fileAge = DateTime.Now.Subtract(fileChangeDate)  
        fileAgeInDays = fileAge.Days  
        CheckAgeOfFile(localFile, fileAgeInDays)  
      Next  
  
      If Directory.GetDirectories(folderPath).Length > 0 Then  
        For Each childFolder In Directory.GetDirectories(folderPath)  
          GetFilesInFolder(childFolder)  
        Next  
      End If  
  
    Catch  
      ' Ignore exceptions on special folders such as System Volume Information.  
    End Try  
  
  End Sub  
  
  Private Sub CheckAgeOfFile(ByVal localFile As String, ByVal fileAgeInDays As Integer)  
  
    If isCheckForNewer Then  
      If fileAgeInDays <= fileAgeLimit Then  
        listForEnumerator.Add(localFile)  
      End If  
    Else  
      If fileAgeInDays > fileAgeLimit Then  
        listForEnumerator.Add(localFile)  
      End If  
    End If  
  
  End Sub  
  
End Class  
```  
  
```csharp  
using System;  
using System.Data;  
using System.Math;  
using Microsoft.SqlServer.Dts.Runtime;  
using System.Collections;  
using System.IO;  
  
public partial class ScriptMain : Microsoft.SqlServer.Dts.Tasks.ScriptTask.VSTARTScriptObjectModelBase  
    {  
  
        private const int FILE_AGE = -50;  
  
        private const string FILE_ROOT = "C:\\";  
        private const string FILE_FILTER = "*.xls";  
  
        private bool isCheckForNewer = true;  
        int fileAgeLimit;  
        private ArrayList listForEnumerator;  
  
        public void Main()  
  {  
  
    fileAgeLimit = (int)(Dts.Variables["FileAge"].Value);  
  
    // If value provided is positive, we want files NEWER THAN n days.  
    // If negative, we want files OLDER THAN n days.  
    if (fileAgeLimit<0)  
    {  
      isCheckForNewer = false;  
    }  
    // Extract number of days as positive integer.  
    fileAgeLimit = Math.Abs(fileAgeLimit);  
  
    ArrayList listForEnumerator = new ArrayList();  
  
    GetFilesInFolder(FILE_ROOT);  
  
    // Return the list of files to the variable  
    // for later use by the Foreach from Variable enumerator.  
    System.Windows.Forms.MessageBox.Show("Matching files: "+ listForEnumerator.Count, "Results",   
MessageBoxButtons.OK, MessageBoxIcon.Information);  
    Dts.Variables["FileList"].Value = listForEnumerator;  
  
    Dts.TaskResult = (int)ScriptResults.Success;  
  
  }  
  
        private void GetFilesInFolder(string folderPath)  
        {  
  
            string[] localFiles;  
            DateTime fileChangeDate;  
            TimeSpan fileAge;  
            int fileAgeInDays;  
  
            try  
            {  
                localFiles = Directory.GetFiles(folderPath, FILE_FILTER);  
                foreach (string localFile in localFiles)  
                {  
                    fileChangeDate = File.GetLastWriteTime(localFile);  
                    fileAge = DateTime.Now.Subtract(fileChangeDate);  
                    fileAgeInDays = fileAge.Days;  
                    CheckAgeOfFile(localFile, fileAgeInDays);  
                }  
  
                if (Directory.GetDirectories(folderPath).Length > 0)  
                {  
                    foreach (string childFolder in Directory.GetDirectories(folderPath))  
                    {  
                        GetFilesInFolder(childFolder);  
                    }  
                }  
  
            }  
            catch  
            {  
                // Ignore exceptions on special folders, such as System Volume Information.  
            }  
  
        }  
  
        private void CheckAgeOfFile(string localFile, int fileAgeInDays)  
        {  
  
            if (isCheckForNewer)  
            {  
                if (fileAgeInDays <= fileAgeLimit)  
                {  
                    listForEnumerator.Add(localFile);  
                }  
            }  
            else  
            {  
                if (fileAgeInDays > fileAgeLimit)  
                {  
                    listForEnumerator.Add(localFile);  
                }  
            }  
  
        }  
  
    }  
```  
  
## <a name="see-also"></a>另請參閱  
 [Foreach 迴圈容器](../../integration-services/control-flow/foreach-loop-container.md)   
 [設定 Foreach 迴圈容器](http://msdn.microsoft.com/library/519c6f96-5e1f-47d2-b96a-d49946948c25)  
  
  

