---
title: 在 ADOMD.NET 中建立連接 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- opening connections
- closing connections
- connections [ADOMD.NET]
- ADOMD.NET, connections
ms.assetid: 7b9610f5-6641-42cc-af4e-bd35771913d1
caps.latest.revision: 40
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9d7bf4529df77545cf2d0acf69af5d0b570ef750
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37165299"
---
# <a name="establishing-connections-in-adomdnet"></a>在 ADOMD.NET 中建立連接
  在 ADOMD.NET 中，您使用<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>物件，例如開啟分析資料來源連接[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]資料庫。 當不再需要連接時，應該明確地關閉連接。  
  
## <a name="opening-a-connection"></a>開啟連接  
 若要在 ADOMD.NET 中開啟連接，您必須先將連接字串指定成有效的分析資料來源與資料庫。 然後，您必須明確地開啟該資料來源的連接。  
  
### <a name="specifying-a-multidimensional-data-source"></a>指定多維度資料來源  
 若要指定分析資料來源與資料庫，請設定 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A> 物件的 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 屬性。 為 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A> 屬性指定的連接字串是 OLE DB 相容的字串。 ADOMD.NET 會使用指定的連接字串決定如何連接到伺服器。  
  
 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A> 屬性可以在現有的 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 物件上設定，或是在建立 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 物件的執行個體期間設定。 下列程式碼示範如何在建立 ADOMD 連接時設定 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A> 屬性：  
  
```vb  
Dim advwrksConnection As New AdomdConnection("Data Source=localhost;Catalog=AdventureWorksAS")  
System.Diagnostics.Debug.Writeline(advwrksConnection.ConnectionString)  
```  
  
```csharp  
AdomdConnection advwrksConnection = new AdomdConnection("Data Source=localhost;Catalog=AdventureWorksAS");  
System.Diagnostics.Debug.Writeline(advwrksConnection.ConnectionString);  
```  
  
### <a name="opening-a-connection-to-the-data-source"></a>關閉資料來源的連接  
 在指定連接字串之後，您必須使用 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.Open%2A> 方法來開啟連接。 當您開啟 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 物件時，可以為連接設定各種層級的安全性。 用於連接的安全性層級須視 `ProtectionLevel` 連接字串的設定值而定。 如需有關在 ADOMD.NET 中開啟安全連接的詳細資訊，請參閱 <<c0> [ 在 ADOMD.NET 中建立安全連線](connections-in-adomd-net-establishing-secure-connections.md)。  
  
## <a name="working-with-a-connection"></a>使用連接  
 每個開啟的連接都會存在工作階段中，後者可支援可設定狀態的作業。 工作階段可由一個以上開啟的連接共用。 共用工作階段允許一個以上的用戶端共用相同的內容。 如需詳細資訊，請參閱 <<c0> [ 使用 連接和 ADOMD.NET 中的工作階段](../multidimensional-models-adomd-net-client/connections-in-adomd-net-working-with-connections-and-sessions.md)。  
  
 您可以使用開啟的連接來擷取中繼資料、資料和執行命令。 如需詳細資訊，請參閱 <<c0> [ 擷取從分析資料來源的中繼資料](retrieving-metadata-from-an-analytical-data-source.md)，[擷取的資料，從分析資料來源](retrieving-data-from-an-analytical-data-source.md)，和[執行命令對分析資料來源](executing-commands-against-an-analytical-data-source.md)。  
  
 當連接開啟時，您可以擷取資料、擷取中繼資料並在讀取認可交易內執行命令，在這個交易中，會在讀取資料時保持共用鎖定，以避免中途讀取 (Dirty Read)。 資料仍然可以在交易結束之前變更，不過這將造成不可重複的讀取或是虛設項目資料。 如需詳細資訊，請參閱 <<c0> [ 在 ADOMD.NET 中執行的交易](../../relational-databases/native-client-ole-db-transactions/transactions.md)。  
  
## <a name="closing-a-connection"></a>關閉連接  
 我們建議您一旦不再需要連接，即明確關閉 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 物件。 若要明確關閉連接，請使用 `Close` 物件的 `Dispose` 與 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 方法。  
  
 未明確關閉但允許超出範圍的連接，可能無法夠快速地釋放伺服器資源，以利高並行的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 用戶端應用程式有效地開啟新連接。 視您如何建立連接而定，如果未明確關閉連接，<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 物件所使用的工作階段可能會保持使用中。  
  
 如需有關工作階段的詳細資訊，請參閱[使用 連接和 ADOMD.NET 中的工作階段](../multidimensional-models-adomd-net-client/connections-in-adomd-net-working-with-connections-and-sessions.md)。  
  
> [!IMPORTANT]  
>  在任何已實作類別的 `Finalize` 方法中，請勿呼叫 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 物件、<xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> 物件，或是任何其他 Managed 物件的 `Close` 或 `Dispose` 方法。 在 finalizer 中，只須釋放實作類別直接擁有的 Unmanaged 資源。 如果實作的類別未擁有任何 Unmanaged 資源，請不要在類別定義中包含 `Finalize` 方法。  
  
## <a name="see-also"></a>另請參閱  
 [ADOMD.NET 用戶端程式設計](adomd-net-client-programming.md)  
  
  
