---
title: "Connecting to Data Sources in the Script Component |Microsoft 文件"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Script component [Integration Services], connecting to data sources
ms.assetid: 96de63ab-ff48-4e7e-89e0-ffd6a89c63b6
caps.latest.revision: 15
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: e2accca553f1bd9c536076fd0bbcebbff0ff2c42
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="connecting-to-data-sources-in-the-script-component"></a>連接到指令碼元件中的資料來源
  連接管理員只是一種便利的單位，用以封裝和儲存連接至特定類型的資料來源所需的資訊。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 連接](../../../integration-services/connection-manager/integration-services-ssis-connections.md)。  
  
 您可以讓現有的連接管理員可用於存取來源或目的地元件中的自訂指令碼，即可**新增**和**移除**按鈕**連接管理員**頁面**指令碼轉換編輯器**。 不過，您必須撰寫自己的自訂程式碼，以載入或是儲存資料，以及 (可能的話) 開啟和關閉連至資料來源的連接。 如需有關**連接管理員**頁面**指令碼轉換編輯器**，請參閱[設定指令碼元件指令碼元件編輯器中](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md)和[指令碼轉換編輯器 &#40;連接管理員頁面 &#41;](../../../integration-services/data-flow/transformations/script-transformation-editor-connection-managers-page.md).  
  
 指令碼元件建立**連線**中的集合類別**ComponentWrapper**專案項目，其中包含每個名稱與連接管理員本身的名稱相同的連接管理員的強型別存取子。 此集合會公開透過**連線**屬性**ScriptMain**類別。 存取子屬性會傳回連接管理員的參考，以做為 <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.IDTSConnectionManager100> 的執行個體。 例如，如果您已在對話方塊的 [連接管理員] 頁面中加入名為 `MyADONETConnection` 的連接管理員，就可以加入下列程式碼，取得指令碼中該連接管理員的參考：  
  
 `Dim myADONETConnectionManager As IDTSConnectionManager100 = _`  
  
 `Me.Connections.MyADONETConnection`  
  
> [!NOTE]  
>  您必須知道的呼叫之前，會傳回連接管理員的連線類型**AcquireConnection**。 因為指令碼工作**Option Strict**啟用，您必須轉換的連接，傳回類型為**物件**，才能使用它與適當的連線類型。  
  
 接下來，呼叫**AcquireConnection**方法特定的連接管理員以取得基礎連接或連接到資料來源所需的資訊。 例如，您取得的參考**System.Data.SqlConnection**包裝由 ADO.NET 連接管理員，使用下列程式碼：  
  
 `Dim myADOConnection As SqlConnection = _`  
  
 `CType(MyADONETConnectionManager.AcquireConnection(Nothing), SqlConnection)`  
  
 相反的，對於一般檔案連接管理員的相同呼叫，只會傳回檔案資料來源的路徑與檔案名稱。  
  
 `Dim myFlatFile As String = _`  
  
 `CType(MyFlatFileConnectionManager.AcquireConnection(Nothing), String)`  
  
 然後您必須提供此路徑和檔案名稱，以便**System.IO.StreamReader**或**Streamwriter**讀取或寫入一般檔案中的資料。  
  
> [!IMPORTANT]  
>  當您在指令碼元件中撰寫 managed 程式碼時，您無法呼叫 AcquireConnection 方法的連接管理員傳回 unmanaged 的物件，例如 OLE DB 連接管理員與 Excel 連接管理員。 不過，您可以讀取這些連接管理員之 ConnectionString 屬性，並連接到資料來源直接在您的程式碼中使用的 oledb 連接字串**連接**從**System.Data.OleDb**命名空間。  
>   
>  如果您要呼叫 AcquireConnection 方法傳回 unmanaged 的物件的連接管理員，請使用 ADO.NET 連接管理員。 當您設定 ADO.NET 連接管理員以使用 OLE DB 提供者時，它會透過使用 .NET Framework Data Provider for OLE DB 來連接。 在此案例中，說明 AcquireConnection 方法傳回**System.Data.OleDb.OleDbConnection**而不是未受管理的物件。 設定 ADO.NET 連接管理員使用與 Excel 資料來源，請選取 Microsoft OLE DB Provider for Jet，指定 Excel 活頁簿，然後輸入`Excel 8.0`（針對 Excel 97 和更新版本） 的值為**擴充屬性**上**所有**頁面**連線管理員** 對話方塊。  
  
 如需如何透過指令碼元件使用連接管理員的詳細資訊，請參閱[使用指令碼元件建立來源](../../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-source-with-the-script-component.md)和[與指令碼元件建立目的地](../../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services &#40;SSIS &#41;連線](../../../integration-services/connection-manager/integration-services-ssis-connections.md)   
 [建立連接管理員](http://msdn.microsoft.com/library/6ca317b8-0061-4d9d-b830-ee8c21268345)  
  
  

