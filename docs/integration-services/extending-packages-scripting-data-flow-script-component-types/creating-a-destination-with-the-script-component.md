---
title: 使用指令碼元件建立目的地 | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: extending-packages-scripting-data-flow-script-component-types
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
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
manager: craigg
ms.openlocfilehash: a6fadd30e1db32354c52fcef92b249765948c667
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/16/2018
ms.locfileid: "40410987"
---
# <a name="creating-a-destination-with-the-script-component"></a>以指令碼元件建立目的地
  您可以在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝的資料流程中使用目的地元件，以便將從上游來源和轉換收到的資料儲存至資料來源。 通常，目的地元件會透過現有的連接管理員連接到資料來源。  
  
 如需指令碼元件的概觀，請參閱[使用指令碼元件擴充資料流程](../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md)。  
  
 指令碼元件以及它為您產生的基礎結構程式碼，可大幅簡化開發自訂資料流程元件的程序。 不過，若要了解指令碼元件運作方式，建議您詳細閱讀[開發自訂資料流程元件](../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)一節中開發自訂資料流程元件的步驟，尤其是[開發自訂目的地元件](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-destination-component.md)。  
  
## <a name="getting-started-with-a-destination-component"></a>開始使用目的地元件  
 當您將指令碼元件新增至 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計工具的 [資料流程] 索引標籤時，就會開啟 [選取指令碼元件類型] 對話方塊，並提示您選取 [來源]、[目的地] 或 [轉換] 指令碼。 在這個對話方塊中，請選取 [目的地]。  
  
 接著，請將轉換的輸出連接至 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師中的目的地元件。 進行測試時，您不需要任何轉換，就可以直接將來源連接至目的地。  
  
## <a name="configuring-a-destination-component-in-metadata-design-mode"></a>在中繼資料設計模式中設定目的地元件  
 在選取選項以建立目的地元件之後，您可以使用 [指令碼轉換編輯器] 來設定元件。 如需詳細資訊，請參閱[在指令碼元件編輯器中設定指令碼元件](../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md)。  
  
 若要選取指令碼目的地將使用的指令碼語言，請在 [指令碼轉換編輯器] 對話方塊的 [指令碼] 頁面上，設定 **ScriptLanguage** 屬性。  
  
> [!NOTE]  
>  若要為指令碼元件設定預設的指令碼語言，請使用 [選項] 對話方塊中 [一般] 頁面上的 [指令碼語言] 選項。 如需相關資訊，請參閱 [General Page](../general-page-of-integration-services-designers-options.md)。  
  
 資料流程目的地元件有一個輸入，但是沒有任何輸出。 設定元件的輸入是您必須在中繼資料設計模式下完成的其中一個步驟，方法是在撰寫自訂指令碼之前先使用 [指令碼轉換編輯器]。  
  
### <a name="adding-connection-managers"></a>加入連接管理員  
 通常，目的地元件會使用現有的連接管理員來連接至它用來儲存資料流程之資料的資料來源。 在 [指令碼轉換編輯器] 的 [連線管理員] 頁面上，按一下 [新增] 新增適當的連線管理員。  
  
 不過，連接管理員只是一種便利的單位，用以封裝和儲存連接至特定類型的資料來源所需的資訊。 您必須撰寫自己的自訂程式碼來載入或儲存資料，以及 (可能的話) 開啟和關閉資料來源的連接。  
  
 如需如何利用指令碼元件以使用連線管理員的一般資訊，請參閱[在指令碼元件中連線至資料來源](../../integration-services/extending-packages-scripting/data-flow-script-component/connecting-to-data-sources-in-the-script-component.md)。  
  
 如需 [指令碼轉換編輯器] 之 [連線管理員] 頁面的詳細資訊，請參閱[指令碼轉換編輯器 &#40;連線管理員頁面&#41;](../../integration-services/data-flow/transformations/script-transformation-editor-connection-managers-page.md)。  
  
### <a name="configuring-inputs-and-input-columns"></a>設定輸入和輸入資料行  
 目的地元件有一個輸入，但是沒有任何輸出。  
  
 在 [指令碼轉換編輯器] 的 [輸入資料行] 頁面上，資料行清單會從資料流程中的上游元件輸出顯示可用的資料行。 請選取您想要儲存的資料行。  
  
 如需 [指令碼轉換編輯器] 的 [輸入資料行] 頁面的詳細資訊，請參閱[指令碼轉換編輯器 &#40;輸入資料行頁面&#41;](../../integration-services/data-flow/transformations/script-transformation-editor-input-columns-page.md)。  
  
 [指令碼轉換編輯器] 的 [輸入及輸出] 頁面會顯示您可以重新命名的單一輸入。 您將使用在自動產生程式碼中建立的存取子屬性，依據指令碼中的名稱來參考輸入。  
  
 如需 [指令碼轉換編輯器] 之 [輸入及輸出] 頁面的詳細資訊，請參閱[指令碼轉換編輯器 &#40;輸入及輸出頁面&#41;](../../integration-services/data-flow/transformations/script-transformation-editor-inputs-and-outputs-page.md)。  
  
### <a name="adding-variables"></a>加入變數  
 如果您想要在指令碼中使用現有的變數，可以在 [指令碼轉換編輯器] 的 [指令碼] 頁面上，將它們新增至 **ReadOnlyVariables** 和 **ReadWriteVariables** 屬性欄位中。  
  
 當您在屬性欄位中加入多個變數時，請用逗號分隔變數名稱。 您也可以按一下 **ReadOnlyVariables** 和 **ReadWriteVariables** 屬性欄位旁邊的省略符號 (**...**) 按鈕，然後在 [選取變數] 對話方塊中選取變數，來選取多個變數。  
  
 如需如何利用指令碼元件使用變數的一般資訊，請參閱[在指令碼元件中使用變數](../../integration-services/extending-packages-scripting/data-flow-script-component/using-variables-in-the-script-component.md)。  
  
 如需 [指令碼轉換編輯器] 的 [指令碼] 頁面的詳細資訊，請參閱[指令碼轉換編輯器 &#40;指令碼頁面&#41;](../../integration-services/data-flow/transformations/script-transformation-editor-script-page.md)。  
  
## <a name="scripting-a-destination-component-in-code-design-mode"></a>在程式碼設計模式中編寫目的地元件的指令碼  
 在您設定好元件的中繼資料之後，便可撰寫自訂指令碼。 在 [指令碼轉換編輯器] 的 [指令碼] 頁面上，按一下 [編輯指令碼]，開啟 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA) IDE 以新增自訂指令碼。 所使用的指令碼語言取決於您選取 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic 還是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C# 作為 [指令碼] 頁面上 **ScriptLanguage** 屬性的指令碼語言。  
  
 如需使用指令碼元件所建立之各種元件都適用的重要資訊，請參閱[編碼和偵錯指令碼元件](../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md)。  
  
### <a name="understanding-the-auto-generated-code"></a>了解自動產生的程式碼  
 當您在建立和設定目的地元件之後開啟 VSTA IDE 時，可編輯的 **ScriptMain** 類別會出現在程式碼編輯器中，並具有 **ProcessInputRow** 方法的虛設常式。 **ScriptMain** 類別是您將撰寫自訂程式碼的地方，而 **ProcessInputRow** 則是目的地元件中最重要的方法。  
  
 如果您在 VSTA 中開啟 [專案總管] 視窗，則可以看到指令碼元件也會產生唯讀的 **BufferWrapper** 和 **ComponentWrapper** 專案項目。 **ScriptMain** 類別繼承自 **ComponentWrapper** 專案項目中的 **UserComponent** 類別。  
  
 在執行階段，資料流程引擎會叫用 **UserComponent** 類別中的 **ProcessInput** 方法，它會覆寫 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> 父類別的 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ProcessInput%2A> 方法。 **ProcessInput** 方法接著會在輸入緩衝區的資料列中執行迴圈，並為每個資料列呼叫一次 **ProcessInputRow** 方法。  
  
### <a name="writing-your-custom-code"></a>撰寫您的自訂程式碼  
 為了完成建立自訂目的地元件，您可能會想要以 **ScriptMain** 類別中提供的下列方法來撰寫指令碼。  
  
1.  覆寫 **AcquireConnections** 方法以連線至外部資料來源。 從連接管理員擷取連接物件，或是必要的連接資訊。  
  
2.  覆寫 **PreExecute** 方法以準備儲存資料。 例如，您可能會想要在這個方法中建立並設定 **SqlCommand** 和其參數。  
  
3.  使用覆寫的 **ProcessInputRow** 方法，將每個輸入資料列複製至外部資料來源。 例如，若為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目的地，您可以將資料行值複製至 **SqlCommand** 的參數中，然後針對每個資料列執行此命令一次。 若為一般檔案目的地，您可以將每個資料列的值寫入 **StreamWriter**，並以資料行分隔符號隔開這些值。  
  
4.  覆寫 **PostExecute** 方法以中斷外部資料來源的連線 (若有需要的話)，以及執行任何其他所需的清除作業。  
  
## <a name="examples"></a>範例  
 下列範例示範 **ScriptMain** 類別中建立目的地元件所需的程式碼。  
  
> [!NOTE]  
>  這些範例使用 **AdventureWorks** 範例資料庫中的 **Person.Address** 資料表，並透過資料流程傳遞其第一個和第四個資料行：**int*AddressID*** 和 **nvarchar(30)City** 資料行。 在本章節中的來源、轉換和目的地範例使用相同的資料。 每個範例都會記載其他必要條件與假設。  
  
### <a name="adonet-destination-example"></a>ADO.NET 目的地範例  
 這個範例會示範一個目的地元件，它使用現有的 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 連線管理員，將資料流程的資料儲存至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表。  
  
 如果您要執行這個範例程式碼，必須依下列方式設定封裝與元件：  
  
1.  建立 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 連線管理員，以使用 **SqlClient** 提供者連線至 **AdventureWorks** 資料庫。  
  
2.  您可以在 **AdventureWorks** 資料庫中執行下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 命令，以建立目的地資料表：  
  
    ```sql
    CREATE TABLE [Person].[Address2]([AddressID] [int] NOT NULL,  
        [City] [nvarchar](30) NOT NULL)  
    ```  
  
3.  將新的指令碼元件加入至資料流程設計師介面，並將它設定為目的地。  
  
4.  將上游來源或轉換的輸出連接到 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師中的目的地元件  (不需要任何轉換，就可以直接將來源連接到目的地)。這個輸出應該從 **AdventureWorks** 範例資料庫的 **Person.Address** 資料表中提供資料，這個資料表至少包含 **AddressID** 和 **City** 資料行。  
  
5.  開啟**指令碼轉換編輯器**。 在 [輸入資料行] 頁面上，選取 **AddressID** 和 **City** 輸入資料行。  
  
6.  在 [輸入及輸出] 頁面上，以更具描述性的名稱重新命名輸入，例如 **MyAddressInput**。  
  
7.  在 [連線管理員] 頁面上，使用名稱 (例如 **MyADONETConnectionManager**) 來新增或建立 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 連線管理員。  
  
8.  在 [指令碼] 頁面上，按一下 [編輯指令碼]，並輸入以下指令碼。 然後關閉指令碼開發環境。  
  
9. 關閉 [指令碼轉換編輯器] 並執行該範例。  
  
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
  
1.  建立連接至目的地檔案的一般檔案連接管理員。 此檔案不需要存在，因為目的地元件會建立此檔案。 將目的地檔案設定為包含 **AddressID** 和 **City** 資料行的逗號分隔檔案。  
  
2.  將新的指令碼元件加入至資料流程設計師介面，並將它設定為目的地。  
  
3.  將上游來源或轉換的輸出連接到 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師中的目的地元件  (不需要任何轉換，就可以直接將來源連接到目的地)。這個輸出應該從 **AdventureWorks** 範例資料庫的 **Person.Address** 資料表中提供資料，而且應該至少包含 **AddressID** 和 **City** 資料行。  
  
4.  開啟**指令碼轉換編輯器**。 在 [輸入資料行] 頁面上，選取 **AddressID** 和 **City** 資料行。  
  
5.  在 [輸入及輸出] 頁面上，以更具描述性的名稱重新命名輸入，例如 **MyAddressInput**。  
  
6.  在 [連線管理員] 頁面上，使用描述性的名稱 (例如 **MyFlatFileDestConnectionManager**) 來新增或建立一般檔案連線管理員。  
  
7.  在 [指令碼] 頁面上，按一下 [編輯指令碼]，並輸入以下指令碼。 然後關閉指令碼開發環境。  
  
8.  關閉 [指令碼轉換編輯器] 並執行該範例。  
  
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
 [以指令碼元件建立來源](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-source-with-the-script-component.md)   
 [開發自訂目的地元件](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-destination-component.md)  
  
  
