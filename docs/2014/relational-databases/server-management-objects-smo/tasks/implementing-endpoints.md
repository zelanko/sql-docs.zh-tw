---
title: 執行端點 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- endpoints [SMO]
ms.assetid: f8674dbb-9bc0-488f-9def-e9e0ce1ddf86
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 042bc1cfe2ccf09580d052b1a4bc045d03fc81ee
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/23/2019
ms.locfileid: "72796844"
---
# <a name="implementing-endpoints"></a>實作端點
  端點是可以透過原生方式接聽要求的服務。 SMO 藉由使用 <xref:Microsoft.SqlServer.Management.Smo.Endpoint> 物件來支援各種端點類型。 您可以藉由建立 <xref:Microsoft.SqlServer.Management.Smo.Endpoint> 物件的執行個體和設定其屬性，建立處理特定裝載類型的端點服務 (此類服務使用特定的通訊協定)。  
  
 <xref:Microsoft.SqlServer.Management.Smo.Endpoint.EndpointType%2A> 物件的 <xref:Microsoft.SqlServer.Management.Smo.Endpoint> 屬性可用於指定下列其中一個裝載類型：  
  
-   資料庫鏡像  
  
-   SOAP ( [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] 及更早的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 版本中存在 SOAP 端點的支援)  
  
-   Service Broker  
  
-   [!INCLUDE[tsql](../../../includes/tsql-md.md)]  
  
 此外，<xref:Microsoft.SqlServer.Management.Smo.Endpoint.ProtocolType%2A> 屬性也可用於指定下列兩種支援的通訊協定：  
  
-   HTTP 通訊協定  
  
-   TCP 通訊協定  
  
 在指定裝載類型之後，就可以使用 <xref:Microsoft.SqlServer.Management.Smo.Endpoint.Payload%2A> 物件屬性設定實際的裝載。 <xref:Microsoft.SqlServer.Management.Smo.Payload> 物件屬性針對可修改其屬性的指定類型，提供裝載物件的參考。  
  
 如果是 <xref:Microsoft.SqlServer.Management.Smo.DatabaseMirroringPayload> 物件，則您必須指定鏡像角色以及是否啟用加密。 <xref:Microsoft.SqlServer.Management.Smo.ServiceBrokerPayload> 物件需要訊息轉送、允許的最大連接數目以及驗證模式的相關資訊。 <xref:Microsoft.SqlServer.Management.Smo.SoapPayloadMethod.%23ctor%2A> 物件需要設定多個屬性，包括 <xref:Microsoft.SqlServer.Management.Smo.SoapPayloadMethodCollection.Add%2A> 物件屬性，此屬性會指定用戶端可用的 SOAP 裝載方法 (預存程序和使用者定義函數)。  
  
 同樣地，實際的通訊協定也可使用 <xref:Microsoft.SqlServer.Management.Smo.Endpoint.Protocol%2A> 物件屬性來設定，此屬性會參考 <xref:Microsoft.SqlServer.Management.Smo.Endpoint.ProtocolType%2A> 屬性所指定類型的通訊協定物件。 <xref:Microsoft.SqlServer.Management.Smo.HttpProtocol> 物件需要受限 IP 位址的清單，以及通訊埠、網站和驗證資訊。 <xref:Microsoft.SqlServer.Management.Smo.TcpProtocol> 物件也需要受限 IP 位址的清單和通訊埠資訊。  
  
 在建立和完整地定義端點後，就可以對資料庫使用者、群組、角色和登入等授與、撤銷和拒絕存取權限。  
  
## <a name="example"></a>範例  
 在下列的程式碼範例中，您必須選取用於建立應用程式的程式設計環境、程式設計範本和程式設計語言。 如需詳細資訊，請參閱[在 Visual Studio .net 中建立 VISUAL BASIC SMO 專案](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md)和[在 Visual Studio&#35; .Net 中建立 Visual C SMO 專案](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)。  
  
## <a name="creating-a-database-mirroring-endpoint-service-in-visual-basic"></a>在 Visual Basic 中建立資料庫鏡像端點服務  
 此程式碼範例示範如何在 SMO 中建立資料庫鏡像端點。 您必須先進行這項作業，才能建立資料庫鏡像。 請使用 <xref:Microsoft.SqlServer.Management.Smo.Database.IsMirroringEnabled%2A> 物件上的 <xref:Microsoft.SqlServer.Management.Smo.Database> 和其他屬性建立資料庫鏡像。  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBEndpoints1](SMO How to#SMO_VBEndpoints1)]  -->  
  
## <a name="creating-a-database-mirroring-endpoint-service-in-visual-c"></a>在 Visual C# 中建立資料庫鏡像端點服務  
 此程式碼範例示範如何在 SMO 中建立資料庫鏡像端點。 您必須先進行這項作業，才能建立資料庫鏡像。 請使用 <xref:Microsoft.SqlServer.Management.Smo.Database.IsMirroringEnabled%2A> 物件上的 <xref:Microsoft.SqlServer.Management.Smo.Database> 和其他屬性建立資料庫鏡像。  
  
```csharp
{  
            //Set up a database mirroring endpoint on the server before   
        //setting up a database mirror.   
        //Connect to the local, default instance of SQL Server.   
            Server srv = new Server();  
            //Define an Endpoint object variable for database mirroring.   
            Endpoint ep = default(Endpoint);  
            ep = new Endpoint(srv, "Mirroring_Endpoint");  
            ep.ProtocolType = ProtocolType.Tcp;  
            ep.EndpointType = EndpointType.DatabaseMirroring;  
            //Specify the protocol ports.   
            ep.Protocol.Http.SslPort = 5024;  
            ep.Protocol.Tcp.ListenerPort = 6666;  
            //Specify the role of the payload.   
            ep.Payload.DatabaseMirroring.ServerMirroringRole = ServerMirroringRole.All;  
            //Create the endpoint on the instance of SQL Server.   
            ep.Create();  
            //Start the endpoint.   
            ep.Start();  
            Console.WriteLine(ep.EndpointState);  
        }  
```  
  
## <a name="creating-a-database-mirroring-endpoint-service-in-powershell"></a>在 PowerShell 中建立資料庫鏡像端點服務  
 此程式碼範例示範如何在 SMO 中建立資料庫鏡像端點。 您必須先進行這項作業，才能建立資料庫鏡像。 請使用 <xref:Microsoft.SqlServer.Management.Smo.Database.IsMirroringEnabled%2A> 物件上的 <xref:Microsoft.SqlServer.Management.Smo.Database> 和其他屬性建立資料庫鏡像。  
  
```powershell
# Set the path context to the local, default instance of SQL Server.  
CD \sql\localhost\  
$srv = Get-Item default  
  
#Get a new endpoint to congure and add  
$ep = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Endpoint -argumentlist $srv,"Mirroring_Endpoint"  
  
#Set some properties  
$ep.ProtocolType = [Microsoft.SqlServer.Management.SMO.ProtocolType]::Tcp  
$ep.EndpointType = [Microsoft.SqlServer.Management.SMO.EndpointType]::DatabaseMirroring  
$ep.Protocol.Http.SslPort = 5024  
$ep.Protocol.Tcp.ListenerPort = 6666 #inline comment  
$ep.Payload.DatabaseMirroring.ServerMirroringRole = [Microsoft.SqlServer.Management.SMO.ServerMirroringRole]::All  
  
# Create the endpoint on the instance  
$ep.Create()  
  
# Start the endpoint  
$ep.Start()  
  
# Report its state  
$ep.EndpointState;  
```  
  
## <a name="see-also"></a>請參閱  
 [資料庫鏡像端點 &#40;SQL Server&#41;](../../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)  
