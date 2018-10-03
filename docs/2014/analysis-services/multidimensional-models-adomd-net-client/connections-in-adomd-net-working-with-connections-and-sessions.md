---
title: 使用 連接和 ADOMD.NET 中的工作階段 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- sessions [ADOMD.NET]
- connections [ADOMD.NET]
ms.assetid: 72b43c06-f3e4-42c3-a696-4a3419c3b884
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 20cb03e5ccc65fe219426ba328501129e8747099
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48050228"
---
# <a name="working-with-connections-and-sessions-in-adomdnet"></a>使用連接和 ADOMD.NET 中的工作階段
  在 XML for Analysis (XMLA) 中，工作階段可支援分析資料存取期間可設定狀態的作業。 工作階段會為分析資料來源界定命令與交易的範圍和內容。 用來管理工作階段的 XMLA 元素是[BeginSession](../xmla/xml-elements-headers/beginsession-element-xmla.md)，[工作階段](../xmla/xml-elements-headers/session-element-xmla.md)，並[EndSession](../xmla/xml-elements-headers/endsession-element-xmla.md)。  
  
 ADOMD.NET 會在您開始工作階段時、在工作階段期間查詢或是擷取資料時，以及關閉工作階段時分別使用這三個 XMLA 工作階段元素。  
  
## <a name="starting-a-session"></a>開始工作階段  
 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.SessionID%2A> 物件的 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 屬性會包含與 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 物件關聯的使用中工作階段之識別碼。 透過正確地使用這個屬性，您可以在應用程式中有效地控制用戶端與伺服器 Statefulness。  
  
-   如果在呼叫 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.SessionID%2A> 方法時，<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.Open%2A> 屬性不是設定為有效的工作階段識別碼，<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 物件會向提供者要求新的工作階段識別碼。 ADOMD.NET 透過將 XMLA `BeginSession` 標頭傳送到提供者，來起始工作階段。 如果 ADOMD.NET 成功啟動工作階段，ADOMD.NET 會將 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.SessionID%2A> 屬性值設定為新建立工作階段的工作階段識別碼。  
  
-   如果在呼叫 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.SessionID%2A> 方法時，<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.Open%2A> 屬性是設定為有效的工作階段識別碼，<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 物件會嘗試連接到指定的工作階段。  
  
 如果 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 物件無法連接到指定的工作階段，或者如果提供者不支援工作階段，就會擲回例外狀況。  
  
> [!NOTE]  
>  在使 ADOMD.NET 建立一個工作階段之後，您可以將多個 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 物件連接到單一使用中工作階段，或者可以從該工作階段中斷連接單一 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 物件，然後將該物件重新連接到另一個工作階段。  
  
## <a name="working-in-a-session"></a>在工作階段中工作  
 ADOMD.NET 將 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 物件連接到有效工作階段之後，會針對應用程式所提出的每個資料或中繼資料要求，將 XMLA `Session` 標頭傳送到提供者。 每個要求會將工作階段識別碼設定成 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.SessionID%2A> 屬性的值。  
  
 工作階段識別碼並不保證工作階段會維持有效狀態。 如果工作階段到期 (例如，如果工作階段逾時或是喪失連接)，提供者可以選擇結束和回復該工作階段的動作。 如果發生這個情況，所有之後從 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 物件呼叫的方法都將擲回例外狀況。 因為只有在下一個要求傳送到提供者時才會擲回例外狀況，而不是在工作階段到期時，所以您的應用程式從提供者擷取資料或中繼資料的期間，必須能夠隨時處理這些例外狀況。  
  
## <a name="closing-a-session"></a>關閉工作階段  
 如果<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.Close%2A>方法在未指定的值呼叫*endSession*參數，或如果*endSession*參數設為 True，這兩個連接到工作階段和工作階段與相關聯<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>物件會關閉。 為了關閉工作階段，ADOMD.NET 會將 XMLA `EndSession` 標頭傳送到提供者，並將工作階段識別碼設定為 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.SessionID%2A> 屬性的值。  
  
 如果<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.Close%2A>方法呼叫*endSession*參數設定為 False 時，相關聯的工作階段<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>物件會保持作用，但在關閉工作階段的連接。  
  
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
  
## <a name="see-also"></a>另請參閱  
 [在 ADOMD.NET 中建立連接](connections-in-adomd-net.md)  
  
  
