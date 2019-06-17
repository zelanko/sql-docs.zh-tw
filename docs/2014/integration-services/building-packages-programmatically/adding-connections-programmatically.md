---
title: 以程式設計方式新增連線 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- connection managers [Integration Services], packages
- Integration Services packages, connections
- connections [Integration Services], packages
- SSIS packages, connections
- packages [Integration Services], connections
- intrinsic properties [Integration Services]
- SQL Server Integration Services packages, connections
- ConnectionManager class
- SSIS connection managers
- adding package connections
ms.assetid: d90716d1-4c65-466c-b82c-4aabbee1e3e5
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b1258797d76df49a2622335ee798120632706c78
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62772219"
---
# <a name="adding-connections-programmatically"></a>以程式設計方式加入連接
  <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 類別代表外部資料來源的實體連接。 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 類別會將連接的實作詳細資料與執行階段隔離。 這可讓執行階段使用一致且可預測的方式與每個連接管理員互動。 連接管理員包含一組所有連接共有的內建屬性，例如 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.Name%2A>、<xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.ID%2A>、<xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.Description%2A> 以及 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.ConnectionString%2A>。 不過，<xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.ConnectionString%2A> 與 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.Name%2A> 屬性通常是唯一需要設定連接管理員的屬性。 與其他程式設計範例不同的是，連接類別會公開像是 `Open` 或 `Connect` 等方法，以實體建立連至資料來源的連接，執行階段引擎則會在執行時管理封裝的所有連接。  
  
 <xref:Microsoft.SqlServer.Dts.Runtime.Connections> 類別是一種已經加入該封裝的連接管理員集合，而且可供在執行階段使用。 您可以使用集合的 <xref:Microsoft.SqlServer.Dts.Runtime.Connections.Add%2A> 方法，並提供指出連接管理員類型的字串，將更多的連接管理員加入集合。 <xref:Microsoft.SqlServer.Dts.Runtime.Connections.Add%2A> 方法會傳回加入封裝的 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 執行個體。  
  
## <a name="intrinsic-properties"></a>內建屬性  
 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 類別會公開一組所有連接都共有的屬性。 然而，有時您需要存取特定連接類型特有的屬性。 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.Properties%2A> 類別的 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 集合提供這些屬性的存取權。 可以使用索引子或是屬性名稱以及 **GetValue** 方法，從集合擷取屬性，並且會使用 **SetValue** 方法來設定值。 基礎連接物件屬性的屬性也可以透過取得物件的實際執行個體以及直接設定其屬性來設定。 若要取得基礎連接，請使用連接管埋員的 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.InnerObject%2A> 屬性。 下列程式碼行顯示以 C# 撰寫的程式碼，將建立具有基礎類別 <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.ConnectionManagerAdoNetClass> 的 ADO.NET 連接管理員。  
  
 `ConnectionManagerAdoNetClass cmado = cm.InnerObject as ConnectionManagerAdoNet;`  
  
 這會將 Managed 連接管理員物件轉換為它的基礎連接物件。 如果您是使用 C++，會呼叫 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 物件的 `QueryInterface` 方法，而且會要求基礎連接物件的介面。  
  
 下表列出包含在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 中的連接管理員。 以及用在 `package.Connections.Add("xxx")` 陳述式中的字串。 如需所有連線管理員的清單，請參閱 [Integration Services &#40;SSIS&#41; 連線](../connection-manager/integration-services-ssis-connections.md)。  
  
|String|[ODBC 來源編輯器]|  
|------------|------------------------|  
|"OLEDB"|OLE DB 連接的連接管理員。|  
|"ODBC"|ODBC 連接的連接管理員。|  
|"ADO"|ADO 連接的連接管理員。|  
|"ADO.NET:SQL"|ADO.NET (SQL 資料提供者) 連接的連接管理員。|  
|"ADO.NET:OLEDB"|ADO.NET (OLE DB 資料提供者) 連接的連接管理員。|  
|"FLATFILE"|一般檔案連接的連接管理員。|  
|"FILE"|檔案連接的連接管理員。|  
|"MULTIFLATFILE"|多個一般檔案連接的連接管理員。|  
|"MULTIFILE"|多個一般檔案連接的連接管理員。|  
|"SQLMOBILE"|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 連線的連線管理員。|  
|"MSOLAP100"|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 連接的連接管理員。|  
|"FTP"|FTP 連接的連接管理員。|  
|"HTTP"|HTTP 連接的連接管理員。|  
|"MSMQ"|Message Queuing (又稱為 MSMQ) 連接的連接管理員。|  
|"SMTP"|SMTP 連接的連接管理員。|  
|"WMI"|Microsoft Windows Management Instrumentation (WMI) 連接的連接管理員。|  
  
 下列程式碼範例示範將 OLE DB 與 FILE 連接加入 <xref:Microsoft.SqlServer.Dts.Runtime.Package.Connections%2A> 的 <xref:Microsoft.SqlServer.Dts.Runtime.Package> 集合。 範例接著會設定 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.ConnectionString%2A>、<xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.Name%2A> 與 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.Description%2A> 屬性。  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      // Create a package, and retrieve its connections.  
      Package pkg = new Package();  
      Connections pkgConns = pkg.Connections;  
  
      // Add an OLE DB connection to the package, using the   
      // method defined in the AddConnection class.  
      CreateConnection myOLEDBConn = new CreateConnection();  
      myOLEDBConn.CreateOLEDBConnection(pkg);  
  
      // View the new connection in the package.  
      Console.WriteLine("Connection description: {0}",  
         pkg.Connections["SSIS Connection Manager for OLE DB"].Description);  
  
      // Add a second connection to the package.  
      CreateConnection myFileConn = new CreateConnection();  
      myFileConn.CreateFileConnection(pkg);  
  
      // View the second connection in the package.  
      Console.WriteLine("Connection description: {0}",  
        pkg.Connections["SSIS Connection Manager for Files"].Description);  
  
      Console.WriteLine();  
      Console.WriteLine("Number of connections in package: {0}", pkg.Connections.Count);  
  
      Console.Read();  
    }  
  }  
  // <summary>  
  // This class contains the definitions for multiple  
  // connection managers.  
  // </summary>  
  public class CreateConnection  
  {  
    // Private data.  
    private ConnectionManager ConMgr;  
  
    // Class definition for OLE DB Provider.  
    public void CreateOLEDBConnection(Package p)  
    {  
      ConMgr = p.Connections.Add("OLEDB");  
      ConMgr.ConnectionString = "Provider=SQLOLEDB.1;" +  
        "Integrated Security=SSPI;Initial Catalog=AdventureWorks;" +  
        "Data Source=(local);";  
      ConMgr.Name = "SSIS Connection Manager for OLE DB";  
      ConMgr.Description = "OLE DB connection to the AdventureWorks database.";  
    }  
    public void CreateFileConnection(Package p)  
    {  
      ConMgr = p.Connections.Add("File");  
      ConMgr.ConnectionString = @"\\<yourserver>\<yourfolder>\books.xml";  
      ConMgr.Name = "SSIS Connection Manager for Files";  
      ConMgr.Description = "Flat File connection";  
    }  
  }  
  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
  
Module Module1  
  
  Sub Main()  
  
    ' Create a package, and retrieve its connections.  
    Dim pkg As New Package()  
    Dim pkgConns As Connections = pkg.Connections  
  
    ' Add an OLE DB connection to the package, using the   
    ' method defined in the AddConnection class.  
    Dim myOLEDBConn As New CreateConnection()  
    myOLEDBConn.CreateOLEDBConnection(pkg)  
  
    ' View the new connection in the package.  
    Console.WriteLine("Connection description: {0}", _  
      pkg.Connections("SSIS Connection Manager for OLE DB").Description)  
  
    ' Add a second connection to the package.  
    Dim myFileConn As New CreateConnection()  
    myFileConn.CreateFileConnection(pkg)  
  
    ' View the second connection in the package.  
    Console.WriteLine("Connection description: {0}", _  
      pkg.Connections("SSIS Connection Manager for Files").Description)  
  
    Console.WriteLine()  
    Console.WriteLine("Number of connections in package: {0}", pkg.Connections.Count)  
  
    Console.Read()  
  
  End Sub  
  
End Module  
  
' This class contains the definitions for multiple  
' connection managers.  
  
Public Class CreateConnection  
  ' Private data.  
  Private ConMgr As ConnectionManager  
  
  ' Class definition for OLE DB provider.  
  Public Sub CreateOLEDBConnection(ByVal p As Package)  
    ConMgr = p.Connections.Add("OLEDB")  
    ConMgr.ConnectionString = "Provider=SQLOLEDB.1;" & _  
      "Integrated Security=SSPI;Initial Catalog=AdventureWorks;" & _  
      "Data Source=(local);"  
    ConMgr.Name = "SSIS Connection Manager for OLE DB"  
    ConMgr.Description = "OLE DB connection to the AdventureWorks database."  
  End Sub  
  
  Public Sub CreateFileConnection(ByVal p As Package)  
    ConMgr = p.Connections.Add("File")  
    ConMgr.ConnectionString = "\\<yourserver>\<yourfolder>\books.xml"  
    ConMgr.Name = "SSIS Connection Manager for Files"  
    ConMgr.Description = "Flat File connection"  
  End Sub  
  
End Class  
```  
  
 **範例輸出：**  
  
 `Connection description: OLE DB connection to the AdventureWorks database.`  
  
 `Connection description: OLE DB connection to the AdventureWorks database.`  
  
 `Number of connections in package: 2`  
  
## <a name="external-resources"></a>外部資源  
 carlprothman.net 上的技術文章：[連接字串](https://go.microsoft.com/fwlink/?LinkId=220743)。  
  
![Integration Services 圖示 （小）](../media/dts-16.gif "Integration Services 圖示 （小）")**保持最多包含 Integration Services 的日期**<br /> 若要取得 Microsoft 的最新下載、文件、範例和影片以及社群中的精選解決方案，請瀏覽 MSDN 上的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 頁面：<br /><br /> [瀏覽 MSDN 上的 Integration Services 頁面](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要得到這些更新的自動通知，請訂閱該頁面上所提供的 RSS 摘要。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services &#40;SSIS&#41; 連線](../connection-manager/integration-services-ssis-connections.md)   
 [建立連線管理員](../create-connection-managers.md)  
  
  
