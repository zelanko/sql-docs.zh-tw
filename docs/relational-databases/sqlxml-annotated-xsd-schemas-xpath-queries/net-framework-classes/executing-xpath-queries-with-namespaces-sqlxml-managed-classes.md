---
title: 執行含有命名空間的 XPath 查詢 (SQLXML Managed 類別) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- namespaces property
- XPath queries [SQLXML], SQLXML Managed Classes
- queries [SQLXML], SQLXML Managed Classes
- XPath queries [SQLXML], namespaces
- Managed Classes [SQLXML], executing XPath queries
- SQLXML Managed Classes, executing XPath queries
- namespaces [SQLXML], XPath queries
ms.assetid: c6fc46d8-6b42-4992-a8f1-a8d4b8886e6e
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ee8abb015ab4dab9606c7f81cb86f712bf23ec54
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47785158"
---
# <a name="executing-xpath-queries-with-namespaces-sqlxml-managed-classes"></a>執行含有命名空間的 XPath 查詢 (SQLXML Managed 類別)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  XPath 查詢可以包含命名空間。 如果結構描述元素會限定命名空間 (使用目標命名空間)，針對此結構描述進行的 XPath 查詢就必須指定此命名空間。  
  
 由於 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML 4.0 不支援萬用字元 (*)，所以您必須使用命名空間前置詞來指定 XPath 查詢。 若要解析此前置詞，使用命名空間屬性來指定命名空間繫結。  
  
 在下列範例中，XPath 查詢，請指定使用萬用字元的命名空間 (\*) 和 local-name （) and namespace-uri （) XPath 函式。 此 XPath 查詢會傳回所有項目所在的區域名稱**員工**和命名空間 uri **urn: myschema:Contacts**:  
  
```  
/*[local-name() = 'Contact' and namespace-uri() = 'urn:myschema:Contacts']  
```  
  
 在 SQLXML 4.0 中，使用命名空間前置詞來指定這個 XPath 查詢。 例如， **x: Contact**，其中**x**是命名空間前置詞。 請考慮下列 XSD 結構描述：  
  
```  
<schema xmlns="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema"  
            xmlns:con="urn:myschema:Contacts"  
            targetNamespace="urn:myschema:Contacts">  
<complexType name="ContactType">  
  <attribute name="CID" sql:field="ContactID" type="ID"/>  
  <attribute name="FName" sql:field="FirstName" type="string"/>  
  <attribute name="LName" sql:field="LastName"/>   
</complexType>  
<element name="Contact" type="con:ContactType" sql:relation="Person.Contact"/>  
</schema>  
```  
  
 由於這個結構描述會定義目標命名空間，所以針對此結構描述進行的 XPath 查詢 (例如 "Employee") 必須包含該命名空間。  
  
 下列 C# 範例應用程式會針對先前的 XSD 結構描述 (MySchema.xml) 執行 XPath 查詢。 若要解析此前置詞，請使用 SqlXmlCommand 物件的命名空間屬性以指定的命名空間繫結。  
  
> [!NOTE]  
>  在程式碼中，您必須於連接字串內提供 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體的名稱。  
  
```  
using System;  
using Microsoft.Data.SqlXml;  
using System.IO;  
class Test  
{  
      static string ConnString = "Provider=SQLOLEDB;Server=(local);database=AdventureWorks;Integrated Security=SSPI";  
      public static int testXPath()  
      {  
         //Stream strm;  
         SqlXmlCommand cmd = new SqlXmlCommand(ConnString);  
         cmd.CommandText = "x:Contact[@CID='1']";  
         cmd.CommandType = SqlXmlCommandType.XPath;  
         cmd.RootTag = "ROOT";  
         cmd.Namespaces = "xmlns:x='urn:myschema:Contacts'";  
         cmd.SchemaPath = "MySchema.xml";  
         using (Stream strm = cmd.ExecuteStream()){  
            using (StreamReader sr = new StreamReader(strm)){  
               Console.WriteLine(sr.ReadToEnd());  
            }  
         }  
         return 0;  
      }  
      public static int Main(String[] args)  
      {  
         testXPath();  
         return 0;  
      }  
   }  
```  
  
 若要測試此範例，您必須先在電腦上安裝 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework。  
  
### <a name="to-test-the-application"></a>若要測試應用程式  
  
1.  將這個範例所提供的 XSD 結構描述 (MySchema.xml) 儲存在資料夾中。  
  
2.  將此範例中提供的 C# 程式碼 (DocSample.cs) 儲存到儲存結構描述的相同資料夾中  (如果您將檔案儲存在不同的資料夾中，您將需要編輯程式碼，然後為對應的結構描述指定適當的目錄路徑)。  
  
3.  編譯程式碼。 若要在命令提示字元下編譯程式碼，請使用：  
  
    ```  
    csc /reference:Microsoft.Data.SqlXML.dll DocSample.cs  
    ```  
  
     這樣會建立可執行檔 (DocSample.exe)。  
  
4.  在命令提示字元中，執行 DocSample.exe。  
  
  
