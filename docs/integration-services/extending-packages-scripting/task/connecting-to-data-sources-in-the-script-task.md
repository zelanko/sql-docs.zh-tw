---
title: "Connecting to Data Sources in the Script Task |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
helpviewer_keywords:
- connections [Integration Services], scripts
- Integration Services packages, connections
- connection managers [Integration Services], scripts
- scripts [Integration Services], connections
- SSIS packages, connections
- packages [Integration Services], connections
- Script task [Integration Services], connections
- Connections property
- SQL Server Integration Services packages, connections
- SSIS Script task, connections
ms.assetid: 9c008380-715b-455b-9da7-22572d67c388
caps.latest.revision: 59
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 825ff059476614085a338dd9c568031885bed64b
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="connecting-to-data-sources-in-the-script-task"></a>連接至指令碼工作中的資料來源
  連接管理員會提供已在封裝中設定的資料來源存取權。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 連接](../../../integration-services/connection-manager/integration-services-ssis-connections.md)。  
  
 指令碼工作可以存取這些連接管理員，透過<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Connections%2A>屬性**Dts**物件。 在 <xref:Microsoft.SqlServer.Dts.Runtime.Connections> 集合中的每個連接管理員儲存有關如何連接至基礎資料來源的資訊。  
  
 當您呼叫連接管理員的 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.AcquireConnection%2A> 方法時，如果連接管理員尚未連接，連接管理員會連接至資料來源，並傳回適當的連接或是連接資訊，供您在指令碼工作程式碼中使用。  
  
> [!NOTE]  
>  您必須知道連接管理員，然後再呼叫所傳回的連接類型**AcquireConnection**。 因為指令碼工作**Option Strict**啟用，您必須轉換的連接，傳回類型為**物件**，才能使用它與適當的連線類型。  
  
 您可以在程式碼中使用連接之前，先透過 <xref:Microsoft.SqlServer.Dts.Runtime.Connections.Contains%2A> 屬性傳回的 <xref:Microsoft.SqlServer.Dts.Runtime.Connections> 集合之 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Connections%2A> 方法，尋找現有的連接。  
  
> [!IMPORTANT]  
>  您無法呼叫 AcquireConnection 方法傳回 unmanaged 的物件，例如 OLE DB 連接管理員與 Excel 連接管理員，在 managed 程式碼的指令碼工作中的連接管理員。 不過，您可以讀取這些連接管理員之 ConnectionString 屬性，並連接到資料來源直接在您的程式碼中使用的連接字串**OledbConnection**從**System.Data.OleDb**命名空間。  
>   
>  如果您必須傳回 unmanaged 的物件的管理員呼叫 AcquireConnection 方法的連線，使用[!INCLUDE[vstecado](../../../includes/vstecado-md.md)]連接管理員。 當您設定 [!INCLUDE[vstecado](../../../includes/vstecado-md.md)] 連接管理員以使用 OLE DB 提供者時，它會透過使用 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] Data Provider for OLE DB 來連接。 在此案例中，說明 AcquireConnection 方法傳回**System.Data.OleDb.OleDbConnection**而不是未受管理的物件。 若要設定[!INCLUDE[vstecado](../../../includes/vstecado-md.md)]搭配 Excel 資料來源，選取連接管理員[!INCLUDE[msCoName](../../../includes/msconame-md.md)]OLE DB Provider for Jet，指定 Excel 檔案，並輸入`Excel 8.0`（針對 Excel 97 和更新版本） 做為值**擴充屬性**上**所有**頁面**連線管理員** 對話方塊。  
  
## <a name="connections-example"></a>連接範例  
 在下列程式碼範例中，示範如何從指令碼工作存取連接管理員。 此範例假設您已建立和設定[!INCLUDE[vstecado](../../../includes/vstecado-md.md)]名為連接管理員**Test ADO.NET Connection**和名為 「 一般檔案連接管理員**Test Flat File Connection**。 請注意，[!INCLUDE[vstecado](../../../includes/vstecado-md.md)]連接管理員會傳回**SqlConnection**物件，您可以立即用來連接到資料來源。 另一方面，一般檔案連接管理員只會傳回包含路徑與檔案名稱的字串。 您必須使用從方法**System.IO**來開啟和使用的一般檔案的命名空間。  
  
```vb  
Public Sub Main()  
  
    Dim myADONETConnection As SqlClient.SqlConnection  
    myADONETConnection = _  
        DirectCast(Dts.Connections("Test ADO.NET Connection").AcquireConnection(Dts.Transaction), _  
        SqlClient.SqlConnection)  
    MsgBox(myADONETConnection.ConnectionString, _  
        MsgBoxStyle.Information, "ADO.NET Connection")  
  
    Dim myFlatFileConnection As String  
    myFlatFileConnection = _  
        DirectCast(Dts.Connections("Test Flat File Connection").AcquireConnection(Dts.Transaction), _  
        String)  
    MsgBox(myFlatFileConnection, MsgBoxStyle.Information, "Flat File Connection")  
  
    Dts.TaskResult = ScriptResults.Success  
  
End Sub  
```  
  
```csharp  
using System;  
using System.Data.SqlClient;  
using Microsoft.SqlServer.Dts.Runtime;  
using System.Windows.Forms;  
  
public class ScriptMain  
{  
  
        public void Main()  
        {  
            SqlConnection myADONETConnection = new SqlConnection();  
            myADONETConnection = (SqlConnection)(Dts.Connections["Test ADO.NET Connection"].AcquireConnection(Dts.Transaction)as SqlConnection);  
            MessageBox.Show(myADONETConnection.ConnectionString, "ADO.NET Connection");  
  
            string myFlatFileConnection;  
            myFlatFileConnection = (string)(Dts.Connections["Test Flat File Connection"].AcquireConnection(Dts.Transaction) as String);  
            MessageBox.Show(myFlatFileConnection, "Flat File Connection");  
  
            Dts.TaskResult = (int)ScriptResults.Success;  
  
        }  
  
}  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services &#40;SSIS &#41;連線](../../../integration-services/connection-manager/integration-services-ssis-connections.md)   
 [建立連接管理員](http://msdn.microsoft.com/library/6ca317b8-0061-4d9d-b830-ee8c21268345)  
  
  
