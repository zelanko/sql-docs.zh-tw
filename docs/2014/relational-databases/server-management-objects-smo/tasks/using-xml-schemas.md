---
title: 使用 XML 結構描述 |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- XML [SMO]
ms.assetid: 9d04de01-efeb-4b2d-8c28-3234bc7ff2f3
caps.latest.revision: 38
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: f59dd029b5dc0311323efa85c852c611d787b894
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36036328"
---
# <a name="using-xml-schemas"></a>使用 XML 結構描述
  SMO 中的 XML 程式設計僅限於提供 XML 資料類型、XML 命名空間，以及 XML 資料類型資料行上的簡單索引。  
  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 針對 XML 文件執行個體提供原生儲存。 XML 結構描述可讓您定義複雜的 XML 資料類型，後者則可用於驗證 XML 文件以確保資料完整性。 XML 結構描述是定義在 <xref:Microsoft.SqlServer.Management.Smo.XmlSchemaCollection> 物件中。  
  
## <a name="example"></a>範例  
 如果要使用所提供的任何程式碼範例，您必須選擇建立應用程式用的程式設計環境、程式設計範本，及程式設計語言。 如需詳細資訊，請參閱[Visual Studio.NET 中建立 Visual Basic SMO 專案](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md)或[建立 Visual C&#35; SMO Project in Visual Studio](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)。  
  
## <a name="creating-an-xml-schema-in-visual-basic"></a>在 Visual Basic 中建立 XML 結構描述  
 此程式碼範例示範如何使用 <xref:Microsoft.SqlServer.Management.Smo.XmlSchemaCollection> 物件來建立 XML 結構描述。 定義 XML 結構描述集合的 <xref:Microsoft.SqlServer.Management.Smo.XmlSchemaCollection.Text%2A> 屬性包含數個雙引號。 這些會由 `chr(34)` 字串取代。  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBXMLSchema1](SMO How to#SMO_VBXMLSchema1)]  -->  
  
## <a name="creating-an-xml-schema-in-visual-c"></a>在 Visual C# 中建立 XML 結構描述  
 此程式碼範例示範如何使用 <xref:Microsoft.SqlServer.Management.Smo.XmlSchemaCollection> 物件來建立 XML 結構描述。 定義 XML 結構描述集合的 <xref:Microsoft.SqlServer.Management.Smo.XmlSchemaCollection.Text%2A> 屬性包含數個雙引號。 這些會由 `chr(34)` 字串取代。  
  
```  
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
            xsc.Text = "<schema xmlns=" + Strings.Chr(34) + "http://www.w3.org/2001/XMLSchema" + Strings.Chr(34) + " xmlns:ns=" + Strings.Chr(34) + "http://ns" + Strings.Chr(34) + "><element name=" + Strings.Chr(34) + "e" + Strings.Chr(34) + " type=" + Strings.Chr(34) + "dateTime" + Strings.Chr(34) + "/></schema>";  
            //Create the XML schema collection on the instance of SQL Server.   
            xsc.Create();  
        }  
```  
  
## <a name="creating-an-xml-schema-in-powershell"></a>在 PowerShell 中建立 XML 結構描述  
 此程式碼範例示範如何使用 <xref:Microsoft.SqlServer.Management.Smo.XmlSchemaCollection> 物件來建立 XML 結構描述。 定義 XML 結構描述集合的 <xref:Microsoft.SqlServer.Management.Smo.XmlSchemaCollection.Text%2A> 屬性包含數個雙引號。 這些會由 `chr(34)` 字串取代。  
  
```  
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
  
  