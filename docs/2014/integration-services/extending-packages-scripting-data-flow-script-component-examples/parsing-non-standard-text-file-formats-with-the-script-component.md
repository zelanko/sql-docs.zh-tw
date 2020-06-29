---
title: 使用指令碼元件剖析非標準文字檔案格式 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- text file reading [Integration Services]
- Script component [Integration Services], non-standard text file formats
- transformations [Integration Services], components
- Script component [Integration Services], examples
ms.assetid: 1fda034d-09e4-4647-9a9f-e8d508c2cc8f
author: chugugrace
ms.author: chugu
ms.openlocfilehash: fc8ac157a3bdfa240414fe4055cc322370bac019
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/26/2020
ms.locfileid: "85427085"
---
# <a name="parsing-non-standard-text-file-formats-with-the-script-component"></a>使用指令碼元件剖析非標準文字檔案格式
  當來源資料是以非標準格式排列時，為了達成相同的結果，您可能會發現將所有剖析邏輯合併在單一指令碼中會比將多個 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 轉換鏈結在一起更方便。  
  
 [範例 1：剖析以資料列分隔的記錄](#example1)  
  
 [範例 2：分割父記錄和子記錄](#example2)  
  
> [!NOTE]  
>  如果您要建立可以更輕鬆地在多個資料流程工作與多個封裝之間重複使用的元件，請考慮使用這個指令碼元件範例中的程式碼，做為自訂資料流程元件的起點。 如需詳細資訊，請參閱 [開發自訂資料流程元件](../extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)。  
  
##  <a name="example-1-parsing-row-delimited-records"></a><a name="example1"></a> 範例 1：剖析以資料列分隔的記錄  
 這則範例將示範如何取得每個資料行都以個別行顯示的文字檔案，並且使用指令碼元件，將它剖析成目的地資料表。  
  
 如需如何設定腳本元件做為資料流程中的轉換的詳細資訊，請參閱[使用腳本元件建立同步轉換](../extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)和[使用腳本元件建立異步轉換](../extending-packages-scripting-data-flow-script-component-types/creating-an-asynchronous-transformation-with-the-script-component.md)。  
  
#### <a name="to-configure-this-script-component-example"></a>設定此指令碼元件範例  
  
1.  建立並儲存名為 **rowdelimiteddata.txt** 的文字檔案，其中包含下列來源資料：  
  
    ```  
    FirstName: Nancy  
    LastName: Davolio  
    Title: Sales Representative  
    City: Seattle  
    StateProvince: WA  
  
    FirstName: Andrew  
    LastName: Fuller  
    Title: Vice President, Sales  
    City: Tacoma  
    StateProvince: WA  
  
    FirstName: Steven  
    LastName: Buchanan  
    Title: Sales Manager  
    City: London  
    StateProvince:  
  
    ```  
  
2.  開啟 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 並連接至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的執行個體。  
  
3.  選取目的地資料庫，並且開啟新的查詢視窗。 在查詢視窗中，執行下列指令碼來建立目的地資料表：  
  
    ```  
    create table RowDelimitedData  
    (  
    FirstName varchar(32),  
    LastName varchar(32),  
    Title varchar(32),  
    City varchar(32),  
    StateProvince varchar(32)  
    )  
  
    ```  
  
4.  開啟 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 並建立名為 ParseRowDelim.dtsx 的新 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝。  
  
5.  將一般檔案連接管理員加入至此封裝、將它命名為 RowDelimitedData，並且將它設定為連接至您在先前步驟中建立的 rowdelimiteddata.txt 檔案。  
  
6.  將 OLE DB 連接管理員加入至此封裝，並且將它設定為連接至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體以及您在其中建立目的地資料表的資料庫。  
  
7.  將資料流程工作新增至套件，然後按一下 SSIS 設計工具的 [資料流程]  索引標籤。  
  
8.  將一般檔案來源加入至資料流程，並且將它設定為使用 RowDelimitedData 連接管理員。 在 [一般檔案來源編輯器] 的 [資料行] 頁面上，選取單一可用的外部資料行。  
  
9. 將指令碼元件加入至資料流程並將它設定為轉換。 將一般檔案來源的輸出連接至指令碼元件。  
  
10. 按兩下指令碼元件，以顯示 [指令碼轉換編輯器]  。  
  
11. 在 [指令碼轉換編輯器] 的 [輸入資料行] 頁面上，選取單一可用的輸入資料行。  
  
12. 在 [**腳本轉換編輯器**] 的 [**輸入和輸出**] 頁面上，選取 [輸出 0]，並將其設定 `SynchronousInputID` 為 [無]。 建立 5 個輸出資料行，全部都屬於字串 [DT_STR] 類型而且長度為 32：  
  
    -   名字  
  
    -   姓氏  
  
    -   Title  
  
    -   City  
  
    -   StateProvince  
  
13. 在 [**腳本轉換編輯器**] 的 [**腳本**] 頁面上，按一下 [**編輯腳本**]，然後輸入範例的類別中所顯示的程式碼 `ScriptMain` 。 關閉指令碼開發環境以及 [指令碼轉換編輯器]  。  
  
14. 將 SQL Server 目的地加入至資料流程。 將它設定為使用 OLE DB 連接管理員和 RowDelimitedData 資料表。 將指令碼元件的輸出連接至這個目的地。  
  
15. 執行封裝。 封裝完成之後，檢查 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目的地資料表中的記錄。  
  
```vb  
Public Overrides Sub Input0_ProcessInputRow(ByVal Row As Input0Buffer)  
  
    Dim columnName As String  
    Dim columnValue As String  
  
    ' Check for an empty row.  
    If Row.Column0.Trim.Length > 0 Then  
        columnName = Row.Column0.Substring(0, Row.Column0.IndexOf(":"))  
        ' Check for an empty value after the colon.  
        If Row.Column0.Substring(Row.Column0.IndexOf(":")).TrimEnd.Length > 1 Then  
            ' Extract the column value from after the colon and space.  
            columnValue = Row.Column0.Substring(Row.Column0.IndexOf(":") + 2)  
            Select Case columnName  
                Case "FirstName"  
                    ' The FirstName value indicates a new record.  
                    Me.Output0Buffer.AddRow()  
                    Me.Output0Buffer.FirstName = columnValue  
                Case "LastName"  
                    Me.Output0Buffer.LastName = columnValue  
                Case "Title"  
                    Me.Output0Buffer.Title = columnValue  
                Case "City"  
                    Me.Output0Buffer.City = columnValue  
                Case "StateProvince"  
                    Me.Output0Buffer.StateProvince = columnValue  
            End Select  
        End If  
    End If  
  
End Sub  
```  
  
```csharp  
public override void Input0_ProcessInputRow(Input0Buffer Row)  
    {  
  
        string columnName;  
        string columnValue;  
  
        // Check for an empty row.  
        if (Row.Column0.Trim().Length > 0)  
        {  
            columnName = Row.Column0.Substring(0, Row.Column0.IndexOf(":"));  
            // Check for an empty value after the colon.  
            if (Row.Column0.Substring(Row.Column0.IndexOf(":")).TrimEnd().Length > 1)  
            // Extract the column value from after the colon and space.  
            {  
                columnValue = Row.Column0.Substring(Row.Column0.IndexOf(":") + 2);  
                switch (columnName)  
                {  
                    case "FirstName":  
                        // The FirstName value indicates a new record.  
                        this.Output0Buffer.AddRow();  
                        this.Output0Buffer.FirstName = columnValue;  
                        break;  
                    case "LastName":  
                        this.Output0Buffer.LastName = columnValue;  
                        break;  
                    case "Title":  
                        this.Output0Buffer.Title = columnValue;  
                        break;  
                    case "City":  
                        this.Output0Buffer.City = columnValue;  
                        break;  
                    case "StateProvince":  
                        this.Output0Buffer.StateProvince = columnValue;  
                        break;  
                }  
            }  
        }  
  
    }  
```  
  
##  <a name="example-2-splitting-parent-and-child-records"></a><a name="example2"></a> 範例 2：分割父記錄和子記錄  
 這則範例將示範如何取得文字檔案 (分隔符號資料列位於父記錄資料列前面，而且後面接著不定數目的子記錄資料列)，並且使用指令碼元件，將它剖析成適當正規化的父和子目的地資料表。 您可以針對每筆父記錄和子記錄使用多個資料列或資料行的來源檔案輕鬆地調整這則簡單範例，只要存在可識別每筆記錄之開頭和結尾的方式即可。  
  
> [!CAUTION]  
>  這則範例僅供示範使用。 如果您執行此範例多次，它就會將重複的索引鍵值插入目的地資料表中。  
  
 如需如何設定腳本元件做為資料流程中的轉換的詳細資訊，請參閱[使用腳本元件建立同步轉換](../extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)和[使用腳本元件建立異步轉換](../extending-packages-scripting-data-flow-script-component-types/creating-an-asynchronous-transformation-with-the-script-component.md)。  
  
#### <a name="to-configure-this-script-component-example"></a>設定此指令碼元件範例  
  
1.  建立並儲存名為 **parentchilddata.txt** 的文字檔案，其中包含下列來源資料：  
  
    ```  
    **********  
    PARENT 1 DATA  
    child 1 data  
    child 2 data  
    child 3 data  
    child 4 data  
    **********  
    PARENT 2 DATA  
    child 5 data  
    child 6 data  
    child 7 data  
    child 8 data  
    **********  
  
    ```  
  
2.  開啟 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 並連接至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的執行個體。  
  
3.  選取目的地資料庫，並且開啟新的查詢視窗。 在查詢視窗中，執行下列指令碼來建立目的地資料表：  
  
    ```  
    CREATE TABLE [dbo].[Parents]([ParentID] [int] NOT NULL,  
    [ParentRecord] [varchar](32) NOT NULL,  
     CONSTRAINT [PK_Parents] PRIMARY KEY CLUSTERED   
    ([ParentID] ASC))  
    GO  
    CREATE TABLE [dbo].[Children]([ChildID] [int] NOT NULL,  
    [ParentID] [int] NOT NULL,  
    [ChildRecord] [varchar](32) NOT NULL,  
     CONSTRAINT [PK_Children] PRIMARY KEY CLUSTERED   
    ([ChildID] ASC))  
    GO  
    ALTER TABLE [dbo].[Children] ADD CONSTRAINT [FK_Children_Parents] FOREIGN KEY([ParentID])  
    REFERENCES [dbo].[Parents] ([ParentID])  
  
    ```  
  
4.  開啟 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 並建立名為 SplitParentChild.dtsx 的新 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝。  
  
5.  將一般檔案連接管理員加入至此封裝、將它命名為 ParentChildData，並且將它設定為連接至您在先前步驟中建立的 parentchilddata.txt 檔案。  
  
6.  將 OLE DB 連接管理員加入至此封裝，並且將它設定為連接至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體以及您在其中建立目的地資料表的資料庫。  
  
7.  將資料流程工作新增至套件，然後按一下 SSIS 設計工具的 [資料流程]  索引標籤。  
  
8.  將一般檔案來源加入至資料流程，並且將它設定為使用 ParentChildData 連接管理員。 在 [一般檔案來源編輯器] 的 [資料行] 頁面上，選取單一可用的外部資料行。  
  
9. 將指令碼元件加入至資料流程並將它設定為轉換。 將一般檔案來源的輸出連接至指令碼元件。  
  
10. 按兩下指令碼元件，以顯示 [指令碼轉換編輯器]  。  
  
11. 在 [指令碼轉換編輯器] 的 [輸入資料行] 頁面上，選取單一可用的輸入資料行。  
  
12. 在 [**腳本轉換編輯器**] 的 [**輸入和輸出**] 頁面上，選取 [輸出 0]，將它重新命名為 ParentRecords，並將其設定 `SynchronousInputID` 為 [無]。 建立 2 個輸出資料行：  
  
    -   ParentID (主索引鍵)，屬於四位元組帶正負號的整數 [DT_I4] 類型  
  
    -   ParentRecord，屬於字串 [DT_STR] 類型而且長度為 32  
  
13. 建立第二個輸出並將它命名為 ChildRecords。 新輸出的 `SynchronousInputID` 已經設定為 None。 建立 3 個輸出資料行：  
  
    -   ChildID (主索引鍵)，屬於四位元組帶正負號的整數 [DT_I4] 類型  
  
    -   ParentID (外部索引鍵)，也屬於四位元組帶正負號的整數 [DT_I4] 類型  
  
    -   ChildRecord，屬於字串 [DT_STR] 類型而且長度為 50  
  
14. 在 [指令碼轉換編輯器] 的 [指令碼] 頁面上，按一下 [編輯指令碼]。 在 `ScriptMain` 類別中，輸入此範例中所示的程式碼。 關閉指令碼開發環境以及 [指令碼轉換編輯器]  。  
  
15. 將 SQL Server 目的地加入至資料流程。 將指令碼元件的 ParentRecords 輸出連接至這個目的地。將它設定為使用 OLE DB 連接管理員和 Parents 資料表。  
  
16. 將另一個 SQL Server 目的地加入至資料流程。 將指令碼元件的 ChildRecords 輸出連接至這個目的地。 將它設定為使用 OLE DB 連接管理員和 Children 資料表。  
  
17. 執行封裝。 封裝完成之後，檢查兩個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目的地資料表中的父記錄和子記錄。  
  
```vb  
Public Overrides Sub Input0_ProcessInputRow(ByVal Row As Input0Buffer)  
  
    Static nextRowIsParent As Boolean = False  
    Static parentCounter As Integer = 0  
    Static childCounter As Integer = 0  
  
    ' If current row starts with separator characters,  
    '  then following row contains new parent record.  
    If Row.Column0.StartsWith("***") Then  
        nextRowIsParent = True  
    Else  
        If nextRowIsParent Then  
            ' Current row contains parent record.  
            parentCounter += 1  
            Me.ParentRecordsBuffer.AddRow()  
            Me.ParentRecordsBuffer.ParentID = parentCounter  
            Me.ParentRecordsBuffer.ParentRecord = Row.Column0  
            nextRowIsParent = False  
        Else  
            ' Current row contains child record.  
            childCounter += 1  
            Me.ChildRecordsBuffer.AddRow()  
            Me.ChildRecordsBuffer.ChildID = childCounter  
            Me.ChildRecordsBuffer.ParentID = parentCounter  
            Me.ChildRecordsBuffer.ChildRecord = Row.Column0  
        End If  
    End If  
  
End Sub  
```  
  
```csharp  
public override void Input0_ProcessInputRow(Input0Buffer Row)  
    {  
  
    int static_Input0_ProcessInputRow_childCounter = 0;  
    int static_Input0_ProcessInputRow_parentCounter = 0;  
    bool static_Input0_ProcessInputRow_nextRowIsParent = false;  
  
        // If current row starts with separator characters,   
        // then following row contains new parent record.   
        if (Row.Column0.StartsWith("***"))  
        {  
            static_Input0_ProcessInputRow_nextRowIsParent = true;  
        }  
        else  
        {  
            if (static_Input0_ProcessInputRow_nextRowIsParent)  
            {  
                // Current row contains parent record.   
                static_Input0_ProcessInputRow_parentCounter += 1;  
                this.ParentRecordsBuffer.AddRow();  
                this.ParentRecordsBuffer.ParentID = static_Input0_ProcessInputRow_parentCounter;  
                this.ParentRecordsBuffer.ParentRecord = Row.Column0;  
                static_Input0_ProcessInputRow_nextRowIsParent = false;  
            }  
            else  
            {  
                // Current row contains child record.   
                static_Input0_ProcessInputRow_childCounter += 1;  
                this.ChildRecordsBuffer.AddRow();  
                this.ChildRecordsBuffer.ChildID = static_Input0_ProcessInputRow_childCounter;  
                this.ChildRecordsBuffer.ParentID = static_Input0_ProcessInputRow_parentCounter;  
                this.ChildRecordsBuffer.ChildRecord = Row.Column0;  
            }  
        }  
  
    }  
```  
  
![Integration Services 圖示（小型）](../media/dts-16.gif "Integration Services 圖示 (小)")**與 Integration Services 保持最**新狀態  <br /> 若要取得 Microsoft 的最新下載、文件、範例和影片以及社群中的精選解決方案，請瀏覽 MSDN 上的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 頁面：<br /><br /> [瀏覽 MSDN 上的 Integration Services 頁面](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要得到這些更新的自動通知，請訂閱該頁面上所提供的 RSS 摘要。  
  
## <a name="see-also"></a>另請參閱  
 [使用指令碼元件建立同步轉換](../extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)  
 [使用指令碼元件建立非同步轉換](../extending-packages-scripting-data-flow-script-component-types/creating-an-asynchronous-transformation-with-the-script-component.md)  
  
  
