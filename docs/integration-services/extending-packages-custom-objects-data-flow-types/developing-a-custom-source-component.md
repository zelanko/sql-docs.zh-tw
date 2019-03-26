---
title: 開發自訂來源元件 | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- validation [Integration Services], components
- external data sources [Integration Services]
- data flow components [Integration Services], source components
- output columns [Integration Services]
- custom data flow components [Integration Services], source components
- custom sources [Integration Services]
- source components [Integration Services]
ms.assetid: 4dc0f631-8fd6-4007-b573-ca67f58ca068
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 169b815d9cbf09c2fc4ccf24e5585f4c2c8e5d56
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/20/2019
ms.locfileid: "58275756"
---
# <a name="developing-a-custom-source-component"></a>開發自訂來源元件
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 提供開發人員撰寫來源元件的能力，這些元件可以連線至自訂資料來源，並將那些來源的資料提供給資料流程工作中的其他元件。 當您必須連接至無法使用其中一個現有 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 來源存取的資料來源時，能夠建立自訂來源的能力是很重要的。  
  
 來源元件具有一或多個輸出與零輸入。 在設計階段，來源元件是用以建立和設定連接、從外部資料來源讀取資料行中繼資料，以及設定以外部資料來源為基礎之來源的輸出資料行。 在執行期間，它們會連接至外部資料來源並將資料列加入輸出緩衝區。 資料流程工作會將這個緩衝區的資料列提供給下游元件。  
  
 如需資料流程元件開發的一般概觀，請參閱[開發自訂資料流程元件](../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)。  
  
## <a name="design-time"></a>設計階段  
 實作來源元件的設計階段功能需要指定連至外部資料來源的連接、加入和設定反映資料來源的輸出資料行，以及驗證元件是否已就緒可執行。 依定義，來源元件具有零個輸入以及一或多個非同步輸出。  
  
### <a name="creating-the-component"></a>建立元件  
 來源元件使用在封裝中定義的 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 物件，連接至外部資料來源。 它們將元素加入 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.RuntimeConnectionCollection%2A> 屬性的 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ComponentMetaData%2A> 集合，以指出其連接管理員需求。 這個集合有兩個目的：用以儲存元件所使用的封裝中的連接管理員參考，以及用以向設計工具通告連接管理員的需求。 將 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSRuntimeConnection100> 新增至集合時，[進階編輯器] 會顯示 [連線屬性] 索引標籤，這可讓使用者在套件中選取或是建立連線。  
  
 下列程式碼範例顯示 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProvideComponentProperties%2A> 的實作，它加入輸出並將 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSRuntimeConnection100> 物件加入 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.RuntimeConnectionCollection%2A>。  
  
```csharp  
using System;  
using System.Collections;  
using System.Data;  
using System.Data.SqlClient;  
using System.Data.OleDb;  
using Microsoft.SqlServer.Dts.Runtime;  
using Microsoft.SqlServer.Dts.Runtime.Wrapper;  
using Microsoft.SqlServer.Dts.Pipeline;  
using Microsoft.SqlServer.Dts.Pipeline.Wrapper;  
  
namespace Microsoft.Samples.SqlServer.Dts  
{  
    [DtsPipelineComponent(DisplayName = "MySourceComponent",ComponentType = ComponentType.SourceAdapter)]  
    public class MyComponent : PipelineComponent  
    {  
        public override void ProvideComponentProperties()  
        {  
            // Reset the component.  
            base.RemoveAllInputsOutputsAndCustomProperties();  
            ComponentMetaData.RuntimeConnectionCollection.RemoveAll();  
  
            IDTSOutput100 output = ComponentMetaData.OutputCollection.New();  
            output.Name = "Output";  
  
            IDTSRuntimeConnection100 connection = ComponentMetaData.RuntimeConnectionCollection.New();  
            connection.Name = "ADO.NET";  
        }  
```  
  
```vb  
Imports System.Data  
Imports System.Data.SqlClient  
Imports Microsoft.SqlServer.Dts.Runtime  
Imports Microsoft.SqlServer.Dts.Runtime.Wrapper  
Imports Microsoft.SqlServer.Dts.Pipeline  
Imports Microsoft.SqlServer.Dts.Pipeline.Wrapper  
  
<DtsPipelineComponent(DisplayName:="MySourceComponent", ComponentType:=ComponentType.SourceAdapter)> _  
Public Class MySourceComponent  
    Inherits PipelineComponent  
  
    Public Overrides Sub ProvideComponentProperties()  
  
        ' Allow for resetting the component.  
        RemoveAllInputsOutputsAndCustomProperties()  
        ComponentMetaData.RuntimeConnectionCollection.RemoveAll()  
  
        Dim output As IDTSOutput100 = ComponentMetaData.OutputCollection.New()  
        output.Name = "Output"  
  
        Dim connection As IDTSRuntimeConnection100 = ComponentMetaData.RuntimeConnectionCollection.New()  
        connection.Name = "ADO.NET"  
  
    End Sub  
End Class  
```  
  
### <a name="connecting-to-an-external-data-source"></a>連接到外部資料來源  
 在將連接加入 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.RuntimeConnectionCollection%2A> 之後，就可覆寫 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.AcquireConnections%2A> 方法以建立連至外部資料來源的連接。 會在設計與執行階段呼叫此方法。 元件應該建立一個連接，以連至執行階段連接所指定的連接管理員，之後再建立連至外部資料來源的連接。  
  
 在建立連接之後，元件應該會在內部快取它，並在呼叫 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ReleaseConnections%2A> 方法時釋放。 會在設計階段與執行階段呼叫 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ReleaseConnections%2A> 方法，就像呼叫 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.AcquireConnections%2A> 方法一樣。 開發人員會覆寫這個方法，並在 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.AcquireConnections%2A> 期間釋放元件建立的連接。  
  
 下列程式碼範例顯示連接到 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.AcquireConnections%2A> 方法中的 ADO.NET 連接，並關閉 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ReleaseConnections%2A> 方法中的連接。  
  
```csharp  
private SqlConnection sqlConnection;  
  
public override void AcquireConnections(object transaction)  
{  
    if (ComponentMetaData.RuntimeConnectionCollection[0].ConnectionManager != null)  
    {  
        ConnectionManager cm = Microsoft.SqlServer.Dts.Runtime.DtsConvert.GetWrapper(ComponentMetaData.RuntimeConnectionCollection[0].ConnectionManager);  
        ConnectionManagerAdoNet cmado = cm.InnerObject as ConnectionManagerAdoNet;  
  
        if (cmado == null)  
            throw new Exception("The ConnectionManager " + cm.Name + " is not an ADO.NET connection.");  
  
        sqlConnection = cmado.AcquireConnection(transaction) as SqlConnection;  
        sqlConnection.Open();  
    }  
}  
  
public override void ReleaseConnections()  
{  
    if (sqlConnection != null && sqlConnection.State != ConnectionState.Closed)  
        sqlConnection.Close();  
}  
```  
  
```vb  
Private sqlConnection As SqlConnection  
  
Public Overrides Sub AcquireConnections(ByVal transaction As Object)  
  
    If Not IsNothing(ComponentMetaData.RuntimeConnectionCollection(0).ConnectionManager) Then  
  
        Dim cm As ConnectionManager = Microsoft.SqlServer.Dts.Runtime.DtsConvert.GetWrapper(ComponentMetaData.RuntimeConnectionCollection(0).ConnectionManager)  
        Dim cmado As ConnectionManagerAdoNet = CType(cm.InnerObject, ConnectionManagerAdoNet)  
  
        If IsNothing(cmado) Then  
            Throw New Exception("The ConnectionManager " + cm.Name + " is not an ADO.NET connection.")  
        End If  
  
        sqlConnection = CType(cmado.AcquireConnection(transaction), SqlConnection)  
        sqlConnection.Open()  
  
    End If  
End Sub  
  
Public Overrides Sub ReleaseConnections()  
  
    If Not IsNothing(sqlConnection) And sqlConnection.State <> ConnectionState.Closed Then  
        sqlConnection.Close()  
    End If  
  
End Sub  
```  
  
### <a name="creating-and-configuring-output-columns"></a>建立和設定輸出資料行  
 來源元件的輸出資料行會反映元件在執行期間，加入資料流程的外部資料來源之資料行。 在設計階段，您在設定元件以連接至外部資料來源之後，加入輸出資料行。 元件將資料行加入其輸出集合的設計階段方法，有可能因元件的需求而有所不同，雖然在 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.Validate%2A> 或 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.AcquireConnections%2A> 期間不應該加入它們。 例如，在控制元件資料集之自訂屬性中包含 SQL 陳述式的元件，可能會在 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.SetComponentProperty%2A> 方法期間加入其輸出資料行。 元件會檢查它是否有快取的連接，而且如果有話，就會連接到資料來源並產生其輸出資料行。  
  
 在建立輸出資料行之後，請呼叫 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100.SetDataTypeProperties%2A> 方法設定其資料類型屬性。 這個方法是必要的，因為 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100.DataType%2A>、<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100.Length%2A>、<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100.Precision%2A> 和 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100.CodePage%2A> 屬性是唯讀的，而且每個屬性都與另一個屬性的設定相依。 這個方法會強制以一致的方式設定這些值的需求，而且資料流程工作會驗證它們是否已正確設定。  
  
 資料行的 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100.DataType%2A> 會決定為其他屬性設定的值。 下表顯示每個 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100.DataType%2A> 的相依屬性之需求。 未列出的資料類型會將其相依屬性設定為零。  
  
|DataType|長度|小數位數|有效位數|CodePage|  
|--------------|------------|-----------|---------------|--------------|  
|DT_DECIMAL|0|大於 0，且小於或等於 28。|0|0|  
|DT_CY|0|0|0|0|  
|DT_NUMERIC|0|大於 0、小於或等於 28，且小於有效位數 (Precision)。|大於或等於 1，且小於或等於 38。|0|  
|DT_BYTES|大於 0。|0|0|0|  
|DT_STR|大於 0 且小於 8000。|0|0|非 0，並為有效的字碼頁。|  
|DT_WSTR|大於 0，且小於 4000。|0|0|0|  
  
 由於資料類型屬性的限制會以輸出資料行的資料類型為準，因此在使用 Managed 類型時，必須選擇正確的 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 資料類型。 基底類別提供三種 Helper 方法：<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ConvertBufferDataTypeToFitManaged%2A>、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.BufferTypeToDataRecordType%2A> 和 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.DataRecordTypeToBufferType%2A>，以協助受控元件開發人員在提供受控類型時，選取 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 資料類型。 這些方法會將 Managed 資料類型轉換為 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 資料類型，反之亦然。  
  
 下列程式碼範例顯示元件的輸出資料行集合如何根據表格的結構描述擴展。 基底類別的 Helper 方法是用以設定資料行的資料類型，而相依的屬性則會根據資料類型來設定。  
  
```csharp  
SqlCommand sqlCommand;  
  
private void CreateColumnsFromDataTable()  
{  
    // Get the output.  
    IDTSOutput100 output = ComponentMetaData.OutputCollection[0];  
  
    // Start clean, and remove the columns from both collections.  
    output.OutputColumnCollection.RemoveAll();  
    output.ExternalMetadataColumnCollection.RemoveAll();  
  
    this.sqlCommand = sqlConnection.CreateCommand();  
    this.sqlCommand.CommandType = CommandType.Text;  
    this.sqlCommand.CommandText = (string)ComponentMetaData.CustomPropertyCollection["SqlStatement"].Value;  
    SqlDataReader schemaReader = this.sqlCommand.ExecuteReader(CommandBehavior.SchemaOnly);  
    DataTable dataTable = schemaReader.GetSchemaTable();  
  
    // Walk the columns in the schema,   
    // and for each data column create an output column and an external metadata column.  
    foreach (DataRow row in dataTable.Rows)  
    {  
        IDTSOutputColumn100 outColumn = output.OutputColumnCollection.New();  
        IDTSExternalMetadataColumn100 exColumn = output.ExternalMetadataColumnCollection.New();  
  
        // Set column data type properties.  
        bool isLong = false;  
        DataType dt = DataRecordTypeToBufferType((Type)row["DataType"]);  
        dt = ConvertBufferDataTypeToFitManaged(dt, ref isLong);  
        int length = 0;  
        int precision = (short)row["NumericPrecision"];  
        int scale = (short)row["NumericScale"];  
        int codepage = dataTable.Locale.TextInfo.ANSICodePage;  
  
        switch (dt)  
        {  
            // The length cannot be zero, and the code page property must contain a valid code page.  
            case DataType.DT_STR:  
            case DataType.DT_TEXT:  
                length = precision;  
                precision = 0;  
                scale = 0;  
                break;  
  
            case DataType.DT_WSTR:  
                length = precision;  
                codepage = 0;  
                scale = 0;  
                precision = 0;  
                break;  
  
            case DataType.DT_BYTES:  
                precision = 0;  
                scale = 0;  
                codepage = 0;  
                break;  
  
            case DataType.DT_NUMERIC:  
                length = 0;  
                codepage = 0;  
  
                if (precision > 38)  
                    precision = 38;  
  
                if (scale > 6)  
                    scale = 6;  
                break;  
  
            case DataType.DT_DECIMAL:  
                length = 0;  
                precision = 0;  
                codepage = 0;  
                break;  
  
            default:  
                length = 0;  
                precision = 0;  
                codepage = 0;  
                scale = 0;  
                break;  
  
        }  
  
        // Set the properties of the output column.  
        outColumn.Name = (string)row["ColumnName"];  
        outColumn.SetDataTypeProperties(dt, length, precision, scale, codepage);  
    }  
}  
```  
  
```vb  
Private sqlCommand As SqlCommand  
  
Private Sub CreateColumnsFromDataTable()  
  
    ' Get the output.  
    Dim output As IDTSOutput100 = ComponentMetaData.OutputCollection(0)  
  
    ' Start clean, and remove the columns from both collections.  
    output.OutputColumnCollection.RemoveAll()  
    output.ExternalMetadataColumnCollection.RemoveAll()  
  
    Me.sqlCommand = sqlConnection.CreateCommand()  
    Me.sqlCommand.CommandType = CommandType.Text  
    Me.sqlCommand.CommandText = CStr(ComponentMetaData.CustomPropertyCollection("SqlStatement").Value)  
  
    Dim schemaReader As SqlDataReader = Me.sqlCommand.ExecuteReader(CommandBehavior.SchemaOnly)  
    Dim dataTable As DataTable = schemaReader.GetSchemaTable()  
  
    ' Walk the columns in the schema,   
    ' and for each data column create an output column and an external metadata column.  
    For Each row As DataRow In dataTable.Rows  
  
        Dim outColumn As IDTSOutputColumn100 = output.OutputColumnCollection.New()  
        Dim exColumn As IDTSExternalMetadataColumn100 = output.ExternalMetadataColumnCollection.New()  
  
        ' Set column data type properties.  
        Dim isLong As Boolean = False  
        Dim dt As DataType = DataRecordTypeToBufferType(CType(row("DataType"), Type))  
        dt = ConvertBufferDataTypeToFitManaged(dt, isLong)  
        Dim length As Integer = 0  
        Dim precision As Integer = CType(row("NumericPrecision"), Short)  
        Dim scale As Integer = CType(row("NumericScale"), Short)  
        Dim codepage As Integer = dataTable.Locale.TextInfo.ANSICodePage  
  
        Select Case dt  
  
            ' The length cannot be zero, and the code page property must contain a valid code page.  
            Case DataType.DT_STR  
            Case DataType.DT_TEXT  
                length = precision  
                precision = 0  
                scale = 0  
  
            Case DataType.DT_WSTR  
                length = precision  
                codepage = 0  
                scale = 0  
                precision = 0  
  
            Case DataType.DT_BYTES  
                precision = 0  
                scale = 0  
                codepage = 0  
  
            Case DataType.DT_NUMERIC  
                length = 0  
                codepage = 0  
  
                If precision > 38 Then  
                    precision = 38  
                End If  
  
                If scale > 6 Then  
                    scale = 6  
                End If  
  
            Case DataType.DT_DECIMAL  
                length = 0  
                precision = 0  
                codepage = 0  
  
            Case Else  
                length = 0  
                precision = 0  
                codepage = 0  
                scale = 0  
        End Select  
  
        ' Set the properties of the output column.  
        outColumn.Name = CStr(row("ColumnName"))  
        outColumn.SetDataTypeProperties(dt, length, precision, scale, codepage)  
    Next  
End Sub  
```  
  
### <a name="validating-the-component"></a>驗證元件  
 您應該驗證來源元件，並確認輸出資料行集合中所定義的資料行，符合在外部資料來源的資料行。 有時，針對外部資料來源驗證輸出資料行是無法執行的，例如在中斷連接的狀態下，或是當最好避免長時間往返伺服器時。 在這些情況下，在輸出中的資料行仍然可以使用輸出物件的 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100.ExternalMetadataColumnCollection%2A> 來驗證。 如需詳細資訊，請參閱[驗證資料流程元件](../../integration-services/extending-packages-custom-objects/data-flow/validating-a-data-flow-component.md)。  
  
 在輸入和輸出物件上都有這個集合，而且您可以使用外部資料來源的資料行來擴展它。 當 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計工具離線時，或是當 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.ValidateExternalMetadata%2A> 屬性是 **false** 時，可以使用這個集合來驗證輸出資料行。 當建立輸出資料行時，應該同時先擴展集合。 將外部中繼資料行加入集合是相當容易的，因為外部中繼資料行應該一開始便符合輸出資料行。 資料行的資料類型屬性應該已正確地設定，而且可以將屬性直接複製到 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSExternalMetadataColumn100> 物件。  
  
 下列範例程式碼會加入以新建立的輸出資料行為基礎的外部中繼資料行。 它會假設已建立輸出資料行。  
  
```csharp  
private void CreateExternalMetaDataColumn(IDTSOutput100 output, IDTSOutputColumn100 outputColumn)  
{  
  
    // Set the properties of the external metadata column.  
    IDTSExternalMetadataColumn100 externalColumn = output.ExternalMetadataColumnCollection.New();  
    externalColumn.Name = outputColumn.Name;  
    externalColumn.Precision = outputColumn.Precision;  
    externalColumn.Length = outputColumn.Length;  
    externalColumn.DataType = outputColumn.DataType;  
    externalColumn.Scale = outputColumn.Scale;  
  
    // Map the external column to the output column.  
    outputColumn.ExternalMetadataColumnID = externalColumn.ID;  
  
}  
```  
  
```vb  
Private Sub CreateExternalMetaDataColumn(ByVal output As IDTSOutput100, ByVal outputColumn As IDTSOutputColumn100)  
  
        ' Set the properties of the external metadata column.  
        Dim externalColumn As IDTSExternalMetadataColumn100 = output.ExternalMetadataColumnCollection.New()  
        externalColumn.Name = outputColumn.Name  
        externalColumn.Precision = outputColumn.Precision  
        externalColumn.Length = outputColumn.Length  
        externalColumn.DataType = outputColumn.DataType  
        externalColumn.Scale = outputColumn.Scale  
  
        ' Map the external column to the output column.  
        outputColumn.ExternalMetadataColumnID = externalColumn.ID  
  
    End Sub  
```  
  
## <a name="run-time"></a>執行階段  
 在執行期間，元件會將資料列加入資料流程工作所建立的輸出緩衝區，並提供給在 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A> 中的元件。 只要為來源元件呼叫一次，此方法就會收到連接到下游元件的元件之每個 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100> 的輸出緩衝區。  
  
### <a name="locating-columns-in-the-buffer"></a>找出緩衝區中的資料行  
 元件的輸出緩衝區包含元件所定義的資料行，以及任何加入下游元件輸出的資料行。 例如，如果來源元件在其輸出中提供三個資料行，而下一個元件加入第四個輸出資料行，則提供給來源元件使用的輸出緩衝區包含這四個資料行。  
  
 在緩衝區資料列中的資料行順序，不是由輸出資料行集合中的輸出資料行索引所定義。 輸出資料行只有透過使用 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSBufferManagerClass.FindColumnByLineageID%2A> 的 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.BufferManager%2A> 方法，才能正確地位於緩衝區資料列中。 這個方法會在指定的緩衝區中找到具有指定歷程識別碼的資料行，並傳回它在資料列中的位置。 輸出資料行的索引通常位於 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PreExecute%2A> 方法中，並且會在 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A> 期間儲存以供使用。  
  
 下列程式碼範例會在呼叫 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PreExecute%2A> 的期間，在輸出緩衝區中尋找輸出資料行的位置，並將它們儲存在內部結構中。 資料行的名稱也會儲存在結構中，而且會用於本主題下一節的 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A> 方法之程式碼範例中。  
  
```csharp  
ArrayList columnInformation;  
  
private struct ColumnInfo  
{  
    public int BufferColumnIndex;  
    public string ColumnName;  
}  
  
public override void PreExecute()  
{  
    this.columnInformation = new ArrayList();  
    IDTSOutput100 output = ComponentMetaData.OutputCollection[0];  
  
    foreach (IDTSOutputColumn100 col in output.OutputColumnCollection)  
    {  
        ColumnInfo ci = new ColumnInfo();  
        ci.BufferColumnIndex = BufferManager.FindColumnByLineageID(output.Buffer, col.LineageID);  
        ci.ColumnName = col.Name;  
        columnInformation.Add(ci);  
    }  
}  
```  
  
```vb  
Public Overrides Sub PreExecute()  
  
    Me.columnInformation = New ArrayList()  
    Dim output As IDTSOutput100 = ComponentMetaData.OutputCollection(0)  
  
    For Each col As IDTSOutputColumn100 In output.OutputColumnCollection  
  
        Dim ci As ColumnInfo = New ColumnInfo()  
        ci.BufferColumnIndex = BufferManager.FindColumnByLineageID(output.Buffer, col.LineageID)  
        ci.ColumnName = col.Name  
        columnInformation.Add(ci)  
    Next  
End Sub  
```  
  
### <a name="processing-rows"></a>處理資料列  
 透過呼叫 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.AddRow%2A> 方法，將資料列加入輸出緩衝區，這將會建立資料行中為空值的新緩衝區資料列。 元件就會將值指派給個別資料行。 資料流程工作會建立和監視提供給元件的輸出緩衝區。 當它們變滿時，會將緩衝區中的資料列移到下一個元件。 並沒有任何方法可以判斷何時會將資料列批次傳送到下一個元件，因為由資料流程工作來移動資料列，對元件開發人員而言是透明的，而且 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.RowCount%2A> 屬性在輸出緩衝區中永遠都是零。 當來源元件完成將資料列加入其輸出緩衝區時，它會透過呼叫 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.SetEndOfRowset%2A> 的 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer> 方法，來通知資料流程工作，而且在緩衝區中的其餘資料列會傳遞到下一個元件。  
  
 當來源元件從外部資料來源讀取資料列時，您可能會想要呼叫 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.IncrementPipelinePerfCounter%2A> 方法，以更新 "Rows read" 或是 "BLOB bytes read" 效能計數器。 如需相關資訊，請參閱 [Performance Counters](../../integration-services/performance/performance-counters.md)。  
  
 下列程式碼範例顯示將資料列加入 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A> 中的輸出緩衝區的元件。 在上述程式碼範例中使用 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PreExecute%2A> 來找到緩衝區中的輸出資料行索引。  
  
```csharp  
public override void PrimeOutput(int outputs, int[] outputIDs, PipelineBuffer[] buffers)  
{  
    IDTSOutput100 output = ComponentMetaData.OutputCollection[0];  
    PipelineBuffer buffer = buffers[0];  
  
    SqlDataReader dataReader = sqlCommand.ExecuteReader();  
  
    // Loop over the rows in the DataReader,   
    // and add them to the output buffer.  
    while (dataReader.Read())  
    {  
        // Add a row to the output buffer.  
        buffer.AddRow();  
  
        for (int x = 0; x < columnInformation.Count; x++)  
        {  
            ColumnInfo ci = (ColumnInfo)columnInformation[x];  
            int ordinal = dataReader.GetOrdinal(ci.ColumnName);  
  
            if (dataReader.IsDBNull(ordinal))  
                buffer.SetNull(ci.BufferColumnIndex);  
            else  
            {  
                buffer[ci.BufferColumnIndex] = dataReader[ci.ColumnName];  
            }  
        }  
    }  
    buffer.SetEndOfRowset();  
}  
```  
  
```vb  
Public Overrides Sub PrimeOutput(ByVal outputs As Integer, ByVal outputIDs As Integer(), ByVal buffers As PipelineBuffer())  
  
    Dim output As IDTSOutput100 = ComponentMetaData.OutputCollection(0)  
    Dim buffer As PipelineBuffer = buffers(0)  
  
    Dim dataReader As SqlDataReader = sqlCommand.ExecuteReader()  
  
    ' Loop over the rows in the DataReader,   
    ' and add them to the output buffer.  
    While (dataReader.Read())  
  
        ' Add a row to the output buffer.  
        buffer.AddRow()  
  
        For x As Integer = 0 To columnInformation.Count  
  
            Dim ci As ColumnInfo = CType(columnInformation(x), ColumnInfo)  
  
            Dim ordinal As Integer = dataReader.GetOrdinal(ci.ColumnName)  
  
            If (dataReader.IsDBNull(ordinal)) Then  
                buffer.SetNull(ci.BufferColumnIndex)  
            Else  
                buffer(ci.BufferColumnIndex) = dataReader(ci.ColumnName)  
  
            End If  
        Next  
  
    End While  
  
    buffer.SetEndOfRowset()  
End Sub  
```  
  
## <a name="sample"></a>範例  
 下列範例顯示範例來源元件，它使用檔案連接管理員來將檔案的二進位內容載入資料流程。 這個範例並未示範本主題中討論的所有方法與功能。 它示範每個自訂來源元件必須覆寫的重要方法，但是並不包含設計階段驗證的程式碼。  
  
```csharp  
using System;  
using System.IO;  
using Microsoft.SqlServer.Dts.Pipeline;  
using Microsoft.SqlServer.Dts.Pipeline.Wrapper;  
using Microsoft.SqlServer.Dts.Runtime.Wrapper;  
  
namespace BlobSrc  
{  
  [DtsPipelineComponent(DisplayName = "BLOB Inserter Source", Description = "Inserts files into the data flow as BLOBs")]  
  public class BlobSrc : PipelineComponent  
  {  
    IDTSConnectionManager100 m_ConnMgr;  
    int m_FileNameColumnIndex = -1;  
    int m_FileBlobColumnIndex = -1;  
  
    public override void ProvideComponentProperties()  
    {  
      IDTSOutput100 output = ComponentMetaData.OutputCollection.New();  
      output.Name = "BLOB File Inserter Output";  
  
      IDTSOutputColumn100 column = output.OutputColumnCollection.New();  
      column.Name = "FileName";  
      column.SetDataTypeProperties(DataType.DT_WSTR, 256, 0, 0, 0);  
  
      column = output.OutputColumnCollection.New();  
      column.Name = "FileBLOB";  
      column.SetDataTypeProperties(DataType.DT_IMAGE, 0, 0, 0, 0);  
  
      IDTSRuntimeConnection100 conn = ComponentMetaData.RuntimeConnectionCollection.New();  
      conn.Name = "FileConnection";  
    }  
  
    public override void AcquireConnections(object transaction)  
    {  
      IDTSRuntimeConnection100 conn = ComponentMetaData.RuntimeConnectionCollection[0];  
      m_ConnMgr = conn.ConnectionManager;  
    }  
  
    public override void ReleaseConnections()  
    {  
      m_ConnMgr = null;  
    }  
  
    public override void PreExecute()  
    {  
      IDTSOutput100 output = ComponentMetaData.OutputCollection[0];  
  
      m_FileNameColumnIndex = (int)BufferManager.FindColumnByLineageID(output.Buffer, output.OutputColumnCollection[0].LineageID);  
      m_FileBlobColumnIndex = (int)BufferManager.FindColumnByLineageID(output.Buffer, output.OutputColumnCollection[1].LineageID);  
    }  
  
    public override void PrimeOutput(int outputs, int[] outputIDs, PipelineBuffer[] buffers)  
    {  
      string strFileName = (string)m_ConnMgr.AcquireConnection(null);  
  
      while (strFileName != null)  
      {  
        buffers[0].AddRow();  
  
        buffers[0].SetString(m_FileNameColumnIndex, strFileName);  
  
        FileInfo fileInfo = new FileInfo(strFileName);  
        byte[] fileData = new byte[fileInfo.Length];  
        FileStream fs = new FileStream(strFileName, FileMode.Open, FileAccess.Read, FileShare.Read);  
        fs.Read(fileData, 0, fileData.Length);  
  
        buffers[0].AddBlobData(m_FileBlobColumnIndex, fileData);  
  
        strFileName = (string)m_ConnMgr.AcquireConnection(null);  
      }  
  
      buffers[0].SetEndOfRowset();  
    }  
  }  
}  
```  
  
```vb  
Imports System   
Imports System.IO   
Imports Microsoft.SqlServer.Dts.Pipeline   
Imports Microsoft.SqlServer.Dts.Pipeline.Wrapper   
Imports Microsoft.SqlServer.Dts.Runtime.Wrapper   
Namespace BlobSrc   
  
 <DtsPipelineComponent(DisplayName="BLOB Inserter Source", Description="Inserts files into the data flow as BLOBs")> _   
 Public Class BlobSrc   
 Inherits PipelineComponent   
   Private m_ConnMgr As IDTSConnectionManager100   
   Private m_FileNameColumnIndex As Integer = -1   
   Private m_FileBlobColumnIndex As Integer = -1   
  
   Public  Overrides Sub ProvideComponentProperties()   
     Dim output As IDTSOutput100 = ComponentMetaData.OutputCollection.New   
     output.Name = "BLOB File Inserter Output"   
     Dim column As IDTSOutputColumn100 = output.OutputColumnCollection.New   
     column.Name = "FileName"   
     column.SetDataTypeProperties(DataType.DT_WSTR, 256, 0, 0, 0)   
     column = output.OutputColumnCollection.New   
     column.Name = "FileBLOB"   
     column.SetDataTypeProperties(DataType.DT_IMAGE, 0, 0, 0, 0)   
     Dim conn As IDTSRuntimeConnection90 = ComponentMetaData.RuntimeConnectionCollection.New   
     conn.Name = "FileConnection"   
   End Sub   
  
   Public  Overrides Sub AcquireConnections(ByVal transaction As Object)   
     Dim conn As IDTSRuntimeConnection100 = ComponentMetaData.RuntimeConnectionCollection(0)   
     m_ConnMgr = conn.ConnectionManager   
   End Sub   
  
   Public  Overrides Sub ReleaseConnections()   
     m_ConnMgr = Nothing   
   End Sub   
  
   Public  Overrides Sub PreExecute()   
     Dim output As IDTSOutput100 = ComponentMetaData.OutputCollection(0)   
     m_FileNameColumnIndex = CType(BufferManager.FindColumnByLineageID(output.Buffer, output.OutputColumnCollection(0).LineageID), Integer)   
     m_FileBlobColumnIndex = CType(BufferManager.FindColumnByLineageID(output.Buffer, output.OutputColumnCollection(1).LineageID), Integer)   
   End Sub   
  
   Public  Overrides Sub PrimeOutput(ByVal outputs As Integer, ByVal outputIDs As Integer(), ByVal buffers As PipelineBuffer())   
     Dim strFileName As String = CType(m_ConnMgr.AcquireConnection(Nothing), String)   
     While Not (strFileName Is Nothing)   
       buffers(0).AddRow   
       buffers(0).SetString(m_FileNameColumnIndex, strFileName)   
       Dim fileInfo As FileInfo = New FileInfo(strFileName)   
       Dim fileData(fileInfo.Length) As Byte   
       Dim fs As FileStream = New FileStream(strFileName, FileMode.Open, FileAccess.Read, FileShare.Read)   
       fs.Read(fileData, 0, fileData.Length)   
       buffers(0).AddBlobData(m_FileBlobColumnIndex, fileData)   
       strFileName = CType(m_ConnMgr.AcquireConnection(Nothing), String)   
     End While   
     buffers(0).SetEndOfRowset   
   End Sub   
 End Class   
End Namespace  
```  
  
## <a name="see-also"></a>另請參閱  
 [開發自訂目的地元件](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-destination-component.md)   
 [以指令碼元件建立來源](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-source-with-the-script-component.md)  
  
  
