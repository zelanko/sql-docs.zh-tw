---
title: 從 ADO MD 移轉至 ADOMD.NET |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: adomd
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e6d0e3acb77657bcac754b9e6b9392dc2971ce9c
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="migrating-from-ado-md-to-adomdnet"></a>從 ADO MD 移轉至 ADOMD.NET
  ADOMD.NET 程式庫類似於 ActiveX Data Objects Multidimensional (ADO MD) 程式庫，這個 ActiveX Data Objects (ADO) 程式庫的延伸模組是用來存取以元件物件模型 (COM) 為基礎的用戶端應用程式中的多維度資料。 ADO MD 可輕鬆地從 Unmanaged 語言 (例如 C++ 與 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic) 存取多維度資料。 ADOMD.NET 可輕鬆地從 Managed 語言 (例如 [!INCLUDE[msCoName](../../includes/msconame-md.md)] C# 與 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic .NET) 存取分析資料 (多維度與資料採礦)。 此外，ADOMD.NET 提供增強型中繼資料物件模型。  
  
 將現有用戶端應用程式從 ADO MD 移轉到 ADOMD.NET 很容易，但是有幾項關於移轉的差異：  
  
 **提供用戶端應用程式的連接和資料存取**  
 |ADO MD|ADOMD.NET|  
|------------|---------------|  
|需要參考 Adodb.dll 和 Adomd.dll。|需要單一的 Microsoft.AnalysisServices.AdomdClient.dll 參考。|  
  
 除了中繼資料的存取之外，<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 類別還提供連接性支援。  
  
 **若要擷取多維度物件的中繼資料**  
 |ADO MD|ADOMD.NET|  
|------------|---------------|  
|使用類別目錄類別。|使用 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.Cubes%2A> 的 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 屬性。|  
  
 **執行查詢並傳回資料格集物件**  
 |ADO MD|ADOMD.NET|  
|------------|---------------|  
|使用資料格集類別。|使用 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand> 類別。|  
  
 **若要存取用來顯示資料格集的中繼資料**  
 |ADO MD|ADOMD.NET|  
|------------|---------------|  
|使用位置的類別。|使用 <xref:Microsoft.AnalysisServices.AdomdClient.Set> 和 <xref:Microsoft.AnalysisServices.AdomdClient.Tuple> 物件。|  
  
> [!NOTE]  
>  支援 <xref:Microsoft.AnalysisServices.AdomdClient.Position> 類別是為了與舊版相容。  
  
 **若要擷取採礦模型中繼資料**  
 在 ADO MD 中有任何類別。 在 ADO.NET 中使用資料採礦集合之一：  
  
-   <xref:Microsoft.AnalysisServices.AdomdClient.MiningModelCollection> 包含資料來源中所有採礦模型的清單。  
  
-   <xref:Microsoft.AnalysisServices.AdomdClient.MiningServiceCollection> 會提供可用之採礦演算法的相關資訊。  
  
-   <xref:Microsoft.AnalysisServices.AdomdClient.MiningStructureCollection> 會公開伺服器上採礦結構的相關資訊。  
  
 下列移轉範例比較現有 ADO MD 應用程式與對等 ADOMD.NET 應用程式，以強調這些差異。  
  
## <a name="looking-at-a-migration-example"></a>查看移轉範例  
 在本章節中所顯示的現有 ADO MD 與對等的 ADOMD.NET 程式碼範例，會執行相同的動作：建立連接、執行多維度運算式 (MDX) 陳述式以及擷取中繼資料與資料。 不過，這兩組程式碼不會使用相同的物件來執行這些工作。  
  
### <a name="existing-ado-md-code"></a>現有的 ADO MD 程式碼  
 下列程式碼範例，取自 ADO MD 2.8 說明文件，以撰寫[!INCLUDE[msCoName](../../includes/msconame-md.md)]Visual Basic® 6.0 並使用 ADO MD 來示範如何連接及查詢[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料來源。 這個 ADO MD 範例使用下列物件：  
  
-   建立連接，以從**目錄**物件。  
  
-   執行多維度運算式 (MDX) 陳述式使用**資料格集**物件。  
  
-   擷取中繼資料和資料從**位置**物件，擷取自**資料格集**物件。  
  
```  
Private Sub cmdCellSettoDebugWindow_Click()  
Dim cat As New ADOMD.Catalog  
Dim cst As New ADOMD.Cellset  
Dim i As Integer  
Dim j As Integer  
Dim k As Integer  
Dim strServer As String  
Dim strSource As String  
Dim strColumnHeader As String  
Dim strRowText As String  
  
On Error GoTo Error_cmdCellSettoDebugWindow_Click  
Screen.MousePointer = vbHourglass  
'*-----------------------------------------------------------------------  
'* Set server to local host.  
'*-----------------------------------------------------------------------  
    strServer = "LOCALHOST"  
  
'*-----------------------------------------------------------------------  
'* Set MDX query string source.  
'*-----------------------------------------------------------------------  
    strSource = strSource & "SELECT "  
    strSource = strSource & "{[Measures].members} ON COLUMNS,"  
    strSource = strSource & _  
        "NON EMPTY [Store].[Store City].members ON ROWS"  
    strSource = strSource & " FROM Sales"  
  
'*-----------------------------------------------------------------------  
'* Set active connection.  
'*-----------------------------------------------------------------------  
        cat.ActiveConnection = "Data Source=" & strServer & _  
            ";Provider=msolap;"  
  
'*-----------------------------------------------------------------------  
'* Set cellset source to MDX query string.  
'*-----------------------------------------------------------------------  
        cst.Source = strSource  
  
'*-----------------------------------------------------------------------  
'* Set cellset active connection to current connection  
'*-----------------------------------------------------------------------  
    Set cst.ActiveConnection = cat.ActiveConnection  
  
'*-----------------------------------------------------------------------  
'* Open cellset.  
'*-----------------------------------------------------------------------  
    cst.Open  
  
'*-----------------------------------------------------------------------  
'* Allow space for row header text.  
'*-----------------------------------------------------------------------  
strColumnHeader = vbTab & vbTab & vbTab & vbTab & vbTab & vbTab  
  
'*-----------------------------------------------------------------------  
'* Loop through column headers.  
'*-----------------------------------------------------------------------  
       For i = 0 To cst.Axes(0).Positions.Count - 1  
            strColumnHeader = strColumnHeader & _  
                cst.Axes(0).Positions(i).Members(0).Caption & vbTab & _  
                    vbTab & vbTab & vbTab  
       Next  
       Debug.Print vbTab & strColumnHeader & vbCrLf  
  
'*-----------------------------------------------------------------------  
'* Loop through row headers and provide data for each row.  
'*-----------------------------------------------------------------------  
        strRowText = ""  
        For j = 0 To cst.Axes(1).Positions.Count - 1  
            strRowText = strRowText & _  
                cst.Axes(1).Positions(j).Members(0).Caption & vbTab & _  
                    vbTab & vbTab & vbTab  
            For k = 0 To cst.Axes(0).Positions.Count - 1  
                strRowText = strRowText & cst(k, j).FormattedValue & _  
                    vbTab & vbTab & vbTab & vbTab  
            Next  
            Debug.Print strRowText & vbCrLf  
            strRowText = ""  
        Next  
  
    Screen.MousePointer = vbDefault  
Exit Sub  
  
Error_cmdCellSettoDebugWindow_Click:  
   Beep  
   Screen.MousePointer = vbDefault  
   MsgBox "The following error has occurred:" & vbCrLf & _  
      Err.Description, vbCritical, " Error!"  
   Exit Sub  
End Sub  
```  
  
### <a name="equivalent-adomdnet-code"></a>對等的 ADOMD.NET 程式碼  
 下列以 Visual Basic .NET 撰寫且使用 ADOMD.NET 的範例，示範如何執行與前面 Visual Basic 6.0 範例相同的動作。 下列範例與前面所顯示的 ADO MD 範例之間主要的差異，在於用以執行這些動作的物件。 ADOMD.NET 範例使用下列物件：  
  
-   建立與連線**AdomdConnection**物件。  
  
-   執行 MDX 陳述式使用**AdomdCommand**物件。  
  
-   擷取中繼資料和資料從**設定**物件，擷取自**資料格集**物件。  
  
```  
Private Sub DisplayCellSetInOutputWindow()  
    Dim conn As AdomdConnection  
    Dim cmd As AdomdCommand  
    Dim cst As CellSet  
    Dim i As Integer  
    Dim j As Integer  
    Dim k As Integer  
    Dim strServer As String = "LOCALHOST"  
    Dim strSource As String = "SELECT [Measures].members ON COLUMNS, " & _  
        "NON EMPTY [Store].[Store City].members ON ROWS FROM SALES"  
    Dim strOutput As New System.IO.StringWriter  
  
    '*-----------------------------------------------------------------------  
    '* Open connection.  
    '*-----------------------------------------------------------------------  
    Try  
        ' Create a new AdomdConnection object, providing the connection  
        ' string.  
        conn = New AdomdConnection("Data Source=" & strServer & _  
        ";Provider=msolap;")  
        ' Open the connection.  
        conn.Open()  
    Catch ex As Exception  
        Throw New ApplicationException( _  
            "An error occurred while connecting.")  
    End Try  
  
    Try  
    '*-----------------------------------------------------------------------  
    '* Open cellset.  
    '*-----------------------------------------------------------------------  
        ' Create a new AdomdCommand object, providing the MDX query string.  
        cmd = New AdomdCommand(strSource, conn)  
        ' Run the command and return a CellSet object.  
        cst = cmd.ExecuteCellSet()  
  
    '*-----------------------------------------------------------------------  
    '* Concatenate output.  
    '*-----------------------------------------------------------------------  
  
    ' Include spacing to account for row headers.  
    strOutput.Write(vbTab, 6)  
  
    ' Iterate through the first axis of the CellSet object and  
    ' retrieve column headers.  
    For i = 0 To cst.Axes(0).Set.Tuples.Count - 1  
        strOutput.Write(cst.Axes(0).Set.Tuples(i).Members(0).Caption)  
        strOutput.Write(vbTab, 4)  
    Next  
    strOutput.WriteLine()  
  
    ' Iterate through the second axis of the CellSet object and  
    ' retrieve row headers and cell data.  
    For j = 0 To cst.Axes(1).Set.Tuples.Count - 1  
        ' Append the row header.  
        strOutput.Write(cst.Axes(1).Set.Tuples(j).Members(0).Caption)  
        strOutput.Write(vbTab, 4)  
  
        ' Append the cell data for that row.  
        For k = 0 To cst.Axes(0).Set.Tuples.Count - 1  
            strOutput.Write(cst.Cells(k, j).FormattedValue)  
            strOutput.Write(vbTab, 4)  
        Next  
        strOutput.WriteLine()  
    Next  
  
    ' Display the output.  
    Debug.WriteLine(strOutput.ToString)  
  
    '*-----------------------------------------------------------------------  
    '* Release resources.  
    '*-----------------------------------------------------------------------  
        conn.Close()  
    Catch ex As Exception  
        ' Ignore or handle errors.  
    Finally  
        cst = Nothing  
        cmd = Nothing  
        conn = Nothing  
    End Try  
End Sub  
```  
  
  
