---
title: 存取.NET 環境中的 SQLXML 功能 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- Managed Classes [SQLXML], accessing SQLXML functionality
- SQLXML Managed Classes, accessing SQLXML functionality
- DiffGrams [SQLXML], accessing SQLXML functionality
- .NET Framework [SQLXML], accessing SQLXML functionality
ms.assetid: 74744535-2945-414d-9a5b-7e8cc363953a
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5c13c4b05a0443db4df711f8522e8ad57e1433c2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47823516"
---
# <a name="accessing-sqlxml-functionality-in-the-net-environment"></a>存取 .NET 環境中的 SQLXML 功能
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  此範例顯示：  
  
-   如何使用[!INCLUDE[msCoName](../../../includes/msconame-md.md)]SQLXML Managed 類別 (Microsoft.Data.SqlXml) 來存取 Microsoft[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]在[!INCLUDE[msCoName](../../../includes/msconame-md.md)].NET Framework 環境。  
  
-   在 .NET Framework 環境中產生的 DiffGrams 如何將資料更新套用到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料表。  
  
 在此應用程式中，XPath 查詢會根據 XSD 結構描述執行。 執行 XPath 查詢會傳回包含連絡人資料的 XML 文件 (**FirstName**， **LastName**)。 應用程式會將 XML 文件載入到 .NET Framework 環境的資料集中。 資料集中的資料已修改：連絡人的名字會變更為 "Susan"，成為資料集中的第一個連絡人。 DiffGram 會從資料集產生，然後會將 DiffGram (員工名字的變更) 中指定的更新套用到 Person.Contact 資料表。  
  
> [!NOTE]  
>  在程式碼中，您必須於連接字串內提供 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體的名稱。  
  
```  
using System;  
using System.Data;  
using Microsoft.Data.SqlXml;  
using System.IO;  
class Test  
{  
   static string ConnString = "Provider=SQLOLEDB;Server=SqlServerName;database=AdventureWorks;Integrated Security=SSPI;";  
   public static int testParams()  
   {  
      DataRow row;  
      SqlXmlAdapter ad;  
      //need a memory stream to hold diff gram temporarily  
      MemoryStream ms = new MemoryStream();  
      SqlXmlCommand cmd = new SqlXmlCommand(ConnString);  
      cmd.RootTag = "ROOT";  
      cmd.CommandText = "Con";  
      cmd.CommandType = SqlXmlCommandType.XPath;  
      cmd.SchemaPath = "MySchema.xml";  
      //load data set  
      DataSet ds = new DataSet();  
      ad = new SqlXmlAdapter(cmd);  
      ad.Fill(ds);  
      row = ds.Tables["Con"].Rows[0];  
      row["FName"] = "Susan";  
      ad.Update(ds);  
      return 0;  
   }  
   public static int Main(String[] args)  
   {  
      testParams();  
      return 0;  
   }  
}  
```  
  
 **若要測試的範例：**  
  
 若要測試此範例，您必須先在電腦上安裝 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework。  
  
1.  將這個 XSD 結構描述 (MySchema.xml) 儲存在資料夾中：  
  
    ```  
    <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
                xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
      <xsd:element name="Con" sql:relation="Person.Contact" >  
       <xsd:complexType>  
         <xsd:sequence>  
            <xsd:element name="FName"    
                         sql:field="FirstName"   
                         type="xsd:string" />   
            <xsd:element name="LName"    
                         sql:field="LastName"    
                         type="xsd:string" />  
         </xsd:sequence>  
         <xsd:attribute name="ContactID" type="xsd:integer" />  
        </xsd:complexType>  
      </xsd:element>  
    </xsd:schema>  
    ```  
  
2.  將此範例中提供的 C# 程式碼 (DocSample.cs) 儲存到儲存結構描述的相同資料夾中  (如果您將檔案儲存在不同的資料夾中，您將需要編輯程式碼，然後為對應的結構描述指定適當的目錄路徑)。  
  
3.  編譯程式碼。 若要在命令提示字元下編譯程式碼，請使用：  
  
    ```  
    csc /reference:Microsoft.Data.SqlXML.dll DocSample.cs  
    ```  
  
     這樣會建立可執行檔 (DocSample.exe)。  
  
 在命令提示字元中，執行 DocSample.exe。  
  
  
