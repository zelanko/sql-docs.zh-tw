---
title: 利用 CommandStream 屬性執行範本檔案 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- Managed Classes [SQLXML], executing template files
- SQLXML Managed Classes, executing template files
- templates [SQLXML], SQLXML Managed Classes
- CommandStream property
ms.assetid: 55c564e3-56d1-4d85-bcaa-703e2905dd57
caps.latest.revision: 21
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: bd8d03627ada894ca93ab354978b154eb0f8c33d
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43099467"
---
# <a name="executing-template-files-by-using-the-commandstream-property"></a>利用 CommandStream 屬性執行範本檔案
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  此範例說明如何指定 SQL 或 XPath 查詢所組成的範本檔案，利用 CommandStream 屬性的 SqlXmlCommand 物件。 在此應用程式，FileStreamobject 會針對命令檔案開啟，而檔案資料流指派為執行 CommandStream。  
  
 在下列範例中，CommandType 屬性會指定為 SqlXmlCommandType.Template （而非作為 TemplateFile)。  
  
 這是 XML 範本範例：  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <sql:query>  
    SELECT TOP 2 ContactID, FirstName, LastName   
    FROM   Person.Contact  
    FOR XML AUTO  
  </sql:query>  
</ROOT>  
```  
  
 這是 C# 應用程式範例。 若要測試應用程式，請儲存範本 (TemplateFile.xml)，然後再執行應用程式。 應用程式會執行在 XML 範本中指定的查詢，並將產生的 XML 文件顯示在螢幕上。  
  
> [!NOTE]  
>  在程式碼中，您必須於連接字串內提供 Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體的名稱。  
  
```  
using System;  
using Microsoft.Data.SqlXml;  
using System.IO;  
  
class Test  
{  
      static string ConnString = "Provider=SQLOLEDB;Server=(local);database=AdventureWorks;Integrated Security=SSPI";  
      public static int testParams()  
      {  
         //Stream strm;  
         MemoryStream ms = new MemoryStream();  
         StreamWriter sw = new StreamWriter(ms);  
         ms.Position = 0;  
         SqlXmlCommand cmd = new SqlXmlCommand(ConnString);  
         cmd.CommandStream = new FileStream("TemplateFile.xml", FileMode.Open, FileAccess.Read);  
         cmd.CommandType = SqlXmlCommandType.Template;  
         using (Stream strm = cmd.ExecuteStream())  
         {  
            using (StreamReader sr = new StreamReader(strm)){  
               Console.WriteLine(sr.ReadToEnd());  
            }  
         }  
         return 0;        
      }  
  
      public static int Main(String[] args)  
      {  
         testParams();     
         return 0;  
      }  
   }  
```  
  
### <a name="to-test-the-application"></a>若要測試應用程式  
  
1.  將這個範例所提供的 XML 範本 (TemplateFile.xml) 儲存在資料夾中。  
  
2.  將此範例中提供的 C# 程式碼 (DocSample.cs) 儲存到儲存結構描述的相同資料夾中  (如果您將檔案儲存在不同的資料夾中，您將需要編輯程式碼，然後為對應的結構描述指定適當的目錄路徑)。  
  
3.  編譯程式碼。 若要在命令提示字元下編譯程式碼，請使用：  
  
    ```  
    csc /reference:Microsoft.Data.SqlXML.dll DocSample.cs  
    ```  
  
     這樣會建立可執行檔 (DocSample.exe)。  
  
4.  在命令提示字元中，執行 DocSample.exe。  
  
  
