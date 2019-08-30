---
title: 使用 XML 架構 |Microsoft Docs
ms.custom: ''
ms.date: 01/11/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- XML [SMO]
ms.assetid: 9d04de01-efeb-4b2d-8c28-3234bc7ff2f3
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e15ac5d5a028657a8f5ee30c8577d2990b1e31c6
ms.sourcegitcommit: f3f83ef95399d1570851cd1360dc2f072736bef6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/13/2019
ms.locfileid: "70148382"
---
# <a name="using-xml-schemas"></a>使用 XML 結構描述

[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  SMO 中的 XML 程式設計僅限於提供 XML 資料類型、XML 命名空間，以及 XML 資料類型資料行上的簡單索引。  
  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]提供 XML 檔實例的原生儲存區。 XML 結構描述可讓您定義複雜的 XML 資料類型，後者則可用於驗證 XML 文件以確保資料完整性。 XML 結構描述是定義在 <xref:Microsoft.SqlServer.Management.Smo.XmlSchemaCollection> 物件中。  
  
## <a name="example"></a>範例  
 如果要使用所提供的任何程式碼範例，您必須選擇建立應用程式用的程式設計環境、程式設計範本，及程式設計語言。 如需詳細資訊, 請參閱[在 Visual Studio&#35; .Net 中建立 Visual C SMO 專案](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)。  
  
## <a name="creating-an-xml-schema-in-visual-basic"></a>在 Visual Basic 中建立 XML 結構描述  
 此程式碼範例示範如何使用 <xref:Microsoft.SqlServer.Management.Smo.XmlSchemaCollection> 物件來建立 XML 結構描述。 定義 XML 結構描述集合的 <xref:Microsoft.SqlServer.Management.Smo.XmlSchemaCollection.Text%2A> 屬性包含數個雙引號。 這些會由 `chr(34)` 字串取代。  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server()
'Reference the AdventureWorks2012 2008R2 database.
Dim db As Database
db = srv.Databases("AdventureWorks2012")
'Define an XmlSchemaCollection object by supplying the parent database and name arguments in the constructor.
Dim xsc As XmlSchemaCollection
xsc = New XmlSchemaCollection(db, "MySampleCollection")
xsc.Text = "\<schema xmlns=" + Chr(34) + "http://www.w3.org/2001/XMLSchema" + Chr(34) + "  xmlns:ns=" + Chr(34) + "http://ns" + Chr(34) + ">\<element name=" + Chr(34) + "e" + Chr(34) + " type=" + Chr(34) + "dateTime" + Chr(34) + "/></schema>"
'Create the XML schema collection on the instance of SQL Server.
xsc.Create()
```
  
## <a name="creating-an-xml-schema-in-visual-c"></a>在 Visual C# 中建立 XML 結構描述  
 此程式碼範例示範如何使用 <xref:Microsoft.SqlServer.Management.Smo.XmlSchemaCollection> 物件來建立 XML 結構描述。 定義 XML 結構描述集合的 <xref:Microsoft.SqlServer.Management.Smo.XmlSchemaCollection.Text%2A> 屬性包含數個雙引號。 這些會由 `chr(34)` 字串取代。  
  
```csharp  
{  
            //Connect to the local, default instance of SQL Server.   
            Server srv = default(Server);  
            srv = new Server();  
            //Reference the AdventureWorks2012 database.   
            Database db = default(Database);  
            db = srv.Databases["AdventureWorks2012"];  
            //Define an XmlSchemaCollection object by supplying the parent  
            // database and name arguments in the constructor.   
            XmlSchemaCollection xsc = default(XmlSchemaCollection);  
            xsc = new XmlSchemaCollection(db, "MySampleCollection");  
            xsc.Text = "\<schema xmlns=" + Strings.Chr(34) + "http://www.w3.org/2001/XMLSchema" + Strings.Chr(34) + " xmlns:ns=" + Strings.Chr(34) + "http://ns" + Strings.Chr(34) + ">\<element name=" + Strings.Chr(34) + "e" + Strings.Chr(34) + " type=" + Strings.Chr(34) + "dateTime" + Strings.Chr(34) + "/></schema>";  
            //Create the XML schema collection on the instance of SQL Server.   
            xsc.Create();  
        }  
```  
  
## <a name="creating-an-xml-schema-in-powershell"></a>在 PowerShell 中建立 XML 結構描述  
 此程式碼範例示範如何使用 <xref:Microsoft.SqlServer.Management.Smo.XmlSchemaCollection> 物件來建立 XML 結構描述。 定義 XML 結構描述集合的 <xref:Microsoft.SqlServer.Management.Smo.XmlSchemaCollection.Text%2A> 屬性包含數個雙引號。 這些會由 `chr(34)` 字串取代。  
  
```powershell   
#Get a server object which corresponds to the default instance replace LocalMachine with the physical server  
cd \sql\LocalHost  
$srv = get-item default  
  
#Reference the AdventureWorks database.  
$db = $srv.Databases["AdventureWorks2012"]  
  
#Create a new schema collection  
$xsc = New-Object -TypeName Microsoft.SqlServer.Management.SMO.XmlSchemaCollection `  
-argumentlist $db,"MySampleCollection"  
  
#Add the xml  
$dq = '"' # the double quote character  
$xsc.Text = "<schema xmlns=" + $dq + "http://www.w3.org/2001/XMLSchema" + $dq + `  
"  xmlns:ns=" + $dq + "http://ns" + $dq + "><element name=" + $dq + "e" + $dq +`  
 " type=" + $dq + "dateTime" + $dq + "/></schema>"  
  
#Create the XML schema collection on the instance of SQL Server.  
$xsc.Create()  
```  
  
  
