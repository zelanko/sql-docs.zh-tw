---
title: "使用指令碼元件建立來源 |Microsoft 文件"
ms.custom: 
ms.date: 03/17/2017
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
- Script component [Integration Services], source components
- output columns [Integration Services]
- sources [Integration Services], components
ms.assetid: 547c4179-ea82-4265-8c6f-04a2aa77a3c0
caps.latest.revision: 59
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: d4944c3d5752da21fed90f16a38a33b4fad41515
ms.contentlocale: zh-tw
ms.lasthandoff: 09/26/2017

---
# <a name="creating-a-source-with-the-script-component"></a>以指令碼元件建立來源
  您在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝的資料流程中使用來源元件，以從資料來源載入資料，進而將其傳遞至下游轉換與目的地。 通常您會透過現有的連接管理員來連接到資料來源。  
  
 如需指令碼元件的概觀，請參閱[Extending the Data Flow with Script Component](../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md)。  
  
 指令碼元件以及它為您產生的基礎結構程式碼，可大幅簡化開發自訂資料流程元件的程序。 不過，若要了解指令碼元件如何運作，全部讀完開發自訂資料流程元件所需的步驟，可能會非常有用。 請參閱節[開發自訂資料流程元件](../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)，特別是 <<c4> [ 開發自訂來源元件](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-source-component.md)。  
  
## <a name="getting-started-with-a-source-component"></a>開始使用來源元件  
 當您將指令碼元件加入至 [資料流程] 窗格的[!INCLUDE[ssIS](../../includes/ssis-md.md)]設計工具中，**選取指令碼元件類型**對話方塊會開啟，並提示您選取的來源、 目的地或轉換的指令碼。 在此對話方塊中，選取**來源**。  
  
## <a name="configuring-a-source-component-in-metadata-design-mode"></a>在中繼資料設計模式中設定來源元件  
 選取後建立來源元件，您必須設定元件利用**指令碼轉換編輯器**。 如需詳細資訊，請參閱[設定指令碼元件指令碼元件編輯器中](../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md)。  
  
 資料流程來源元件沒有輸入，而且支援一或多個輸出。 設定輸出的元件是其中一個步驟，您必須使用中繼資料設計模式中，在完成**指令碼轉換編輯器**，然後才能在您撰寫自訂指令碼。  
  
 您也可以藉由設定指定的指令碼語言**ScriptLanguage**屬性**指令碼**頁面**指令碼轉換編輯器**。  
  
> [!NOTE]  
>  若要設定指令碼元件和指令碼工作的預設指令碼語言，使用**指令碼語言**選項**一般**頁面**選項** 對話方塊。 如需相關資訊，請參閱 [General Page](~/integration-services/control-flow/script-task-editor-general-page.md)。  
  
### <a name="adding-connection-managers"></a>加入連接管理員  
 通常來源元件使用現有的連接管理員，以連接到它將資料載入資料流程的資料來源。 在**連接管理員**頁面**指令碼轉換編輯器**，按一下 **新增**新增適當的連接管理員。  
  
 然而，連接管理員只是一種便利的單位，用以封裝和儲存連接至特定類型的資料來源所需的資訊。 您必須撰寫自己的自訂程式碼，以載入或是儲存資料，以及 (可能的話) 開啟和關閉連至資料來源的連接。  
  
 如需如何透過指令碼元件使用連接管理員的一般資訊，請參閱[連接到指令碼元件中的資料來源](../../integration-services/extending-packages-scripting/data-flow-script-component/connecting-to-data-sources-in-the-script-component.md)。  
  
 如需有關**連接管理員**頁面**指令碼轉換編輯器**，請參閱[指令碼轉換編輯器 &#40;連接管理員頁面 &#41;](../../integration-services/data-flow/transformations/script-transformation-editor-connection-managers-page.md).  
  
### <a name="configuring-outputs-and-output-columns"></a>設定輸出和輸出資料行  
 來源元件沒有輸入，而且支援一或多個輸出。 在**輸入和輸出**頁面**指令碼轉換編輯器**，根據預設，已建立單一輸出，但是尚未建立任何輸出資料行。 在編輯器的此頁面上，您可能會需要或想要設定下列項目。  
  
-   您必須為每個輸出手動加入和設定輸出資料行。 選取每個輸出，輸出資料行 資料夾，然後使用**加入資料行**和**移除資料行**按鈕管理來源元件的每個輸出的輸出資料行。 之後，您將在指令碼中使用這裡所指派的名稱來參考輸出資料行，方法是使用在自動產生的程式碼中為您建立的具有類型之存取子屬性。  
  
-   您可能會想要建立一或多個其他輸出，例如含有非預期值的資料列之模擬錯誤輸出。 使用**加入輸出**和**移除輸出**按鈕管理來源元件的輸出。 所有輸入資料列會導向至所有可用的輸出，除非您同時指定相同的非零值的**ExclusionGroup**那些您想要將導向至其中一個共用相同的輸出的每個資料列的輸出屬性**ExclusionGroup**值。 若要識別選取特定的整數值**ExclusionGroup**並不重要。  
  
    > [!NOTE]  
    >  您也可以使用非零**ExclusionGroup**具有單一輸出，當您不想要輸出所有資料列的屬性值。 在此情況下，不過，您必須明確呼叫**DirectRowTo\<outputbuffer >**您想要傳送至輸出每個資料列的方法。  
  
-   您可能會想要將易記名稱指派給輸出。 之後，您將在指令碼中使用輸出的名稱來加以參考，方法是使用在自動產生的程式碼中為您建立的具有類型之存取子屬性。  
  
-   多個在相同的輸出通常**ExclusionGroup**有相同的輸出資料行。 然而，如果您正在建立模擬的錯誤輸出，可能會想要加入更多的資料行以儲存錯誤資訊。 如需如何資料流程引擎的相關資訊，處理錯誤資料列，請參閱[資料流程元件中使用錯誤輸出](../../integration-services/extending-packages-custom-objects/data-flow/using-error-outputs-in-a-data-flow-component.md)。 不過，在指令碼元件中，您必須撰寫自已的程式碼，以適當的錯誤資訊填入其他資料行。 如需詳細資訊，請參閱[模擬錯誤輸出指令碼元件](../../integration-services/extending-packages-scripting-data-flow-script-component-examples/simulating-an-error-output-for-the-script-component.md)。  
  
 如需有關**輸入和輸出**頁面**指令碼轉換編輯器**，請參閱[指令碼轉換編輯器 &#40; 輸入及輸出頁面 &#41;](../../integration-services/data-flow/transformations/script-transformation-editor-inputs-and-outputs-page.md)。  
  
### <a name="adding-variables"></a>加入變數  
 如果有任何現有變數的值，您想要使用指令碼中，您可以將其加入**[readonlyvariables]**和**[readwritevariables]**屬性欄位上**指令碼**頁面**指令碼轉換編輯器**。  
  
 當您在屬性欄位中輸入多個變數時，請用逗號分隔變數名稱。 您也可以輸入多個變數，依序按一下省略符號 (**...**) 旁邊**[readonlyvariables]**和**[readwritevariables]**中的，選取變數和屬性欄位**選取變數**對話方塊.  
  
 如需如何使用指令碼元件中使用變數的一般資訊，請參閱[在指令碼元件中使用變數](../../integration-services/extending-packages-scripting/data-flow-script-component/using-variables-in-the-script-component.md)。  
  
 如需有關**指令碼**頁面**指令碼轉換編輯器**，請參閱[指令碼轉換編輯器 &#40;指令碼頁面 &#41;](../../integration-services/data-flow/transformations/script-transformation-editor-script-page.md).  
  
## <a name="scripting-a-source-component-in-code-design-mode"></a>在程式碼設計模式中編寫來源元件的指令碼  
 您已設定您的元件中繼資料之後，請開啟[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA) IDE 以撰寫自訂指令碼。 若要開啟 VSTA，請按一下**編輯指令碼**上**指令碼**頁面**指令碼轉換編輯器**。 您可以撰寫指令碼使用[!INCLUDE[msCoName](../../includes/msconame-md.md)]Visual Basic 或[!INCLUDE[msCoName](../../includes/msconame-md.md)]Visual C# 中，針對選取的指令碼語言而定**ScriptLanguage**屬性。  
  
 適用於所有類型的元件所使用的指令碼元件建立的重要資訊，請參閱[編碼和偵錯指令碼元件](../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md)。  
  
### <a name="understanding-the-auto-generated-code"></a>了解自動產生的程式碼  
 當您在建立並設定來源元件，可編輯之後開啟 VSTA IDE 時**ScriptMain**類別會出現在程式碼編輯器。 您可以撰寫自訂程式碼**ScriptMain**類別。  
  
 **ScriptMain**類別包含的 stub **CreateNewOutputRows**方法。 **CreateNewOutputRows**是來源元件中最重要的方法。  
  
 如果您開啟**Project Explorer**視窗在 VSTA 中的，您可以看到，指令碼元件也會產生唯讀**BufferWrapper**和**ComponentWrapper**專案項目。 **ScriptMain**類別繼承自**UserComponent**類別**ComponentWrapper**專案項目。  
  
 在執行階段，資料流程引擎會叫用**PrimeOutput**方法中的**UserComponent**類別，它會覆寫<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.PrimeOutput%2A>方法<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent>父類別。 **PrimeOutput**方法會呼叫下列方法：  
  
1.  **CreateNewOutputRows**方法，在您覆寫**ScriptMain**從資料來源的資料列加入輸出緩衝區，也就是空的一開始。  
  
2.  **FinishOutputs**方法，預設是空的。 覆寫這個方法在**ScriptMain**執行完成輸出所需的任何處理。  
  
3.  私用**MarkOutputsAsFinished**方法，這個方法會呼叫<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer.SetEndOfRowset%2A>方法<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer>父類別，表示資料流程引擎輸出已完成。 您不需要呼叫**SetEndOfRowset**在自己的程式碼中明確。  
  
### <a name="writing-your-custom-code"></a>撰寫您的自訂程式碼  
 為了完成建立自訂來源元件，您可能想要撰寫指令碼中提供下列方法**ScriptMain**類別。  
  
1.  覆寫**AcquireConnections**方法，以連接到外部資料來源。 從連接管理員擷取連接物件，或是必要的連接資訊。  
  
2.  覆寫**PreExecute**方法來載入資料時，如果您可以同時載入所有來源資料。 例如，您可以執行**SqlCommand**針對[!INCLUDE[vstecado](../../includes/vstecado-md.md)]連接[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫中，所有來源資料都載入到同時**SqlDataReader**。 如果您必須載入的來源資料的一列一次 （例如，讀取文字檔時），您可以將資料載入循環使用中的資料列**CreateNewOutputRows**。  
  
3.  使用覆寫**CreateNewOutputRows**方法以將新的資料列加入空的輸出緩衝區，並填入新的輸出資料列中每個資料行的值。 使用**AddRow**方法的每一個輸出緩衝區，來加入空白的新資料列，然後再將 每個資料行的值。 通常您會複製從外部來源載入的資料行值。  
  
4.  覆寫**PostExecute**方法來完成處理資料。 例如，您可以關閉**SqlDataReader**您用來載入資料。  
  
5.  覆寫**ReleaseConnections**外部資料來源中斷連線，視需要的方法。  
  
## <a name="examples"></a>範例  
 下列範例示範自訂程式碼所需的**ScriptMain**類別來建立來源元件。  
  
> [!NOTE]  
>  這些範例使用**Person.Address**資料表中**AdventureWorks**範例資料庫，並傳遞其第一個和第四個資料行， **intAddressID**和**nvarchar (30) 縣 （市)** ，經過資料流資料行。 在本章節中的來源、轉換和目的地範例使用相同的資料。 每個範例都會記載其他必要條件與假設。  
  
### <a name="adonet-source-example"></a>ADO.NET 來源範例  
 這個範例示範一個來源元件，它使用現有[!INCLUDE[vstecado](../../includes/vstecado-md.md)]與載入資料的連接管理員[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]至資料流程的資料表。  
  
 如果您要執行這個範例程式碼，必須依下列方式設定封裝與元件：  
  
1.  建立[!INCLUDE[vstecado](../../includes/vstecado-md.md)]使用連接管理員**SqlClient**提供者連接到**AdventureWorks**資料庫。  
  
2.  將新指令碼元件加入資料流程設計師介面，並將它設定為來源。  
  
3.  開啟**指令碼轉換編輯器**。 在**輸入和輸出**頁面上，重新命名預設輸出更具描述性的名稱，例如**MyAddressOutput**，以及加入和設定兩個輸出資料行**AddressID**和**縣 （市)**。  
  
    > [!NOTE]  
    >  確定要變更的資料型別**縣 （市)**為 DT_WSTR 的輸出資料行。  
  
4.  在**連接管理員**頁面上，加入或建立[!INCLUDE[vstecado](../../includes/vstecado-md.md)]連接管理員並加以命名，例如**MyADONETConnection**。  
  
5.  在**指令碼**頁面上，按一下**編輯指令碼**並輸入以下指令碼。 然後關閉 指令碼開發環境和**指令碼轉換編輯器**。  
  
6.  建立和設定目的地元件，例如[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]目的地、 或中所示範的範例目的地元件[與指令碼元件建立目的地](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)，它需要**AddressID**和**縣 （市)**資料行。 然後將來源元件連接到目的地  (不需要任何轉換，就可以直接將來源連接到目的地)。您可以執行下列命令，以建立目的地資料表[!INCLUDE[tsql](../../includes/tsql-md.md)]命令**AdventureWorks**資料庫：  
  
    ```sql
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
  
1.  使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]匯入和匯出精靈 」，匯出**Person.Address**資料表中**AdventureWorks**到逗點分隔的一般檔案的範例資料庫。 這個範例使用的檔案名稱為 ExportedAddresses.txt。  
  
2.  建立一般檔案連接管理員以連接至匯出的資料檔案。  
  
3.  將新指令碼元件加入資料流程設計師介面，並將它設定為來源。  
  
4.  開啟**指令碼轉換編輯器**。 在**輸入和輸出**頁面上，重新命名預設輸出更具描述性的名稱，例如**MyAddressOutput**。 加入和設定兩個輸出資料行**AddressID**和**縣 （市)**。  
  
5.  在**連接管理員**頁面上，加入或建立一般檔案連接管理員 中，使用描述性名稱，例如**MyFlatFileSrcConnectionManager**。  
  
6.  在**指令碼**頁面上，按一下**編輯指令碼**並輸入以下指令碼。 然後關閉 指令碼開發環境和**指令碼轉換編輯器**。  
  
7.  建立和設定目的地元件，例如[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]目的地、 或中所示範的範例目的地元件[與指令碼元件建立目的地](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)。 然後將來源元件連接到目的地  (不需要任何轉換，就可以直接將來源連接到目的地)。您可以執行下列命令，以建立目的地資料表[!INCLUDE[tsql](../../includes/tsql-md.md)]命令**AdventureWorks**資料庫：  
  
    ```sql
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
  
## <a name="see-also"></a>另請參閱  
 [使用指令碼元件建立目的地](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)   
 [開發自訂來源元件](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-source-component.md)  
  
  

