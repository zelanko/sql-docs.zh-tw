---
title: 連接至指令碼工作中的資料來源 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
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
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 138dd405df110c42e8f5b754ebd64a96b133bba9
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/16/2019
ms.locfileid: "65724077"
---
# <a name="connecting-to-data-sources-in-the-script-task"></a>連接至指令碼工作中的資料來源

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  連接管理員會提供已在封裝中設定的資料來源存取權。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 連接](../../../integration-services/connection-manager/integration-services-ssis-connections.md)。  
  
 指令碼工作可以透過 **Dts** 物件的 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Connections%2A> 屬性來存取這些連線管理員。 在 <xref:Microsoft.SqlServer.Dts.Runtime.Connections> 集合中的每個連接管理員儲存有關如何連接至基礎資料來源的資訊。  
  
 當您呼叫連接管理員的 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.AcquireConnection%2A> 方法時，如果連接管理員尚未連接，連接管理員會連接至資料來源，並傳回適當的連接或是連接資訊，供您在指令碼工作程式碼中使用。  
  
> [!NOTE]  
>  您必須知道連線管理員傳回的連接類型，才能呼叫 **AcquireConnection**。 因為指令碼工作已啟用 **Option Strict**，所以您必須將以 **Object** 類型傳回的連接，轉換為適當的連接類型，才能使用它。  
  
 您可以在程式碼中使用連接之前，先透過 <xref:Microsoft.SqlServer.Dts.Runtime.Connections.Contains%2A> 屬性傳回的 <xref:Microsoft.SqlServer.Dts.Runtime.Connections> 集合之 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Connections%2A> 方法，尋找現有的連接。  
  
> [!IMPORTANT]  
>  在指令碼工作的 Managed 程式碼中，無法呼叫傳回 Unmanaged 物件之連線管理員的 AcquireConnection 方法，例如 OLE DB 連線管理員與 Excel 連線管理員。 不過，您可以讀取這些連線管理員的 ConnectionString 屬性，而且可以透過使用來自 **System.Data.OleDb** 命名空間的 **OledbConnection** 之連接字串，直接在程式碼中連接至資料來源。  
>   
>  如果您必須呼叫會傳回 Unmanaged 物件之連線管理員的 AcquireConnection 方法，請使用 [!INCLUDE[vstecado](../../../includes/vstecado-md.md)] 連線管理員。 當您設定 [!INCLUDE[vstecado](../../../includes/vstecado-md.md)] 連接管理員以使用 OLE DB 提供者時，它會透過使用 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] Data Provider for OLE DB 來連接。 在這種情況下，AcquireConnection 方法會傳回 **System.Data.OleDb.OleDbConnection**，而不是 Unmanaged 物件。 若要將 [!INCLUDE[vstecado](../../../includes/vstecado-md.md)] 連線管理員設定成與 Excel 資料來源搭配使用，請選取 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] OLE DB Provider for Jet，指定 Excel 檔案，然後在 [連線管理員] 對話方塊的 [全部] 頁面上輸入 `Excel 8.0` (針對 Excel 97 和更新的版本)，作為 [擴充屬性] 的值。  
  
## <a name="connections-example"></a>連接範例  
 在下列程式碼範例中，示範如何從指令碼工作存取連接管理員。 範例假設您已建立和設定名為 **Test ADO.NET Connection** 的 [!INCLUDE[vstecado](../../../includes/vstecado-md.md)] 連接管理員，以及名為 **Test Flat File Connection** 的一般檔案連線管理員。 請注意，[!INCLUDE[vstecado](../../../includes/vstecado-md.md)] 連線管理員會傳回您可立即用以連接至資料來源的 **SqlConnection** 物件。 另一方面，一般檔案連接管理員只會傳回包含路徑與檔案名稱的字串。 您必須使用 **System.IO** 命名空間的方法，以開啟和處理一般檔案。  
  
```vb  
    Public Sub Main()

        Dim myADONETConnection As SqlClient.SqlConnection =
            DirectCast(Dts.Connections("Test ADO.NET Connection").AcquireConnection(Dts.Transaction),
                SqlClient.SqlConnection)
        MsgBox(myADONETConnection.ConnectionString,
            MsgBoxStyle.Information, "ADO.NET Connection")

        Dim myFlatFileConnection As String =
            DirectCast(Dts.Connections("Test Flat File Connection").AcquireConnection(Dts.Transaction),
                String)
        MsgBox(myFlatFileConnection, MsgBoxStyle.Information, "Flat File Connection")

        Dts.TaskResult = ScriptResults.Success

    End Sub
```  
  
```csharp  
        public void Main()
        {
            SqlConnection myADONETConnection = 
                Dts.Connections["Test ADO.NET Connection"].AcquireConnection(Dts.Transaction)
                as SqlConnection;
            MessageBox.Show(myADONETConnection.ConnectionString, "ADO.NET Connection");

            string myFlatFileConnection = 
                Dts.Connections["Test Flat File Connection"].AcquireConnection(Dts.Transaction) 
                as string;
            MessageBox.Show(myFlatFileConnection, "Flat File Connection");

            Dts.TaskResult = (int)ScriptResults.Success;
        }
```  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services &#40;SSIS&#41; 連線](../../../integration-services/connection-manager/integration-services-ssis-connections.md)   
 [建立連線管理員](https://msdn.microsoft.com/library/6ca317b8-0061-4d9d-b830-ee8c21268345)  
  
  
