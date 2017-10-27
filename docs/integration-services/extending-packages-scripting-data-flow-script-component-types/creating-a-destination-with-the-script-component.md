---
title: "使用指令碼元件建立目的地 |Microsoft 文件"
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
- Script component [Integration Services], destination components
- destinations [Integration Services], components
- input columns [Integration Services]
ms.assetid: 214e22e8-7e7d-4876-b690-c138e5721b81
caps.latest.revision: 57
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 7680aac73590f92eadd615b9d164967e61877664
ms.contentlocale: zh-tw
ms.lasthandoff: 09/26/2017

---
# <a name="creating-a-destination-with-the-script-component"></a>以指令碼元件建立目的地
  您可以在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝的資料流程中使用目的地元件，以便將從上游來源和轉換收到的資料儲存至資料來源。 通常，目的地元件會透過現有的連接管理員連接到資料來源。  
  
 如需指令碼元件的概觀，請參閱[Extending the Data Flow with Script Component](../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md)。  
  
 指令碼元件以及它為您產生的基礎結構程式碼，可大幅簡化開發自訂資料流程元件的程序。 不過，若要了解指令碼元件如何運作，您可能會發現閱讀開發自訂資料流程元件中的步驟[開發自訂資料流程元件](../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md) 區段中，並且特別[開發自訂目的地元件](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-destination-component.md)。  
  
## <a name="getting-started-with-a-destination-component"></a>開始使用目的地元件  
 當您將指令碼元件加入至 [資料流程] 索引標籤的[!INCLUDE[ssIS](../../includes/ssis-md.md)]設計工具中，**選取指令碼元件類型**對話方塊會開啟，並提示您選取**來源**，**目的地**，或**轉換**指令碼。 在此對話方塊中，選取**目的地**。  
  
 接著，請將轉換的輸出連接至 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師中的目的地元件。 進行測試時，您不需要任何轉換，就可以直接將來源連接至目的地。  
  
## <a name="configuring-a-destination-component-in-metadata-design-mode"></a>在中繼資料設計模式中設定目的地元件  
 您選取選項以建立目的地元件之後，您會設定元件利用**指令碼轉換編輯器**。 如需詳細資訊，請參閱[設定指令碼元件指令碼元件編輯器中](../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md)。  
  
 若要選取指令碼目的地將使用的指令碼語言，您將設定**ScriptLanguage**屬性**指令碼**頁面**指令碼轉換編輯器**對話方塊。  
  
> [!NOTE]  
>  若要設定預設的指令碼語言指令碼元件，請使用**指令碼語言**選項**一般**頁面**選項** 對話方塊。 如需相關資訊，請參閱 [General Page](https://msdn.microsoft.com/library/ms189436(v=sql.110).aspx)。  
  
 資料流程目的地元件有一個輸入，但是沒有任何輸出。 設定元件是其中一個步驟，您必須使用中繼資料設計模式中，在完成輸入**指令碼轉換編輯器**，然後才能在您撰寫自訂指令碼。  
  
### <a name="adding-connection-managers"></a>加入連接管理員  
 通常，目的地元件會使用現有的連接管理員來連接至它用來儲存資料流程之資料的資料來源。 在**連接管理員**頁面**指令碼轉換編輯器**，按一下 **新增**新增適當的連接管理員。  
  
 不過，連接管理員只是一種便利的單位，用以封裝和儲存連接至特定類型的資料來源所需的資訊。 您必須撰寫自己的自訂程式碼來載入或儲存資料，以及 (可能的話) 開啟和關閉資料來源的連接。  
  
 如需如何透過指令碼元件使用連接管理員的一般資訊，請參閱[連接到指令碼元件中的資料來源](../../integration-services/extending-packages-scripting/data-flow-script-component/connecting-to-data-sources-in-the-script-component.md)。  
  
 如需有關**連接管理員**頁面**指令碼轉換編輯器**，請參閱[指令碼轉換編輯器 &#40;連接管理員頁面 &#41;](../../integration-services/data-flow/transformations/script-transformation-editor-connection-managers-page.md).  
  
### <a name="configuring-inputs-and-input-columns"></a>設定輸入和輸入資料行  
 目的地元件有一個輸入，但是沒有任何輸出。  
  
 在**的輸入資料行**頁面**指令碼轉換編輯器**，資料行清單顯示可用的資料行的上游元件輸出從資料流程中的資料。 請選取您想要儲存的資料行。  
  
 如需有關**的輸入資料行**頁面**指令碼轉換編輯器**，請參閱[指令碼轉換編輯器 &#40; 輸入資料行頁面 &#41;](../../integration-services/data-flow/transformations/script-transformation-editor-input-columns-page.md)。  
  
 **輸入和輸出**頁面**指令碼轉換編輯器**顯示單一輸入，您可以重新命名。 您將使用在自動產生程式碼中建立的存取子屬性，依據指令碼中的名稱來參考輸入。  
  
 如需有關**輸入和輸出**頁面**指令碼轉換編輯器**，請參閱[指令碼轉換編輯器 &#40; 輸入及輸出頁面 &#41;](../../integration-services/data-flow/transformations/script-transformation-editor-inputs-and-outputs-page.md)。  
  
### <a name="adding-variables"></a>加入變數  
 如果您想要在您的指令碼中使用現有的變數，您可以將其加入**[readonlyvariables]**和**[readwritevariables]**屬性欄位上**指令碼**頁面**指令碼轉換編輯器**。  
  
 當您在屬性欄位中加入多個變數時，請用逗號分隔變數名稱。 您也可以選取多個變數，依序按一下省略符號 (**...**) 旁邊**readonlyvariables**和**readwritevariables**屬性欄位，然後選取 在變數**選取變數**對話方塊。  
  
 如需如何使用指令碼元件中使用變數的一般資訊，請參閱[在指令碼元件中使用變數](../../integration-services/extending-packages-scripting/data-flow-script-component/using-variables-in-the-script-component.md)。  
  
 如需有關**指令碼**頁面**指令碼轉換編輯器**，請參閱[指令碼轉換編輯器 &#40;指令碼頁面 &#41;](../../integration-services/data-flow/transformations/script-transformation-editor-script-page.md).  
  
## <a name="scripting-a-destination-component-in-code-design-mode"></a>在程式碼設計模式中編寫目的地元件的指令碼  
 在您設定好元件的中繼資料之後，便可撰寫自訂指令碼。 在**指令碼轉換編輯器**上**指令碼**頁面上，按一下**編輯指令碼**開啟[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA) IDE您可以在其中加入自訂指令碼。 您使用的指令碼語言，取決於您選取[!INCLUDE[msCoName](../../includes/msconame-md.md)]Visual Basic 或[!INCLUDE[msCoName](../../includes/msconame-md.md)]Visual C# 做為指令碼語言**ScriptLanguage**屬性**指令碼**頁面。  
  
 適用於所有類型的元件所使用的指令碼元件建立的重要資訊，請參閱[編碼和偵錯指令碼元件](../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md)。  
  
### <a name="understanding-the-auto-generated-code"></a>了解自動產生的程式碼  
 當您開啟 VSTA IDE 之後您建立, 和設定目的地元件，可編輯**ScriptMain**類別會出現在虛設常式的程式碼編輯器**ProcessInputRow**方法。 **ScriptMain**類別是您將在其中撰寫自訂程式碼和**ProcessInputRow**是目的地元件中最重要的方法。  
  
 如果您開啟**Project Explorer**視窗在 VSTA 中的，您可以看到，指令碼元件也會產生唯讀**BufferWrapper**和**ComponentWrapper**專案項目。 **ScriptMain**類別繼承自**UserComponent**類別**ComponentWrapper**專案項目。  
  
 在執行階段，資料流程引擎會叫用**ProcessInput**方法中的**UserComponent**類別，它會覆寫<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ProcessInput%2A>方法<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent>父類別。 **ProcessInput**方法接著執行迴圈的輸入的緩衝區和呼叫中的資料列**ProcessInputRow**方法一次，每個資料列。  
  
### <a name="writing-your-custom-code"></a>撰寫您的自訂程式碼  
 為了完成建立自訂目的地元件，您可能想要撰寫指令碼中提供下列方法**ScriptMain**類別。  
  
1.  覆寫**AcquireConnections**方法，以連接到外部資料來源。 從連接管理員擷取連接物件，或是必要的連接資訊。  
  
2.  覆寫**PreExecute**方法以準備儲存的資料。 例如，您可能想要建立及設定**SqlCommand**及其參數，在此方法。  
  
3.  使用覆寫**ProcessInputRow**方法，將每個輸入資料列複製到外部資料來源。 例如，對於[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]目的地，您可以複製的資料行值的參數到**SqlCommand**執行命令，每個資料列一次。 一般檔案目的地，您可以撰寫每個資料行值**StreamWriter**，資料行分隔符號所分隔的值。  
  
4.  覆寫**PostExecute**方法以中斷外部資料來源，如有需要，並執行任何其他必要的清除作業。  
  
## <a name="examples"></a>範例  
 請依照下列的範例將示範所需的程式碼**ScriptMain**類別以建立目的地元件。  
  
> [!NOTE]  
>  這些範例使用**Person.Address**資料表中**AdventureWorks**範例資料庫，並傳遞其第一個和第四個資料行，  **int*AddressID** * 和**nvarchar (30) 縣 （市)** ，經過資料流資料行。 在本章節中的來源、轉換和目的地範例使用相同的資料。 每個範例都會記載其他必要條件與假設。  
  
### <a name="adonet-destination-example"></a>ADO.NET 目的地範例  
 這個範例示範一個目的地元件，它使用現有[!INCLUDE[vstecado](../../includes/vstecado-md.md)]連接管理員，以將資料從資料流程中儲存[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料表。  
  
 如果您要執行這個範例程式碼，必須依下列方式設定封裝與元件：  
  
1.  建立[!INCLUDE[vstecado](../../includes/vstecado-md.md)]使用連接管理員**SqlClient**提供者連接到**AdventureWorks**資料庫。  
  
2.  執行下列命令以建立目的地資料表[!INCLUDE[tsql](../../includes/tsql-md.md)]命令**AdventureWorks**資料庫：  
  
    ```sql
    CREATE TABLE [Person].[Address2]([AddressID] [int] NOT NULL,  
        [City] [nvarchar](30) NOT NULL)  
    ```  
  
3.  將新的指令碼元件加入至資料流程設計師介面，並將它設定為目的地。  
  
4.  將上游來源或轉換的輸出連接到 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師中的目的地元件  (不需要任何轉換，就可以直接將來源連接到目的地)。這個輸出應該會提供來自資料**Person.Address**資料表**AdventureWorks**範例資料庫包含最少為**AddressID**和**縣 （市)**資料行。  
  
5.  開啟**指令碼轉換編輯器**。 在**輸入資料行**頁面上，選取**AddressID**和**縣 （市)**輸入資料行。  
  
6.  在**輸入和輸出**頁面上，例如重新命名以更具描述性的名稱輸入**MyAddressInput**。  
  
7.  在**連接管理員**頁面上，加入或建立[!INCLUDE[vstecado](../../includes/vstecado-md.md)]連接管理員的名稱，例如**MyADONETConnectionManager**。  
  
8.  在**指令碼**頁面上，按一下**編輯指令碼**並輸入以下指令碼。 然後關閉指令碼開發環境。  
  
9. 關閉**指令碼轉換編輯器**及執行範例。  
  
```vb  
Imports System.Data.SqlClient  
...  
Public Class ScriptMain  
    Inherits UserComponent  
  
    Dim connMgr As IDTSConnectionManager100  
    Dim sqlConn As SqlConnection  
    Dim sqlCmd As SqlCommand  
    Dim sqlParam As SqlParameter  
  
    Public Overrides Sub AcquireConnections(ByVal Transaction As Object)  
  
        connMgr = Me.Connections.MyADONETConnectionManager  
        sqlConn = CType(connMgr.AcquireConnection(Nothing), SqlConnection)  
  
    End Sub  
  
    Public Overrides Sub PreExecute()  
  
        sqlCmd = New SqlCommand("INSERT INTO Person.Address2(AddressID, City) " & _  
            "VALUES(@addressid, @city)", sqlConn)  
        sqlParam = New SqlParameter("@addressid", SqlDbType.Int)  
        sqlCmd.Parameters.Add(sqlParam)  
        sqlParam = New SqlParameter("@city", SqlDbType.NVarChar, 30)  
        sqlCmd.Parameters.Add(sqlParam)  
  
    End Sub  
  
    Public Overrides Sub MyAddressInput_ProcessInputRow(ByVal Row As MyAddressInputBuffer)  
        With sqlCmd  
            .Parameters("@addressid").Value = Row.AddressID  
            .Parameters("@city").Value = Row.City  
            .ExecuteNonQuery()  
        End With  
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
    SqlCommand sqlCmd;  
    SqlParameter sqlParam;  
  
    public override void AcquireConnections(object Transaction)  
    {  
  
        connMgr = this.Connections.MyADONETConnectionManager;  
        sqlConn = (SqlConnection)connMgr.AcquireConnection(null);  
  
    }  
  
    public override void PreExecute()  
    {  
  
        sqlCmd = new SqlCommand("INSERT INTO Person.Address2(AddressID, City) " +  
            "VALUES(@addressid, @city)", sqlConn);  
        sqlParam = new SqlParameter("@addressid", SqlDbType.Int);  
        sqlCmd.Parameters.Add(sqlParam);  
        sqlParam = new SqlParameter("@city", SqlDbType.NVarChar, 30);  
        sqlCmd.Parameters.Add(sqlParam);  
  
    }  
  
    public override void MyAddressInput_ProcessInputRow(MyAddressInputBuffer Row)  
    {  
        {  
            sqlCmd.Parameters["@addressid"].Value = Row.AddressID;  
            sqlCmd.Parameters["@city"].Value = Row.City;  
            sqlCmd.ExecuteNonQuery();  
        }  
    }  
  
    public override void ReleaseConnections()  
    {  
  
        connMgr.ReleaseConnection(sqlConn);  
  
    }  
  
}  
```  
  
### <a name="flat-file-destination-example"></a>一般檔案目的地範例  
 這個範例會示範一個目的地元件，它使用現有的一般檔案連接管理員，將資料流程的資料儲存至一般檔案。  
  
 如果您要執行這個範例程式碼，必須依下列方式設定封裝與元件：  
  
1.  建立連接至目的地檔案的一般檔案連接管理員。 此檔案不需要存在，因為目的地元件會建立此檔案。 將目的地檔案設定為以逗號分隔的檔案，其中包含**AddressID**和**縣 （市)**資料行。  
  
2.  將新的指令碼元件加入至資料流程設計師介面，並將它設定為目的地。  
  
3.  將上游來源或轉換的輸出連接到 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師中的目的地元件  (不需要任何轉換，就可以直接將來源連接到目的地)。這個輸出應該會提供來自資料**Person.Address**資料表**AdventureWorks**範例資料庫，而且應該包含至少**AddressID**和**縣 （市)**資料行。  
  
4.  開啟**指令碼轉換編輯器**。 在**的輸入資料行**頁面上，選取**AddressID**和**縣 （市)**資料行。  
  
5.  在**輸入和輸出**頁面上，例如重新命名為更具描述性的名稱，輸入**MyAddressInput**。  
  
6.  在**連接管理員**頁面上，加入或建立一般檔案連接管理員使用描述性的名稱這類**MyFlatFileDestConnectionManager**。  
  
7.  在**指令碼**頁面上，按一下**編輯指令碼**並輸入以下指令碼。 然後關閉指令碼開發環境。  
  
8.  關閉**指令碼轉換編輯器**及執行範例。  
  
```vb  
Imports System.IO  
...  
Public Class ScriptMain  
    Inherits UserComponent  
  
    Dim copiedAddressFile As String  
    Private textWriter As StreamWriter  
    Private columnDelimiter As String = ","  
  
    Public Overrides Sub AcquireConnections(ByVal Transaction As Object)  
  
        Dim connMgr As IDTSConnectionManager100 = _  
            Me.Connections.MyFlatFileDestConnectionManager  
        copiedAddressFile = CType(connMgr.AcquireConnection(Nothing), String)  
  
    End Sub  
  
    Public Overrides Sub PreExecute()  
  
        textWriter = New StreamWriter(copiedAddressFile, False)  
  
    End Sub  
  
    Public Overrides Sub MyAddressInput_ProcessInputRow(ByVal Row As MyAddressInputBuffer)  
  
        With textWriter  
            If Not Row.AddressID_IsNull Then  
                .Write(Row.AddressID)  
            End If  
            .Write(columnDelimiter)  
            If Not Row.City_IsNull Then  
                .Write(Row.City)  
            End If  
            .WriteLine()  
        End With  
  
    End Sub  
  
    Public Overrides Sub PostExecute()  
  
        textWriter.Close()  
  
    End Sub  
  
End Class  
```  
  
```csharp  
using System.IO;  
public class ScriptMain:  
    UserComponent  
  
{  
    string copiedAddressFile;  
    private StreamWriter textWriter;  
    private string columnDelimiter = ",";  
  
    public override void AcquireConnections(object Transaction)  
    {  
  
        IDTSConnectionManager100 connMgr = this.Connections.MyFlatFileDestConnectionManager;  
        copiedAddressFile = (string) connMgr.AcquireConnection(null);  
  
    }  
  
    public override void PreExecute()  
    {  
  
        textWriter = new StreamWriter(copiedAddressFile, false);  
  
    }  
  
    public override void MyAddressInput_ProcessInputRow(MyAddressInputBuffer Row)  
    {  
  
        {  
            if (!Row.AddressID_IsNull)  
            {  
                textWriter.Write(Row.AddressID);  
            }  
            textWriter.Write(columnDelimiter);  
            if (!Row.City_IsNull)  
            {  
                textWriter.Write(Row.City);  
            }  
            textWriter.WriteLine();  
        }  
  
    }  
  
    public override void PostExecute()  
    {  
  
        textWriter.Close();  
  
    }  
  
}  
```  
  
## <a name="see-also"></a>另請參閱  
 [使用指令碼元件建立來源](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-source-with-the-script-component.md)   
 [開發自訂目的地元件](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-destination-component.md)  
  
  
