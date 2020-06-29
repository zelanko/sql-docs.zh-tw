---
title: 使用指令碼元件建立來源 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- Script component [Integration Services], source components
- output columns [Integration Services]
- sources [Integration Services], components
ms.assetid: 547c4179-ea82-4265-8c6f-04a2aa77a3c0
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ce3cd275cea40ad3485066157b3fe02ceedd98ad
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/26/2020
ms.locfileid: "85426955"
---
# <a name="creating-a-source-with-the-script-component"></a>以指令碼元件建立來源
  您在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝的資料流程中使用來源元件，以從資料來源載入資料，進而將其傳遞至下游轉換與目的地。 通常您會透過現有的連接管理員來連接到資料來源。

 如需腳本元件的總覽，請參閱 [使用腳本元件擴充資料流程] （。/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md.

 指令碼元件以及它為您產生的基礎結構程式碼，可大幅簡化開發自訂資料流程元件的程序。 不過，若要了解指令碼元件如何運作，全部讀完開發自訂資料流程元件所需的步驟，可能會非常有用。 請參閱[開發自訂資料流程元件](../extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)一節，尤其是[開發自訂來源元件](../extending-packages-custom-objects-data-flow-types/developing-a-custom-source-component.md)主題。

## <a name="getting-started-with-a-source-component"></a>開始使用來源元件
 當您將指令碼元件新增至 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計工具的 [資料流程] 窗格時，就會開啟 [選取指令碼元件類型]  對話方塊，並提示您選取 [來源]、[目的地] 或是 [轉換] 指令碼。 在這個對話方塊中，選取 [來源]  。

## <a name="configuring-a-source-component-in-metadata-design-mode"></a>在中繼資料設計模式中設定來源元件
 選擇建立來源元件之後，您可以使用 [指令碼轉換編輯器]  來設定元件。 如需詳細資訊，請參閱[在指令碼元件編輯器中設定指令碼元件](../extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md)。

 資料流程來源元件沒有輸入，而且支援一或多個輸出。 設定元件的輸出是您必須在中繼資料設計模式下完成的其中一個步驟，方法是在撰寫自訂指令碼之前先使用 [指令碼轉換編輯器]  。

 您也可以在 [指令碼轉換編輯器]  的 [指令碼]  頁面上設定 [ScriptLanguage]  屬性，來指定指令碼語言。

> [!NOTE]
>  若要為指令碼元件和指令碼工作設定預設指令碼語言，請使用 [選項]  對話方塊的 [一般]  頁面上的 [指令碼語言]  選項。 如需相關資訊，請參閱 [General Page](../general-page-of-integration-services-designers-options.md)。

### <a name="adding-connection-managers"></a>加入連接管理員
 通常來源元件使用現有的連接管理員，以連接到它將資料載入資料流程的資料來源。 在 [指令碼轉換編輯器]  的 [連線管理員]  頁面上，按一下 [新增]  新增適當的連線管理員。

 然而，連接管理員只是一種便利的單位，用以封裝和儲存連接至特定類型的資料來源所需的資訊。 您必須撰寫自己的自訂程式碼，以載入或是儲存資料，以及 (可能的話) 開啟和關閉連至資料來源的連接。

 如需如何利用指令碼元件以使用連線管理員的一般資訊，請參閱[在指令碼元件中連線至資料來源](../extending-packages-scripting/data-flow-script-component/connecting-to-data-sources-in-the-script-component.md)。

 如需 [指令碼轉換編輯器]  之 [連線管理員]  頁面的詳細資訊，請參閱[指令碼轉換編輯器 &#40;連線管理員頁面&#41;](../script-transformation-editor-connection-managers-page.md)。

### <a name="configuring-outputs-and-output-columns"></a>設定輸出和輸出資料行
 來源元件沒有輸入，而且支援一或多個輸出。 在 [指令碼轉換編輯器]  的 [輸入及輸出]  頁面上，預設已建立單一輸出，但是尚未建立輸出資料行。 在編輯器的此頁面上，您可能會需要或想要設定下列項目。

-   您必須為每個輸出手動加入和設定輸出資料行。 為每個輸出選取 [輸出資料行] 資料夾，然後使用 [新增資料行]  和 [移除資料行]  按鈕，為來源元件的每個輸出管理輸出資料行。 之後，您將在指令碼中使用這裡所指派的名稱來參考輸出資料行，方法是使用在自動產生的程式碼中為您建立的具有類型之存取子屬性。

-   您可能會想要建立一或多個其他輸出，例如含有非預期值的資料列之模擬錯誤輸出。 使用 [新增輸出]  和 [移除輸出]  按鈕管理來源元件的輸出。 所有的輸入資料列都會導向至所有可用的輸出，除非您也為那些輸出的 `ExclusionGroup` 屬性指定相同的非零值，也就是您想要將每個輸入資料列導向至有著相同 `ExclusionGroup` 值的其中一個輸出。 至於選取哪一個特定的整數值以識別 `ExclusionGroup` 則無關緊要。

    > [!NOTE]
    >  當您不想要輸出所有的資料列時，也可以使用具有單一輸出的非零 `ExclusionGroup` 屬性值。 不過，在此情況下，您必須針對要傳送至輸出的每個資料列，明確地呼叫**DirectRowTo \<outputbuffer> **方法。

-   您可能會想要將易記名稱指派給輸出。 之後，您將在指令碼中使用輸出的名稱來加以參考，方法是使用在自動產生的程式碼中為您建立的具有類型之存取子屬性。

-   通常，在相同 `ExclusionGroup` 中的多個輸出都有相同的輸出資料行。 然而，如果您正在建立模擬的錯誤輸出，可能會想要加入更多的資料行以儲存錯誤資訊。 如需資料流程引擎如何處理錯誤資料列的資訊，請參閱[使用資料流程元件中的錯誤輸出](../extending-packages-custom-objects/data-flow/using-error-outputs-in-a-data-flow-component.md)。 不過，在指令碼元件中，您必須撰寫自已的程式碼，以適當的錯誤資訊填入其他資料行。 如需詳細資訊，請參閱[模擬指令碼元件的錯誤輸出](../extending-packages-scripting-data-flow-script-component-examples/simulating-an-error-output-for-the-script-component.md)。

 如需 [指令碼轉換編輯器]  之 [輸入及輸出]  頁面的詳細資訊，請參閱[指令碼轉換編輯器 &#40;輸入及輸出頁面&#41;](../script-transformation-editor-inputs-and-outputs-page.md)。

### <a name="adding-variables"></a>加入變數
 如果有任何現有變數的值是您想要在腳本中使用的，您可以在 [ `ReadOnlyVariables` `ReadWriteVariables` **腳本轉換編輯器**] 的 [**腳本**] 頁面上，將它們加入和屬性欄位中。

 當您在屬性欄位中輸入多個變數時，請用逗號分隔變數名稱。 您也可以按一下和屬性欄位旁的省略號（**...**）按鈕 `ReadOnlyVariables` `ReadWriteVariables` ，然後在 [**選取變數**] 對話方塊中選取變數，以輸入多個變數。

 如需如何利用指令碼元件使用變數的一般資訊，請參閱[在指令碼元件中使用變數](../extending-packages-scripting/data-flow-script-component/using-variables-in-the-script-component.md)。

 如需 [指令碼轉換編輯器]  的 [指令碼]  頁面的詳細資訊，請參閱[指令碼轉換編輯器 &#40;指令碼頁面&#41;](../script-transformation-editor-script-page.md)。

## <a name="scripting-a-source-component-in-code-design-mode"></a>在程式碼設計模式中編寫來源元件的指令碼
 在您已為元件設定中繼資料之後，請開啟 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA) IDE 以撰寫自訂指令碼。 若要開啟 VSTA，請在 [指令碼轉換編輯器]  的 [指令碼]  頁面上，按一下 [編輯指令碼]  。 您可以使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic 或 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C# 撰寫指令碼，視為 **ScriptLanguage** 屬性選取的指令碼語言而定。

 如需使用指令碼元件所建立之各種元件都適用的重要資訊，請參閱[編碼和偵錯指令碼元件](../extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md)。

### <a name="understanding-the-auto-generated-code"></a>了解自動產生的程式碼
 當您在建立和設定來源元件之後開啟 VSTA IDE，可編輯的 `ScriptMain` 類別會出現在程式碼編輯器中。 您在 `ScriptMain` 類別中撰寫自訂程式碼。

 `ScriptMain` 類別包括 `CreateNewOutputRows` 方法的 Stub。 `CreateNewOutputRows` 是來源元件中最重要的方法。

 如果您在 VSTA 中開啟 [**專案管理器**] 視窗，您可以看到腳本元件也會產生唯讀 `BufferWrapper` 和 `ComponentWrapper` 專案專案。 `ScriptMain` 類別會繼承 `UserComponent` 專案項目中的 `ComponentWrapper` 類別。

 在執行階段，資料流程引擎會叫用 `PrimeOutput` 類別中的 `UserComponent` 方法，它會覆寫 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponentHost.PrimeOutput%2A> 父類別的 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> 方法。 `PrimeOutput` 方法會依序呼叫下列方法：

1.  您在 `CreateNewOutputRows` 中覆寫以便從資料來源將資料列加入輸出緩衝區的 `ScriptMain` 方法，一開始會是空的。

2.   方法預設是空的。 在 `ScriptMain` 中覆寫此方法以執行完成輸出所需的處理。

3.  私用 `MarkOutputsAsFinished` 方法 (呼叫 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer.SetEndOfRowset%2A> 父類別的 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer> 方法) 用以指出輸出已完成的資料流程引擎。 在自己的程式碼中不必明確地呼叫 `SetEndOfRowset`。

### <a name="writing-your-custom-code"></a>撰寫您的自訂程式碼
 為了完成建立自訂來源元件，您可能會想要以 `ScriptMain` 類別中提供的下列方法來撰寫指令碼。

1.  覆寫 `AcquireConnections` 方法以連接至外部資料來源。 從連接管理員擷取連接物件，或是必要的連接資訊。

2.  如果您可以同時載入所有的來源資料，請覆寫 `PreExecute` 方法以載入資料。 例如，您可以針對連至 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 資料庫的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 連接，執行 `SqlCommand`，並同時將所有的來源資料載入 `SqlDataReader`。 如果您必須一次載入一個資料列的來源資料 (例如，在讀取文字檔時)，可以在 `CreateNewOutputRows` 中循環使用資料列時載入資料。

3.  使用覆寫的 `CreateNewOutputRows` 方法將新資料列加入空的輸出緩衝區，並將新輸出資料列中的每個資料行填入值。 使用每個輸出緩衝區的 `AddRow` 方法，加入空的新資料列，然後設定每個資料行的值。 通常您會複製從外部來源載入的資料行值。

4.  覆寫 `PostExecute` 方法以完成處理資料。 例如，您可以關閉用以載入資料的 `SqlDataReader`。

5.  視需要，覆寫 `ReleaseConnections` 方法從外部資料來源中斷連接。

## <a name="examples"></a>範例
 下列範例示範建立來源元件時，`ScriptMain` 類別中所需的自訂程式碼。

> [!NOTE]
>  這些範例使用範例資料庫中的**Person**資料表， `AdventureWorks` 並透過資料流程傳遞第一個和第四個數據行，也就是**intAddressID**和**Nvarchar （30） City**資料行。 在本章節中的來源、轉換和目的地範例使用相同的資料。 每個範例都會記載其他必要條件與假設。

### <a name="adonet-source-example"></a>ADO.NET 來源範例
 這個範例示範一個來源元件，它使用現有的 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 連線管理員，從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表將資料載入資料流程。

 如果您要執行這個範例程式碼，必須依下列方式設定封裝與元件：

1.  建立一個 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 連接管理員，以使用 `SqlClient` 提供者連接到 `AdventureWorks` 資料庫。

2.  將新指令碼元件加入資料流程設計師介面，並將它設定為來源。

3.  開啟**指令碼轉換編輯器**。 在 [輸入及輸出]  頁面上，以更具描述性的名稱重新命名預設輸出，例如 **MyAddressOutput**，以及新增和設定兩個輸出資料行：**AddressID** 和 **City**。

    > [!NOTE]
    >  務必將 **City** 輸出資料行的資料類型變更為 DT_WSTR。

4.  在 [連線管理員]  頁面上，新增或建立 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 連線管理員，並指定一個名稱，例如 **MyADONETConnection**。

5.  在 [指令碼]  頁面上，按一下 [編輯指令碼]  ，並輸入以下指令碼。 然後關閉指令碼開發環境以及 [指令碼轉換編輯器]  。

6.  建立和設定目的地元件，例如 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目的地，或是在[使用指令碼元件建立目的地](../extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)中所示範的範例目的地元件，它需要 **AddressID** 和 **City** 資料行。 然後將來源元件連接到目的地 （您可以直接將來源連接到目的地，而不需要任何轉換）。您可以 [!INCLUDE[tsql](../../includes/tsql-md.md)] 在資料庫中執行下列命令，以建立目的地資料表 `AdventureWorks` ：

    ```
    CREATE TABLE [Person].[Address2]([AddressID] [int] NOT NULL,
        [City] [nvarchar](30) NOT NULL)
    ```

7.  執行範例。

    ```vb
    Imports System.Data.SqlClient
    ...
    Public Class ScriptMain
        Inherits UserComponent

        Dim connMgr As IDTSConnectionManager100
        Dim sqlConn As SqlConnection
        Dim sqlReader As SqlDataReader

        Public Overrides Sub AcquireConnections(ByVal Transaction As Object)

            connMgr = Me.Connections.MyADONETConnection
            sqlConn = CType(connMgr.AcquireConnection(Nothing), SqlConnection)

        End Sub

        Public Overrides Sub PreExecute()

            Dim cmd As New SqlCommand("SELECT AddressID, City, StateProvinceID FROM Person.Address", sqlConn)
            sqlReader = cmd.ExecuteReader

        End Sub

        Public Overrides Sub CreateNewOutputRows()

            Do While sqlReader.Read
                With MyAddressOutputBuffer
                    .AddRow()
                    .AddressID = sqlReader.GetInt32(0)
                    .City = sqlReader.GetString(1)
                End With
            Loop

        End Sub

        Public Overrides Sub PostExecute()

            sqlReader.Close()

        End Sub

        Public Overrides Sub ReleaseConnections()

            connMgr.ReleaseConnection(sqlConn)

        End Sub

    End Class
    ```

    ```csharp
    using System.Data.SqlClient;
    public class ScriptMain:
        UserComponent

    {
        IDTSConnectionManager100 connMgr;
        SqlConnection sqlConn;
        SqlDataReader sqlReader;

        public override void AcquireConnections(object Transaction)
        {
            connMgr = this.Connections.MyADONETConnection;
            sqlConn = (SqlConnection)connMgr.AcquireConnection(null);

        }

        public override void PreExecute()
        {

            SqlCommand cmd = new SqlCommand("SELECT AddressID, City, StateProvinceID FROM Person.Address", sqlConn);
            sqlReader = cmd.ExecuteReader();

        }

        public override void CreateNewOutputRows()
        {

            while (sqlReader.Read())
            {
                {
                    MyAddressOutputBuffer.AddRow();
                    MyAddressOutputBuffer.AddressID = sqlReader.GetInt32(0);
                    MyAddressOutputBuffer.City = sqlReader.GetString(1);
                }
            }

        }

        public override void PostExecute()
        {

            sqlReader.Close();

        }

        public override void ReleaseConnections()
        {

            connMgr.ReleaseConnection(sqlConn);

        }

    }
    ```

### <a name="flat-file-source-example"></a>一般檔案來源範例
 這個範例示範一個來源元件，它使用現有的一般檔案連接管理員，從一般檔案將資料載入資料流程。 透過從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 將它匯出，就會建立一般檔案來源資料。

 如果您要執行這個範例程式碼，必須依下列方式設定封裝與元件：

1.  使用 [匯 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 入和匯出嚮導]，將 [ **Person. Address** ] 資料表從 `AdventureWorks` 範例資料庫匯出至逗號分隔的一般檔案。 這個範例使用的檔案名稱為 ExportedAddresses.txt。

2.  建立一般檔案連接管理員以連接至匯出的資料檔案。

3.  將新指令碼元件加入資料流程設計師介面，並將它設定為來源。

4.  開啟**指令碼轉換編輯器**。 在 [輸入及輸出]  頁面上，以更具描述性的名稱重新命名預設輸出，例如 **MyAddressOutput**。 新增和設定兩個輸出資料行：**AddressID** 和 **City**。

5.  在 [連線管理員]  頁面上，使用更具描述性的名稱 (例如 **MyFlatFileSrcConnectionManager**) 以新增或建立一般檔案連線管理員。

6.  在 [指令碼]  頁面上，按一下 [編輯指令碼]  ，並輸入以下指令碼。 然後關閉指令碼開發環境以及 [指令碼轉換編輯器]  。

7.  建立和設定目的地元件，例如 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目的地，或是在[使用指令碼元件建立目的地](../extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)中所示範的範例目的地元件。 然後將來源元件連接到目的地 （您可以直接將來源連接到目的地，而不需要任何轉換）。您可以 [!INCLUDE[tsql](../../includes/tsql-md.md)] 在資料庫中執行下列命令，以建立目的地資料表 `AdventureWorks` ：

    ```
    CREATE TABLE [Person].[Address2]([AddressID] [int] NOT NULL,
        [City] [nvarchar](30) NOT NULL)
    ```

8.  執行範例。

    ```vb
    Imports System.IO
    ...
    Public Class ScriptMain
        Inherits UserComponent

        Private textReader As StreamReader
        Private exportedAddressFile As String

        Public Overrides Sub AcquireConnections(ByVal Transaction As Object)

            Dim connMgr As IDTSConnectionManager100 = _
                Me.Connections.MyFlatFileSrcConnectionManager
            exportedAddressFile = _
                CType(connMgr.AcquireConnection(Nothing), String)

        End Sub

        Public Overrides Sub PreExecute()
            MyBase.PreExecute()
            textReader = New StreamReader(exportedAddressFile)
        End Sub

        Public Overrides Sub CreateNewOutputRows()

            Dim nextLine As String
            Dim columns As String()

            Dim delimiters As Char()
            delimiters = ",".ToCharArray

            nextLine = textReader.ReadLine
            Do While nextLine IsNot Nothing
                columns = nextLine.Split(delimiters)
                With MyAddressOutputBuffer
                    .AddRow()
                    .AddressID = columns(0)
                    .City = columns(3)
                End With
                nextLine = textReader.ReadLine
            Loop

        End Sub

        Public Overrides Sub PostExecute()
            MyBase.PostExecute()
            textReader.Close()

        End Sub

    End Class
    ```

    ```csharp
    using System.IO;
    public class ScriptMain:
        UserComponent

    {
        private StreamReader textReader;
        private string exportedAddressFile;

        public override void AcquireConnections(object Transaction)
        {

            IDTSConnectionManager100 connMgr = this.Connections.MyFlatFileSrcConnectionManager;
            exportedAddressFile = (string)connMgr.AcquireConnection(null);

        }

        public override void PreExecute()
        {
            base.PreExecute();
            textReader = new StreamReader(exportedAddressFile);
        }

        public override void CreateNewOutputRows()
        {

            string nextLine;
            string[] columns;

            char[] delimiters;
            delimiters = ",".ToCharArray();

            nextLine = textReader.ReadLine();
            while (nextLine != null)
            {
                columns = nextLine.Split(delimiters);
                {
                    MyAddressOutputBuffer.AddRow();
                    MyAddressOutputBuffer.AddressID = columns[0];
                    MyAddressOutputBuffer.City = columns[3];
                }
                nextLine = textReader.ReadLine();
            }

        }

        public override void PostExecute()
        {

            base.PostExecute();
            textReader.Close();

        }

    }
    ```

![Integration Services 圖示（小型）](../media/dts-16.gif "Integration Services 圖示 (小)")**與 Integration Services 保持最**新狀態  <br /> 若要取得 Microsoft 的最新下載、文件、範例和影片以及社群中的精選解決方案，請瀏覽 MSDN 上的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 頁面：<br /><br /> [瀏覽 MSDN 上的 Integration Services 頁面](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要得到這些更新的自動通知，請訂閱該頁面上所提供的 RSS 摘要。

## <a name="see-also"></a>另請參閱
 [使用腳本元件建立目的地以](../extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)[開發自訂來源元件](../extending-packages-custom-objects-data-flow-types/developing-a-custom-source-component.md)


