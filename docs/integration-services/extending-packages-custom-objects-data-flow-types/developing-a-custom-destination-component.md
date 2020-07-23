---
title: 開發自訂目的地元件 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
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
- destinations [Integration Services], components
- ProcessInput method
- external data sources [Integration Services]
- custom data flow components [Integration Services], destination components
- data flow components [Integration Services], destination components
ms.assetid: 24619363-9535-4c0e-8b62-1d22c6630e40
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d819dc54c992c20d8558860420d27e4b54b09760
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/22/2020
ms.locfileid: "86923727"
---
# <a name="developing-a-custom-destination-component"></a>開發自訂目的地元件

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 可讓開發人員撰寫自訂目的地元件，以便連線到任何自訂資料來源中的資料，以及將資料儲存到任何自訂資料來源。 當您必須連接至無法使用 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 隨附的其中一個現有來源元件所存取的資料來源時，自訂目的地元件就很有用。  
  
 目的地元件具有一或多個輸入與零個輸出。 在設計階段中，它們會建立並設定連接，並且從外部資料來源中讀取資料行中繼資料。 在執行期間，它們會連接至外部資料來源，並且將從資料流程的上游元件收到的資料列加入至外部資料來源。 如果外部資料來源在執行此元件之前就存在，目的地元件也必須確定此元件收到之資料行的資料類型與外部資料來源之資料行的資料類型相符。  
  
 本節將討論如何開發目的地元件的詳細資料，並且提供程式碼範例以釐清重要的概念。 如需資料流程元件開發的一般概觀，請參閱[開發自訂資料流程元件](../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)。  
  
## <a name="design-time"></a>設計階段  
 實作目的地元件的設計階段功能包括指定外部資料來源的連接，以及驗證元件是否已正確設定。 根據定義，目的地元件具有一個輸入，而且可能具有一個錯誤輸出。  
  
### <a name="creating-the-component"></a>建立元件  
 目的地元件會使用在封裝中定義的 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 物件，連接至外部資料來源。 目的地元件會將元素新增至 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ComponentMetaData%2A> 的 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.RuntimeConnectionCollection%2A> 集合，以向 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計工具和元件的使用者指出其連線管理員的需求。 這個集合有兩個目的：首先，它會向 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師通告連接管理員的需求。然後，在使用者已選取或建立連接管理員之後，它會在封裝中保留元件所使用之連接管理員的參考。 將 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSRuntimeConnection100> 新增至集合時，[進階編輯器]  會顯示 [連線屬性]  索引標籤，提示使用者在套件中選取或建立連線以供元件使用。  
  
 下列程式碼範例會顯示 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProvideComponentProperties%2A> 的實作，它加入輸入並將 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSRuntimeConnection100> 物件加入至 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.RuntimeConnectionCollection%2A>。  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Pipeline;  
using Microsoft.SqlServer.Dts.Pipeline.Wrapper;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace Microsoft.Samples.SqlServer.Dts  
{  
    [DtsPipelineComponent(DisplayName = "Destination Component",ComponentType =ComponentType.DestinationAdapter)]  
    public class DestinationComponent : PipelineComponent   
    {  
        public override void ProvideComponentProperties()  
        {  
            // Reset the component.  
            base.RemoveAllInputsOutputsAndCustomProperties();  
            ComponentMetaData.RuntimeConnectionCollection.RemoveAll();  
  
            IDTSInput100 input = ComponentMetaData.InputCollection.New();  
            input.Name = "Input";  
  
            IDTSRuntimeConnection100 connection = ComponentMetaData.RuntimeConnectionCollection.New();  
            connection.Name = "ADO.net";  
        }  
    }  
}  
```  
  
```vb  
Imports System  
Imports System.Data  
Imports System.Data.SqlClient  
Imports Microsoft.SqlServer.Dts.Pipeline  
Imports Microsoft.SqlServer.Dts.Pipeline.Wrapper  
Imports Microsoft.SqlServer.Dts.Runtime  
  
Namespace Microsoft.Samples.SqlServer.Dts  
  
    <DtsPipelineComponent(DisplayName:="Destination Component", ComponentType:=ComponentType.DestinationAdapter)> _  
    Public Class DestinationComponent  
        Inherits PipelineComponent  
  
        Public Overrides Sub ProvideComponentProperties()  
  
            ' Reset the component.  
            Me.RemoveAllInputsOutputsAndCustomProperties()  
            ComponentMetaData.RuntimeConnectionCollection.RemoveAll()  
  
            Dim input As IDTSInput100 = ComponentMetaData.InputCollection.New()  
            input.Name = "Input"  
  
            Dim connection As IDTSRuntimeConnection100 = ComponentMetaData.RuntimeConnectionCollection.New()  
            connection.Name = "ADO.net"  
  
        End Sub  
    End Class  
End Namespace  
```  
  
### <a name="connecting-to-an-external-data-source"></a>連接到外部資料來源  
 在將連接加入至 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.RuntimeConnectionCollection%2A> 之後，就可覆寫 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.AcquireConnections%2A> 方法以建立外部資料來源的連接。 這個方法會在設計階段和執行階段呼叫。 元件必須建立一個連接，以便連至執行階段連接所指定的連接管理員，之後再連至外部資料來源。 一旦建立連接之後，元件就應該在內部快取連接，然後在呼叫 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ReleaseConnections%2A> 時釋放此連接。 開發人員會覆寫這個方法，並在 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.AcquireConnections%2A> 期間釋放元件建立的連接。 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ReleaseConnections%2A> 和 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.AcquireConnections%2A> 這兩個方法是在設計階段與執行階段呼叫的。  
  
 下列程式碼範例會顯示一個元件，它在 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.AcquireConnections%2A> 方法中連接至 ADO.NET 連接，然後在 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ReleaseConnections%2A> 方法中關閉此連接。  
  
```csharp  
using Microsoft.SqlServer.Dts.Runtime.Wrapper;  
  
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
Imports Microsoft.SqlServer.Dts.Runtime.Wrapper  
  
Private sqlConnection As SqlConnection  
  
Public Overrides Sub AcquireConnections(ByVal transaction As Object)  
  
    If IsNothing(ComponentMetaData.RuntimeConnectionCollection(0).ConnectionManager) = False Then  
  
        Dim cm As ConnectionManager = DtsConvert.GetWrapper(ComponentMetaData.RuntimeConnectionCollection(0).ConnectionManager)  
        Dim cmado As ConnectionManagerAdoNet = CType(cm.InnerObject,ConnectionManagerAdoNet)  
  
        If IsNothing(cmado) Then  
            Throw New Exception("The ConnectionManager " + cm.Name + " is not an ADO.NET connection.")  
        End If  
  
        sqlConnection = CType(cmado.AcquireConnection(transaction), SqlConnection)  
        sqlConnection.Open()  
  
    End If  
End Sub  
  
Public Overrides Sub ReleaseConnections()  
  
    If IsNothing(sqlConnection) = False And sqlConnection.State <> ConnectionState.Closed Then  
        sqlConnection.Close()  
    End If  
  
End Sub  
```  
  
### <a name="validating-the-component"></a>驗證元件  
 目的地元件開發人員應該依照[元件驗證](../../integration-services/extending-packages-custom-objects/data-flow/validating-a-data-flow-component.md)中所述的內容執行驗證。 此外，他們應該驗證元件輸入資料行集合中定義的資料行資料類型屬性與外部資料來源的資料行相符。 有時候，您可能無法或不想要針對外部資料來源驗證輸入資料行，例如元件或 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師處於中斷連接狀態時，或者無法接受伺服器的往返時。 在這些情況下，您仍然可以使用輸入物件的 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSInput100.ExternalMetadataColumnCollection%2A> 來驗證輸入資料行集合中的資料行。  
  
 這個集合同時存在輸入和輸出物件上，而且必須由元件開發人員根據外部資料來源的資料行擴展它。 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計工具離線、中斷元件連線或 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.ValidateExternalMetadata%2A> 屬性為 **false** 時，這個集合可以用來驗證輸入資料行。  
  
 下列範例程式碼會加入以現有輸入資料行為基礎的外部中繼資料行。  
  
```csharp  
private void AddExternalMetaDataColumn(IDTSInput100 input,IDTSInputColumn100 inputColumn)  
{  
    // Set the properties of the external metadata column.  
    IDTSExternalMetadataColumn100 externalColumn = input.ExternalMetadataColumnCollection.New();  
    externalColumn.Name = inputColumn.Name;  
    externalColumn.Precision = inputColumn.Precision;  
    externalColumn.Length = inputColumn.Length;  
    externalColumn.DataType = inputColumn.DataType;  
    externalColumn.Scale = inputColumn.Scale;  
  
    // Map the external column to the input column.  
    inputColumn.ExternalMetadataColumnID = externalColumn.ID;  
}  
```  
  
```vb  
Private Sub AddExternalMetaDataColumn(ByVal input As IDTSInput100, ByVal inputColumn As IDTSInputColumn100)  
  
    ' Set the properties of the external metadata column.  
    Dim externalColumn As IDTSExternalMetadataColumn100 = input.ExternalMetadataColumnCollection.New()  
    externalColumn.Name = inputColumn.Name  
    externalColumn.Precision = inputColumn.Precision  
    externalColumn.Length = inputColumn.Length  
    externalColumn.DataType = inputColumn.DataType  
    externalColumn.Scale = inputColumn.Scale  
  
    ' Map the external column to the input column.  
    inputColumn.ExternalMetadataColumnID = externalColumn.ID  
  
End Sub  
```  
  
## <a name="run-time"></a>執行階段  
 在執行期間，每當上游元件提供完整的 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> 時，目的地元件就會接收 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer> 方法的呼叫。 系統會重複呼叫這個方法，直到沒有其他緩衝區可用而且 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.EndOfRowset%2A> 屬性為 **true** 為止。 執行這個方法期間，目的地元件會讀取緩衝區中的資料行和資料列，並且將它們加入至外部資料來源。  
  
### <a name="locating-columns-in-the-buffer"></a>找出緩衝區中的資料行  
 元件的輸入緩衝區包含資料流程中上游元件之輸出資料行集合內定義的所有資料行。 例如，如果來源元件在其輸出中提供三個資料行，而下一個元件加入額外的輸出資料行，則提供給目的地元件的緩衝區就會包含四個資料行，即使目的地元件只會寫入兩個資料行也一樣。  
  
 輸入緩衝區中的資料行順序不是由目的地元件之輸入資料行集合內的資料行索引所定義。 只有使用 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSBufferManager100.FindColumnByLineageID%2A> 的 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.BufferManager%2A> 方法，才能可靠地在緩衝區資料列中找出資料行。 這個方法會在指定的緩衝區中找到具有指定之歷程識別碼的資料行，並傳回它在資料列中的位置。 輸入資料行的索引通常會在執行 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PreExecute%2A> 方法期間找到，而且由開發人員快取，以便之後在 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> 期間使用。  
  
 下列程式碼範例會在 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PreExecute%2A> 期間，在緩衝區中尋找輸入資料行的位置，並將它們儲存在陣列中。 之後，此陣列會在 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> 期間使用，以便讀取緩衝區中資料行的值。  
  
```csharp  
int[] cols;  
  
public override void PreExecute()  
{  
    IDTSInput100 input = ComponentMetaData.InputCollection[0];  
  
    cols = new int[input.InputColumnCollection.Count];  
  
    for (int x = 0; x < input.InputColumnCollection.Count; x++)  
    {  
        cols[x] = BufferManager.FindColumnByLineageID(input.Buffer, input.InputColumnCollection[x].LineageID);  
    }  
}  
```  
  
```vb  
Private cols As Integer()  
  
Public Overrides Sub PreExecute()  
  
    Dim input As IDTSInput100 = ComponentMetaData.InputCollection(0)  
  
    ReDim cols(input.InputColumnCollection.Count)  
  
    For x As Integer = 0 To input.InputColumnCollection.Count  
  
        cols(x) = BufferManager.FindColumnByLineageID(input.Buffer, input.InputColumnCollection(x).LineageID)  
    Next x  
  
End Sub  
```  
  
### <a name="processing-rows"></a>處理資料列  
 一旦在緩衝區中找到輸入資料行之後，就可以讀取它們並將它們寫入外部資料來源。  
  
 當目的地元件將資料列寫入外部資料來源時，您可能會想要呼叫 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.IncrementPipelinePerfCounter%2A> 方法，藉以更新 "Rows read" 或 "BLOB bytes read" 效能計數器。 如需相關資訊，請參閱 [Performance Counters](../../integration-services/performance/performance-counters.md)。  
  
 下列程式碼範例會顯示從 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> 提供之緩衝區中讀取資料列的元件。 在上述程式碼範例中，緩衝區內的資料行索引是在 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PreExecute%2A> 期間找到的。  
  
```csharp  
public override void ProcessInput(int inputID, PipelineBuffer buffer)  
{  
        while (buffer.NextRow())  
        {  
            foreach (int col in cols)  
            {  
                if (!buffer.IsNull(col))  
                {  
                    //  TODO: Read the column data.  
                }  
            }  
        }  
}  
```  
  
```vb  
Public Overrides Sub ProcessInput(ByVal inputID As Integer, ByVal buffer As PipelineBuffer)  
  
        While (buffer.NextRow())  
  
            For Each col As Integer In cols  
  
                If buffer.IsNull(col) = False Then  
  
                    '  TODO: Read the column data.  
                End If  
  
            Next col  
        End While  
End Sub  
```  
  
## <a name="sample"></a>範例  
 下列範例會顯示範例目的地元件，它使用檔案連接管理員，將資料流程的二進位資料儲存至檔案中。 這個範例並未示範本主題中討論的所有方法與功能。 它示範每個自訂目的地元件必須覆寫的重要方法，但是並不包含設計階段驗證的程式碼。  
  
```csharp  
using System;  
using System.IO;  
using Microsoft.SqlServer.Dts.Pipeline;  
using Microsoft.SqlServer.Dts.Pipeline.Wrapper;  
  
namespace BlobDst  
{  
  [DtsPipelineComponent(DisplayName = "BLOB Extractor Destination", Description = "Writes values of BLOB columns to files")]  
  public class BlobDst : PipelineComponent  
  {  
    string m_DestDir;  
    int m_FileNameColumnIndex = -1;  
    int m_BlobColumnIndex = -1;  
  
    public override void ProvideComponentProperties()  
    {  
      IDTSInput100 input = ComponentMetaData.InputCollection.New();  
      input.Name = "BLOB Extractor Destination Input";  
      input.HasSideEffects = true;  
  
      IDTSRuntimeConnection100 conn = ComponentMetaData.RuntimeConnectionCollection.New();  
      conn.Name = "FileConnection";  
    }  
  
    public override void AcquireConnections(object transaction)  
    {  
      IDTSRuntimeConnection100 conn = ComponentMetaData.RuntimeConnectionCollection[0];  
      m_DestDir = (string)conn.ConnectionManager.AcquireConnection(null);  
  
      if (m_DestDir.Length > 0 && m_DestDir[m_DestDir.Length - 1] != '\\')  
        m_DestDir += "\\";  
    }  
  
    public override IDTSInputColumn100 SetUsageType(int inputID, IDTSVirtualInput100 virtualInput, int lineageID, DTSUsageType usageType)  
    {  
      IDTSInputColumn100 inputColumn = base.SetUsageType(inputID, virtualInput, lineageID, usageType);  
      IDTSCustomProperty100 custProp;  
  
      custProp = inputColumn.CustomPropertyCollection.New();  
      custProp.Name = "IsFileName";  
      custProp.Value = (object)false;  
  
      custProp = inputColumn.CustomPropertyCollection.New();  
      custProp.Name = "IsBLOB";  
      custProp.Value = (object)false;  
  
      return inputColumn;  
    }  
  
    public override void PreExecute()  
    {  
      IDTSInput100 input = ComponentMetaData.InputCollection[0];  
      IDTSInputColumnCollection100 inputColumns = input.InputColumnCollection;  
      IDTSCustomProperty100 custProp;  
  
      foreach (IDTSInputColumn100 column in inputColumns)  
      {  
        custProp = column.CustomPropertyCollection["IsFileName"];  
        if ((bool)custProp.Value == true)  
        {  
          m_FileNameColumnIndex = (int)BufferManager.FindColumnByLineageID(input.Buffer, column.LineageID);  
        }  
  
        custProp = column.CustomPropertyCollection["IsBLOB"];  
        if ((bool)custProp.Value == true)  
        {  
          m_BlobColumnIndex = (int)BufferManager.FindColumnByLineageID(input.Buffer, column.LineageID);  
        }  
      }  
    }  
  
    public override void ProcessInput(int inputID, PipelineBuffer buffer)  
    {  
      while (buffer.NextRow())  
      {  
        string strFileName = buffer.GetString(m_FileNameColumnIndex);  
        int blobLength = (int)buffer.GetBlobLength(m_BlobColumnIndex);  
        byte[] blobData = buffer.GetBlobData(m_BlobColumnIndex, 0, blobLength);  
  
        strFileName = TranslateFileName(strFileName);  
  
        // Make sure directory exists before creating file.  
        FileInfo fi = new FileInfo(strFileName);  
        if (!fi.Directory.Exists)  
          fi.Directory.Create();  
  
        // Write the data to the file.  
        FileStream fs = new FileStream(strFileName, FileMode.Create, FileAccess.Write, FileShare.None);  
        fs.Write(blobData, 0, blobLength);  
        fs.Close();  
      }  
    }  
  
    private string TranslateFileName(string fileName)  
    {  
      if (fileName.Length > 2 && fileName[1] == ':')  
        return m_DestDir + fileName.Substring(3, fileName.Length - 3);  
      else  
        return m_DestDir + fileName;  
    }  
  }  
}  
```  
  
```vb  
Imports System   
Imports System.IO   
Imports Microsoft.SqlServer.Dts.Pipeline   
Imports Microsoft.SqlServer.Dts.Pipeline.Wrapper   
Namespace BlobDst   
  
 <DtsPipelineComponent(DisplayName="BLOB Extractor Destination", Description="Writes values of BLOB columns to files")> _   
 Public Class BlobDst   
 Inherits PipelineComponent   
   Private m_DestDir As String   
   Private m_FileNameColumnIndex As Integer = -1   
   Private m_BlobColumnIndex As Integer = -1   
  
   Public  Overrides Sub ProvideComponentProperties()   
     Dim input As IDTSInput100 = ComponentMetaData.InputCollection.New   
     input.Name = "BLOB Extractor Destination Input"   
     input.HasSideEffects = True   
     Dim conn As IDTSRuntimeConnection100 = ComponentMetaData.RuntimeConnectionCollection.New   
     conn.Name = "FileConnection"   
   End Sub   
  
   Public  Overrides Sub AcquireConnections(ByVal transaction As Object)   
     Dim conn As IDTSRuntimeConnection100 = ComponentMetaData.RuntimeConnectionCollection(0)   
     m_DestDir = CType(conn.ConnectionManager.AcquireConnection(Nothing), String)   
     If m_DestDir.Length > 0 AndAlso Not (m_DestDir(m_DestDir.Length - 1) = "\"C) Then   
       m_DestDir += "\"   
     End If   
   End Sub   
  
   Public  Overrides Function SetUsageType(ByVal inputID As Integer, ByVal virtualInput As IDTSVirtualInput100, ByVal lineageID As Integer, ByVal usageType As DTSUsageType) As IDTSInputColumn100   
     Dim inputColumn As IDTSInputColumn100 = MyBase.SetUsageType(inputID, virtualInput, lineageID, usageType)   
     Dim custProp As IDTSCustomProperty100   
     custProp = inputColumn.CustomPropertyCollection.New   
     custProp.Name = "IsFileName"   
     custProp.Value = CType(False, Object)   
     custProp = inputColumn.CustomPropertyCollection.New   
     custProp.Name = "IsBLOB"   
     custProp.Value = CType(False, Object)   
     Return inputColumn   
   End Function   
  
   Public  Overrides Sub PreExecute()   
     Dim input As IDTSInput100 = ComponentMetaData.InputCollection(0)   
     Dim inputColumns As IDTSInputColumnCollection100 = input.InputColumnCollection   
     Dim custProp As IDTSCustomProperty100   
     For Each column As IDTSInputColumn100 In inputColumns   
       custProp = column.CustomPropertyCollection("IsFileName")   
       If CType(custProp.Value, Boolean) = True Then   
         m_FileNameColumnIndex = CType(BufferManager.FindColumnByLineageID(input.Buffer, column.LineageID), Integer)   
       End If   
       custProp = column.CustomPropertyCollection("IsBLOB")   
       If CType(custProp.Value, Boolean) = True Then   
         m_BlobColumnIndex = CType(BufferManager.FindColumnByLineageID(input.Buffer, column.LineageID), Integer)   
       End If   
     Next   
   End Sub   
  
   Public  Overrides Sub ProcessInput(ByVal inputID As Integer, ByVal buffer As PipelineBuffer)   
     While buffer.NextRow   
       Dim strFileName As String = buffer.GetString(m_FileNameColumnIndex)   
       Dim blobLength As Integer = CType(buffer.GetBlobLength(m_BlobColumnIndex), Integer)   
       Dim blobData As Byte() = buffer.GetBlobData(m_BlobColumnIndex, 0, blobLength)   
       strFileName = TranslateFileName(strFileName)   
       Dim fi As FileInfo = New FileInfo(strFileName)   
       ' Make sure directory exists before creating file.  
       If Not fi.Directory.Exists Then   
         fi.Directory.Create   
       End If   
       ' Write the data to the file.  
       Dim fs As FileStream = New FileStream(strFileName, FileMode.Create, FileAccess.Write, FileShare.None)   
       fs.Write(blobData, 0, blobLength)   
       fs.Close   
     End While   
   End Sub   
  
   Private Function TranslateFileName(ByVal fileName As String) As String   
     If fileName.Length > 2 AndAlso fileName(1) = ":"C Then   
       Return m_DestDir + fileName.Substring(3, fileName.Length - 3)   
     Else   
       Return m_DestDir + fileName   
     End If   
   End Function   
 End Class   
End Namespace  
```  
  
## <a name="see-also"></a>另請參閱  
 [開發自訂來源元件](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-source-component.md)   
 [使用指令碼元件建立目的地](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)  
  
  
