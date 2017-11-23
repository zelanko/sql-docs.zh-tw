---
title: "使用 連接和 ADOMD.NET 中的工作階段 |Microsoft 文件"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- sessions [ADOMD.NET]
- connections [ADOMD.NET]
ms.assetid: 72b43c06-f3e4-42c3-a696-4a3419c3b884
caps.latest.revision: "35"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 061a51539b40630874e36096cc59557ac375c671
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="connections-in-adomdnet---working-with-connections-and-sessions"></a>Connections in ADOMD.NET-使用連接與工作階段
  在 XML for Analysis (XMLA) 中，工作階段可支援分析資料存取期間可設定狀態的作業。 工作階段會為分析資料來源界定命令與交易的範圍和內容。 用來管理工作階段的 XMLA 元素[BeginSession](../../analysis-services/xmla/xml-elements-headers/beginsession-element-xmla.md)，[工作階段](../../analysis-services/xmla/xml-elements-headers/session-element-xmla.md)，和[EndSession](../../analysis-services/xmla/xml-elements-headers/endsession-element-xmla.md)。  
  
 ADOMD.NET 會在您開始工作階段時、在工作階段期間查詢或是擷取資料時，以及關閉工作階段時分別使用這三個 XMLA 工作階段元素。  
  
## <a name="starting-a-session"></a>開始工作階段  
 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.SessionID%2A> 物件的 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 屬性會包含與 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 物件關聯的使用中工作階段之識別碼。 透過正確地使用這個屬性，您可以在應用程式中有效地控制用戶端與伺服器 Statefulness。  
  
-   如果在呼叫 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.SessionID%2A> 方法時，<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.Open%2A> 屬性不是設定為有效的工作階段識別碼，<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 物件會向提供者要求新的工作階段識別碼。 ADOMD.NET 初始化工作階段傳送 XMLA **BeginSession**標頭給提供者。 如果 ADOMD.NET 成功啟動工作階段，ADOMD.NET 會將 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.SessionID%2A> 屬性值設定為新建立工作階段的工作階段識別碼。  
  
-   如果在呼叫 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.SessionID%2A> 方法時，<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.Open%2A> 屬性是設定為有效的工作階段識別碼，<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 物件會嘗試連接到指定的工作階段。  
  
 如果 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 物件無法連接到指定的工作階段，或者如果提供者不支援工作階段，就會擲回例外狀況。  
  
> [!NOTE]  
>  在使 ADOMD.NET 建立一個工作階段之後，您可以將多個 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 物件連接到單一使用中工作階段，或者可以從該工作階段中斷連接單一 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 物件，然後將該物件重新連接到另一個工作階段。  
  
## <a name="working-in-a-session"></a>在工作階段中工作  
 ADOMD.NET 連線後<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>物件有效的工作階段，ADOMD.NET 會將傳送 XMLA**工作階段**之提供者的資料或中繼資料應用程式所提出的每一個要求標頭。 每個要求會將工作階段識別碼設定成 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.SessionID%2A> 屬性的值。  
  
 工作階段識別碼並不保證工作階段會維持有效狀態。 如果工作階段到期 (例如，如果工作階段逾時或是喪失連接)，提供者可以選擇結束和回復該工作階段的動作。 如果發生這個情況，所有之後從 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 物件呼叫的方法都將擲回例外狀況。 因為只有在下一個要求傳送到提供者時才會擲回例外狀況，而不是在工作階段到期時，所以您的應用程式從提供者擷取資料或中繼資料的期間，必須能夠隨時處理這些例外狀況。  
  
## <a name="closing-a-session"></a>關閉工作階段  
 如果<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.Close%2A>呼叫方法時沒有指定的值*endSession*參數，或如果*endSession*參數設定為 True，工作階段和工作階段連線與相關聯<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>物件已關閉。 若要關閉工作階段，ADOMD.NET 會將傳送 XMLA **EndSession**提供者，與工作階段識別碼的標頭設定的值為<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.SessionID%2A>屬性。  
  
 如果<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.Close%2A>方法呼叫*endSession*參數設定為 False，與相關聯的工作階段<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>物件會保持使用中，但在關閉工作階段的連接。  
  
## <a name="example-of-managing-a-session"></a>管理工作階段的範例  
 下列程式碼範例示範如何在 ADOMD.NET 中開啟連接、建立工作階段，以及在保持工作階段開啟的同時關閉連接。  
  
```vb  
Public Function CreateSession(ByVal connectionString As String) As String  
    Dim strSessionID As String = ""  
    Dim objConnection As New AdomdConnection  
  
    Try  
        ' First, try to connect to the specified data source.  
        ' If the connection string is not valid, or if the specified  
        ' provider does not support sessions, an exception is thrown.  
        objConnection.ConnectionString = connectionString  
        objConnection.Open()  
  
        ' Now that the connection is open, retrieve the new  
        ' active session ID.  
        strSessionID = objConnection.SessionID  
        ' Close the connection, but leave the session open.  
        objConnection.Close(False)  
        Return strSessionID  
  
    Finally  
        objConnection = Nothing  
    End Try  
End Function  
```  
  
```csharp  
static string CreateSession(string connectionString)  
{  
    string strSessionID = "";  
    AdomdConnection objConnection = new AdomdConnection();  
    try  
    {  
        /*First, try to connect to the specified data source.  
          If the connection string is not valid, or if the specified  
          provider does not support sessions, an exception is thrown. */  
        objConnection.ConnectionString = connectionString;  
        objConnection.Open();  
  
        // Now that the connection is open, retrieve the new  
        // active session ID.  
        strSessionID = objConnection.SessionID;  
        // Close the connection, but leave the session open.  
        objConnection.Close(false);  
        return strSessionID;  
    }  
    finally  
    {  
        objConnection = null;  
    }  
}  
```  
  
## <a name="see-also"></a>請參閱＜  
 [在 ADOMD.NET 中建立連接](../../analysis-services/multidimensional-models-adomd-net-client/connections-in-adomd-net.md)  
  
  
