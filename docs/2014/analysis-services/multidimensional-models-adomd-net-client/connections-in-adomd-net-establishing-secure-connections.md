---
title: 建立安全 Connections in ADOMD.NET |Microsoft 文件
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
- connections [ADOMD.NET]
- security [ADOMD.NET]
ms.assetid: b084d447-1456-45a4-8e0e-746c07d7d6fd
caps.latest.revision: 40
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: dd860308d9e4e7f7ed17072572594d6b8aaeeb70
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36032010"
---
# <a name="establishing-secure-connections-in-adomdnet"></a>在 ADOMD.NET 中建立安全連接
  在 ADOMD.NET 中使用連接時，用於連接的安全性方法，端視您呼叫 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.Open%2A> 的 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 方法時所使用的連接字串之 `ProtectionLevel` 屬性值而定。  
  
 `ProtectionLevel` 屬性提供四個層級的安全性：未驗證、驗證、簽署和加密。 下表描述各種安全性層級。  
  
> [!NOTE]  
>  如果選擇使用資料庫連接共用，則資料庫將不會管理安全性。 這是因為資料庫連接共用要求連接字串必須與集區連接一致。 因此，您必須在其他地方管理安全性。  
  
|安全性層級|ProtectionLevel 值|  
|--------------------|---------------------------|  
|*未經驗證的連接*<br /> 未經驗證的連接不會執行任何形式的驗證。 這種連接代表最廣泛支援，但最不安全的連接形式。|`None`|  
|*已驗證的連接*<br /> 未驗證的連接會驗證正在建立連接的使用者，但是不會保護其他通訊的安全。 這種連接非常有用，因為您可以建立使用者的識別或是連接到分析資料來源的應用程式。|`Connect`|  
|*帶正負號的連線*<br /> 簽署的連接會驗證正在要求連接的使用者，並確定不會修改傳輸。 當必須驗證傳輸資料的驗證時，這種連接非常有用。 不過，簽署連接只能防止資料封包的內容免於遭到修改。 在傳輸中仍然可以檢視內容。 **注意：** XML for Analysis 提供者所提供只支援帶正負號的連接[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]。|`Pkt Integrity` 或 `PktIntegrity`|  
|*加密的連接*<br /> 加密的連接是 ADOMD.NET 使用的預設連接類型。 這種連接會驗證正在要求連接的使用者，然後也會加密傳輸的資料。 加密的連接是 ADOMD.NET 可以建立的最安全之連接形式。 無法檢視或修改資料封包的內容，因此可在傳輸期間保護資料。 **注意：** 才支援 XML for Analysis 提供者所提供的加密的連線[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]。|`Pkt Privacy` 或 `PktPrivacy`|  
  
 不過，並非所有的安全性等級都可供所有種類的連接使用。  
  
-   TCP 連接可以使用四個安全性層級的任何一個。 事實上，當您將 TCP 連接與 Windows Integrated Security 搭配使用時，可為連接至分析資料來源提供最安全的方法。  
  
-   HTTP 連接只能是驗證的連接。 因此，必須將 `ProtectionLevel` 屬性設定為 `Connect`。  
  
-   HTTPS 連接只能是加密的連接。 因此，必須將 `ProtectionLevel` 屬性設定為 `Pkt Privacy` 或 `PktPrivacy`。  
  
## <a name="securing-tcp-connections"></a>保護 TCP 連接的安全  
 對於 TCP 連接，`ProtectionLevel` 屬性支援全部四個安全性層級，如下表所示。  
  
|ProtectionLevel 值|是否可與 TCP 連接搭配使用？|結果|  
|---------------------------|------------------------------|-------------|  
|`None`|是|指定未驗證的連接。<br /><br /> TCP 資料流是提供者所要求，但是對於要求資料流的使用者，則是未執行任何形式的驗證。|  
|`Connect`|是|指定驗證的連接。<br /><br /> TCP 資料流是提供者所要求，然後會針對伺服器來驗證要求資料流的使用者之安全性內容：<br /><br /> -如果驗證成功，會不採取其他任何動作。<br />-如果驗證失敗，<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>物件中斷連線多維度資料來源，並擲回例外狀況。<br /><br /> 在驗證成功或是失敗之後，會處置用以驗證連接的安全性內容。|  
|`Pkt Integrity` 或 `PktIntegrity`|是|指定簽署的連接。<br /><br /> TCP 資料流是提供者所要求，然後會針對伺服器來驗證要求資料流的使用者之安全性內容：<br /><br /> -如果驗證成功，<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>物件會關閉現有的 TCP 串流並開啟帶正負號的 TCP 資料流來處理所有要求。 每個對於資料或是中繼資料的要求，都會使用之前用以開啟連接的安全性內容來驗證。 此外，會數位簽署每個封包以確定未使用任何方式來變更 TCP 封包的裝載。<br />-如果驗證失敗，<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>物件中斷連線多維度資料來源，並擲回例外狀況。|  
|`Pkt Privacy` 或 `PktPrivacy`|是|指定加密的連接。 **注意：** 您也可以指定加密的連接不設定`ProtectionLevel`連接字串中的屬性。 <br /><br /> TCP 資料流是提供者所要求，然後會針對伺服器來驗證要求資料流的使用者之安全性內容：<br /><br /> -如果驗證成功，<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>物件會關閉現有的 TCP 串流並開啟加密的 TCP 資料流來處理所有要求。 每個對於資料或是中繼資料的要求，都會使用之前用以開啟連接的安全性內容來驗證。 此外，會使用提供者與多維度資料來源支援的最高加密方法，來加密每個 TCP 封包的裝載。<br />-如果驗證失敗，<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>物件中斷連線多維度資料來源，並擲回例外狀況。|  
  
### <a name="using-windows-integrated-security-for-the-connection"></a>針對連接使用 Windows 整合式安全性  
 Windows 整合式安全性是建立和保護 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體連接最安全的方法。 Windows 整合式安全性不會在驗證處理期間顯示安全性認證，例如使用者名稱或是密碼，但是會改用目前執行的處理序之安全性識別碼來建立識別。 對於大部分的用戶端應用程式，這個安全性識別碼代表目前登入的使用者之識別。  
  
 若要使用 Windows 整合式安全性，連接字串需要下列字串：  
  
-   對於 `Integrated Security` 屬性，可以將此屬性設定為或不設定為 `SSPI`。  
  
    > [!NOTE]  
    >  Windows 整合式安全性只能供 TCP 連接使用，因為 HTTP 連接必須使用 `Basic` 屬性的 `Integrated Security` 設定。  
  
-   對於 `ProtectionLevel` 屬性，將此屬性設定為 `Connect`、`Pkt Integrity` 或 `Pkt Privacy`。  
  
## <a name="securing-http-connections"></a>保護 HTTP 連接的安全  
 HTTPS 和安全通訊端層 (SSL) 可用以在外部保護 HTTP 與分析資料來源的通訊。  
  
 因為 XMLA 提供者只會使用安全的 HTTP，所以在 ADOMD.NET 中的 HTTP 連接必須是簽署的連接，如下表所示。  
  
|ProtectionLevel 值|使用 HTTP 或是 HTTPS|  
|---------------------------|----------------------------|  
|`None`|否|  
|`Connect`|HTTP|  
|`Pkt Integrity` 或 `PktIntegrity`|否|  
|`Pkt Privacy` 或 `PktPrivacy`|HTTPS|  
  
### <a name="opening-a-secure-http-connection"></a>開啟安全的 HTTP 連接  
 下列範例示範如何使用 ADOMD.NET 開啟 `AdventureWorksAS` 範例 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫的 HTTP 連接：  
  
```vb  
Public Function GetAWEncryptedConnection( _  
    Optional ByVal serverName As String = "https:\\localhost\isapy\msmdpump.dll") _  
    As AdomdConnection  
  
    Dim strConnectionString As String = ""  
    Dim objConnection As New AdomdConnection  
  
    Try  
        ' To establish an encrypted connection, set the   
        ' ProtectionLevel setting to PktPrivacy.  
        strConnectionString = "DataSource=" & serverName & ";" & _  
            "Catalog=AdventureWorksAS;" & _  
            "ProtectionLevel=PktPrivacy;"  
  
        ' Note that username and password are not supplied here.  
        ' The current security context is used for authentication  
        ' purposes.  
  
        objConnection.ConnectionString = strConnectionString  
        objConnection.Open()  
    Catch ex As Exception  
        objConnection = Nothing  
        Throw ex  
    Finally  
        ' Return the encrypted connection.  
        GetAWEncryptedConnection = objConnection  
    End Try  
End Function  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [在 ADOMD.NET 中建立連接](connections-in-adomd-net.md)  
  
  