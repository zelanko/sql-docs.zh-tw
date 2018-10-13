---
title: 在套件工作流程中納入資料分析工作 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- Data Profiling task [Integration Services], using output in workflow
ms.assetid: 39a51586-6977-4c45-b80b-0157a54ad510
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 74e2ca64c47aaf1b0388fa0d58a3e76f2ec9d20e
ms.sourcegitcommit: 0d6e4cafbb5d746e7d00fdacf8f3ce16f3023306
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/11/2018
ms.locfileid: "49085514"
---
# <a name="incorporate-a-data-profiling-task-in-package-workflow"></a>在封裝工作流程中納入資料分析工作
  在早期階段中，資料分析和清除並非自動化處理序的候選項目。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]中，資料分析工作的輸出通常需要進行視覺化分析和人為判斷，才能決定報告的違規項目是否有意義，或是否為過度報告。 甚至在辨識出資料品質問題之後，您仍然必須仔細地全盤規劃，尋求最佳的清除方法。  
  
 不過，當資料品質的準則確立之後，您可能會想要自動化資料來源的定期分析與清除作業。 請考慮這些狀況：  
  
-   **在累加式載入之前檢查資料品質**： 您可以使用資料分析工作，針對用於 Customers 資料表之 CustomerName 資料行的新資料計算資料行 Null 比例設定檔。 如果 Null 值的百分比大於 20%，便傳送一則包含設定檔輸出的電子郵件訊息給操作員，然後結束封裝。 否則，便繼續累加式載入。  
  
-   **符合指定的條件時自動化清除**： 您可以使用資料分析工作，針對 State 資料行 (根據州的查閱資料表) 和 ZIP Code/Postal Code 資料行 (根據郵遞區號的查閱資料表) 計算值包含設定檔。 如果州值的包含強度小於 80%，但是郵遞區號值的包含強度大於 99%，這就代表兩件事。 首先，州的資料不正確。 其次，郵遞區號的資料是正確的。 您可以透過根據目前郵遞區號值執行正確州值的查閱，啟動清除州資料的資料流程工作。  
  
 在您設有可合併資料流程工作的工作流程之後，就必須了解加入這項工作所需的步驟。 下一節將描述合併資料流程工作的一般程序。 最後兩節則描述如何將資料流程工作直接連接至資料來源，或連接至資料流程的已轉換資料。  
  
## <a name="defining-a-general-workflow-for-the-data-flow-task"></a>定義資料流程工作的一般工作流程  
 下列程序將概述在封裝之工作流程中使用資料分析工作輸出的一般方法。  
  
#### <a name="to-use-the-output-of-the-data-profiling-task-programmatically-in-a-package"></a>以程式設計方式在封裝中使用資料分析工作的輸出  
  
1.  加入並設定封裝中的資料分析工作。  
  
2.  設定封裝變數，以便保存您想要從設定檔結果中擷取的值。  
  
3.  加入並設定指令碼工作。 將指令碼工作連接至資料分析工作。 在指令碼工作中，撰寫從資料分析工作之輸出檔中讀取所需值並填入封裝變數的程式碼。  
  
4.  在將指令碼工作連接至工作流程中下游分支的優先順序條件約束中，撰寫使用變數值來導向工作流程的運算式。  
  
 將資料分析工作併入封裝的工作流程時，請記住此工作的兩個功能：  
  
-   **工作輸出**： 資料分析工作會根據 DataProfile.xsd 結構描述，以 XML 格式將其輸出寫入檔案或封裝變數中。 因此，如果您想要在封裝的條件式工作流程中使用設定檔結果，就必須查詢 XML 輸出。 您可以輕易地使用 Xpath 查詢語言來查詢這個 XML 輸出。 若要研究這個 XML 輸出的結構，您可以開啟範例輸出檔或結構描述本身。 若要開啟輸出檔或結構描述，您可以使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]、其他 XML 編輯器或文字編輯器 (例如 [記事本])。  
  
    > [!NOTE]  
    >  某些顯示在「資料設定檔檢視器」中的設定檔結果是無法直接在輸出中找到的計算值。 例如，資料行 Null 比例設定檔的輸出包含了資料列總數以及含有 Null 值的資料列數目。 您必須查詢這兩個值，然後計算含有 Null 值的資料列百分比，才能取得資料行 Null 比例。  
  
-   **工作輸入**： 資料分析工作會從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表中讀取其輸入。 因此，如果您想要分析已經在資料流程中載入並轉換的資料，就必須將記憶體中的資料儲存至臨時資料表。  
  
 下列各節會將這個一般工作流程套用至直接來自外部資料來源或從資料流程工作轉換的分析資料。 此外，這些章節也會說明如何處理資料流程工作的輸入和輸出需求。  
  
## <a name="connecting-the-data-profiling-task-directly-to-an-external-data-source"></a>將資料分析工作直接連接至外部資料來源  
 資料分析工作可以分析直接來自某個資料來源的資料。  為了說明這項功能，下列範例會使用資料分析工作，針對 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料庫中 Person.Address 資料表的資料行計算資料行 Null 比例設定檔。 然後，這則範例會使用指令碼工作，從輸出檔中擷取結果並填入可用來導向工作流程的封裝變數。  
  
> [!NOTE]  
>  在這則簡易範例中，我們選取了 AddressLine2 資料行，因為這個資料行包含 Null 值的百分比很高。  
  
 這個範例包含下列步驟：  
  
-   設定連接管理員，以便連接至外部資料來源以及即將包含設定檔結果的輸出檔。  
  
-   設定封裝變數，以便保存資料分析工作所需的值。  
  
-   設定資料分析工作，以便計算資料行 Null 比例設定檔。  
  
-   設定指令碼工作，以便處理資料分析工作的 XML 輸出。  
  
-   設定優先順序條件約束，以便控制工作流程中的哪些下游分支會根據資料分析工作的結果執行。  
  
### <a name="configure-the-connection-managers"></a>設定連接管理員  
 在這則範例中，我們設有兩個連接管理員：  
  
-   連接至 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 資料庫的 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 連接管理員。  
  
-   建立輸出檔以便保存資料分析工作結果的檔案連接管理員。  
  
##### <a name="to-configure-the-connection-managers"></a>設定連接管理員  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，建立新的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝。  
  
2.  將 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 連接管理員加入至封裝。 將這個連線管理員設定為使用 NET Data Provider for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SqlClient) 並連接至 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料庫的可用執行個體。  
  
     根據預設，此連線管理員具有下列名稱：\<伺服器名稱>.AdventureWorks1。  
  
3.  將檔案連接管理員加入至封裝。 將這個連接管理員設定為建立資料分析工作的輸出檔。  
  
     這個範例會使用檔案名稱 DataProfile1.xml。 根據預設，此連接管理員與該檔案具有相同的名稱。  
  
### <a name="configure-the-package-variables"></a>設定封裝變數  
 這個範例會使用兩個封裝變數：  
  
-   ProfileConnectionName 變數會將檔案連接管理員的名稱傳遞給指令碼工作。  
  
-   AddressLine2NullRatio 變數會從指令碼工作將這個資料行的已計算 Null 比例傳遞給封裝。  
  
##### <a name="to-configure-the-package-variables-that-will-hold-profile-results"></a>設定即將保存設定檔結果的封裝變數  
  
-   在 **[變數]** 視窗中，加入並設定下列兩個封裝變數：  
  
    -   輸入名稱， `ProfileConnectionName`，針對其中一個變數，並設定這個變數的類型**字串**。  
  
    -   輸入名稱， `AddressLine2NullRatio`、 其他變數並將設定這個變數的類型**Double**。  
  
### <a name="configure-the-data-profiling-task"></a>設定資料分析工作  
 您必須以下列方式來設定資料分析工作：  
  
-   使用 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 連接管理員所提供的資料當做輸入。  
  
-   針對輸入資料執行資料行 Null 比例設定檔。  
  
-   將設定檔結果儲存至與檔案連接管理員相關聯的檔案。  
  
##### <a name="to-configure-the-data-profiling-task"></a>設定資料分析工作  
  
1.  針對控制流程，加入資料分析工作。  
  
2.  開啟 **[資料分析工作編輯器]** 以便設定工作。  
  
3.  在編輯器的 **[一般]** 頁面中，針對 **[目的地]** 選取您先前設定之檔案連接管理員的名稱。  
  
4.  在編輯器的 **[設定檔要求]** 頁面中，建立新的資料行 Null 比例設定檔。  
  
5.  在 **[要求屬性]** 窗格中，針對 **[ConnectionManager]** 選取您先前設定的 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 連接管理員。 然後，針對 **[TableOrView]** 選取 Person.Address。  
  
6.  關閉 [資料分析工作編輯器]。  
  
### <a name="configure-the-script-task"></a>設定指令碼工作  
 您必須設定指令碼工作，以便從輸出檔中擷取結果，然後填入先前設定的封裝變數。  
  
##### <a name="to-configure-the-script-task"></a>設定指令碼工作  
  
1.  針對控制流程，加入指令碼工作。  
  
2.  將指令碼工作連接至資料分析工作。  
  
3.  開啟 **[指令碼工作編輯器]** 以便設定工作。  
  
4.  在 **[指令碼]** 頁面中，選取您慣用的程式語言。 然後，讓這兩個封裝變數可供指令碼使用：  
  
    1.  針對`ReadOnlyVariables`，選取`ProfileConnectionName`。  
  
    2.  針對**ReadWriteVariables**，選取`AddressLine2NullRatio`。  
  
5.  選取 **[編輯指令碼]** 以便開啟指令碼開發環境。  
  
6.  加入 System.Xml 命名空間的參考。  
  
7.  輸入對應至您程式語言的範例程式碼：  
  
    ```vb  
    Imports System  
    Imports Microsoft.SqlServer.Dts.Runtime  
    Imports System.Xml  
  
    Public Class ScriptMain  
  
      Private FILENAME As String = "C:\ TEMP\DataProfile1.xml"  
      Private PROFILE_NAMESPACE_URI As String = "http://schemas.microsoft.com/DataDebugger/"  
      Private NULLCOUNT_XPATH As String = _  
        "/default:DataProfile/default:DataProfileOutput/default:Profiles" & _  
        "/default:ColumnNullRatioProfile[default:Column[@Name='AddressLine2']]/default:NullCount/text()"  
      Private TABLE_XPATH As String = _  
        "/default:DataProfile/default:DataProfileOutput/default:Profiles" & _  
        "/default:ColumnNullRatioProfile[default:Column[@Name='AddressLine2']]/default:Table"  
  
      Public Sub Main()  
  
        Dim profileConnectionName As String  
        Dim profilePath As String  
        Dim profileOutput As New XmlDocument  
        Dim profileNSM As XmlNamespaceManager  
        Dim nullCountNode As XmlNode  
        Dim nullCount As Integer  
        Dim tableNode As XmlNode  
        Dim rowCount As Integer  
        Dim nullRatio As Double  
  
        ' Open output file.  
        profileConnectionName = Dts.Variables("ProfileConnectionName").Value.ToString()  
        profilePath = Dts.Connections(profileConnectionName).ConnectionString  
        profileOutput.Load(profilePath)  
        profileNSM = New XmlNamespaceManager(profileOutput.NameTable)  
        profileNSM.AddNamespace("default", PROFILE_NAMESPACE_URI)  
  
        ' Get null count for column.  
        nullCountNode = profileOutput.SelectSingleNode(NULLCOUNT_XPATH, profileNSM)  
        nullCount = CType(nullCountNode.Value, Integer)  
  
        ' Get row count for table.  
        tableNode = profileOutput.SelectSingleNode(TABLE_XPATH, profileNSM)  
        rowCount = CType(tableNode.Attributes("RowCount").Value, Integer)  
  
        ' Compute and return null ratio.  
        nullRatio = nullCount / rowCount  
        Dts.Variables("AddressLine2NullRatio").Value = nullRatio  
  
        Dts.TaskResult = Dts.Results.Success  
  
      End Sub  
  
    End Class  
    ```  
  
    ```csharp  
    using System;  
    using Microsoft.SqlServer.Dts.Runtime;  
    using System.Xml;  
  
    public class ScriptMain  
    {  
  
      private string FILENAME = "C:\\ TEMP\\DataProfile1.xml";  
      private string PROFILE_NAMESPACE_URI = "http://schemas.microsoft.com/DataDebugger/";  
      private string NULLCOUNT_XPATH = "/default:DataProfile/default:DataProfileOutput/default:Profiles" + "/default:ColumnNullRatioProfile[default:Column[@Name='AddressLine2']]/default:NullCount/text()";  
      private string TABLE_XPATH = "/default:DataProfile/default:DataProfileOutput/default:Profiles" + "/default:ColumnNullRatioProfile[default:Column[@Name='AddressLine2']]/default:Table";  
  
      public void Main()  
      {  
  
        string profileConnectionName;  
        string profilePath;  
        XmlDocument profileOutput = new XmlDocument();  
        XmlNamespaceManager profileNSM;  
        XmlNode nullCountNode;  
        int nullCount;  
        XmlNode tableNode;  
        int rowCount;  
        double nullRatio;  
  
        // Open output file.  
        profileConnectionName = Dts.Variables["ProfileConnectionName"].Value.ToString();  
        profilePath = Dts.Connections[profileConnectionName].ConnectionString;  
        profileOutput.Load(profilePath);  
        profileNSM = new XmlNamespaceManager(profileOutput.NameTable);  
        profileNSM.AddNamespace("default", PROFILE_NAMESPACE_URI);  
  
        // Get null count for column.  
        nullCountNode = profileOutput.SelectSingleNode(NULLCOUNT_XPATH, profileNSM);  
        nullCount = (int)nullCountNode.Value;  
  
        // Get row count for table.  
        tableNode = profileOutput.SelectSingleNode(TABLE_XPATH, profileNSM);  
        rowCount = (int)tableNode.Attributes["RowCount"].Value;  
  
        // Compute and return null ratio.  
        nullRatio = nullCount / rowCount;  
        Dts.Variables["AddressLine2NullRatio"].Value = nullRatio;  
  
        Dts.TaskResult = Dts.Results.Success;  
  
      }  
  
    }  
    ```  
  
    > [!NOTE]  
    >  這個程序中顯示的範例程式碼會說明如何從檔案載入資料分析工作的輸出。 若要改為從封裝變數載入資料分析工作的輸出，請參閱這個程序後面的替代範例程式碼。  
  
8.  關閉指令碼開發環境，然後關閉 [指令碼工作編輯器]。  
  
#### <a name="alternative-codereading-the-profile-output-from-a-variable"></a>替代程式碼 - 從變數中讀取設定檔輸出  
 先前的程序示範如何從檔案載入資料分析工作的輸出。 不過，我們提供了替代方法，可從封裝變數載入這個輸出。 若要從變數載入封裝，您必須針對範例程式碼進行下列變更：  
  
-   呼叫 `LoadXml` 類別的 `XmlDocument` 方法，而非 `Load` 方法。  
  
-   在 [指令碼工作編輯器] 中，將包含設定檔輸出之封裝變數的名稱加入至工作的 `ReadOnlyVariables` 清單。  
  
-   將變數的字串值傳遞給 `LoadXML` 方法，如下列程式碼範例所示  (這個範例會使用 "ProfileOutput" 當做包含設定檔輸出之封裝變數的名稱)。  
  
    ```vb  
    Dim outputString As String  
    outputString = Dts.Variables("ProfileOutput").Value.ToString()  
    ...  
    profileOutput.LoadXml(outputString)  
    ```  
  
    ```csharp  
    string outputString;  
    outputString = Dts.Variables["ProfileOutput"].Value.ToString();  
    ...  
    profileOutput.LoadXml(outputString);  
    ```  
  
### <a name="configure-the-precedence-constraints"></a>設定優先順序條件約束  
 您必須設定優先順序條件約束，以便控制工作流程中的哪些下游分支會根據資料分析工作的結果執行。  
  
##### <a name="to-configure-the-precedence-constraints"></a>設定優先順序條件約束  
  
-   在將指令碼工作連接至工作流程中下游分支的優先順序條件約束中，撰寫使用變數值來導向工作流程的運算式。  
  
     例如，您可能會將優先順序條件約束的 **[評估作業]** 設定為 **[運算式與條件約束]**。 然後，您可能會使用 `@AddressLine2NullRatio < .90` 當做運算式的值。 當先前的工作成功，而且選取資料行中 Null 值的百分比小於 90% 時，這樣做會導致工作流程遵循選取的路徑。  
  
## <a name="connecting-the-data-profiling-task-to-transformed-data-from-the-data-flow"></a>將資料分析工作連接至資料流程的已轉換資料  
 除了分析直接來自資料來源的資料以外，您也可以分析已經在資料流程中載入並轉換的資料。 不過，資料分析工作只能針對保存的資料運作，無法針對記憶體中的資料運作。 因此，您必須先使用目的地元件，將已轉換的資料儲存至臨時資料表。  
  
> [!NOTE]  
>  設定資料分析工作時，您必須選取現有的資料表和資料行。 因此，您必須先在設計階段建立臨時資料表，然後才能設定工作。 換言之，這個狀況不允許您使用在執行階段建立的暫存資料表。  
  
 將資料儲存至臨時資料表之後，您就可以進行下列動作：  
  
-   使用資料分析工作來分析資料。  
  
-   使用指令碼工作來讀取結果，如本主題前文所述。  
  
-   使用這些結果來導向封裝的後續工作流程。  
  
 下列程序將提供使用資料分析工作來分析已經由資料流程轉換之資料的一般方法。 其中許多步驟都與先前針對分析直接來自外部資料來源之資料所描述的步驟相同。 如需有關如何設定各種元件的詳細資訊，您可能會想要檢閱先前的步驟。  
  
#### <a name="to-use-the-data-profiling-task-in-the-data-flow"></a>在資料流程中使用資料分析工作  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，建立封裝。  
  
2.  在資料流程中，加入、設定並連接適當的來源和轉換。  
  
3.  在資料流程中，加入、設定並連接將已轉換資料儲存至臨時資料表的目的地元件。  
  
4.  在控制流程中，加入並設定根據臨時資料表中已轉換資料計算所需設定檔的資料分析工作。 將資料分析工作連接至資料流程工作。  
  
5.  設定封裝變數，以便保存您想要從設定檔結果中擷取的值。  
  
6.  加入並設定指令碼工作。 將指令碼工作連接至資料分析工作。 在指令碼工作中，撰寫從資料分析工作之輸出中讀取所需值並填入封裝變數的程式碼。  
  
7.  在將指令碼工作連接至工作流程中下游分支的優先順序條件約束中，撰寫使用變數值來導向工作流程的運算式。  
  
## <a name="see-also"></a>另請參閱  
 [資料分析工作的設定](data-profiling-task.md)   
 [資料設定檔檢視器](data-profile-viewer.md)  
  
  
