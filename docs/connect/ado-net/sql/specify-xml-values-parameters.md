---
title: 將 XML 值指定為參數
description: 示範如何將 XML 資料當做參數傳遞給命令。
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 2c4d08b8-fc29-4614-97fa-29c8ff7ca5b3
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 5ef73529119245397932a3a2414ce65f381b55bd
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452109"
---
# <a name="specifying-xml-values-as-parameters"></a>將 XML 值指定為參數

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[下載 ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

如果查詢需要值為 XML 字串的參數，則開發人員可以使用 **SqlXml** 資料類型的執行個體提供該值。 這其實沒什麼訣竅；SQL Server 中的 XML 資料行接受參數值的方式與其他資料類型完全相同。  
  
## <a name="example"></a>範例  
下列主控台應用程式會在 **AdventureWorks** 資料庫中建立新的資料表。 新資料表包括名為 **SalesID** 的資料行及名為 **SalesInfo** 的 XML 資料行。  
  
> [!NOTE]
>  當您安裝 SQL Server 時，預設不會安裝 **AdventureWorks** 範例資料庫。 您可以執行 SQL Server 安裝程式來安裝它。  
  
此範例會準備 <xref:Microsoft.Data.SqlClient.SqlCommand> 物件，以便在新的資料表中插入資料列。 已儲存的檔案為 **SalesInfo** 資料行提供必要的 XML 資料。  
  
若要建立執行範例所需的檔案，請在與專案相同的資料夾中建立新的文字檔。 將檔案命名為 MyTestStoreData。 在 [記事本] 中開啟檔案，並複製並貼上下列文字：  
  
```xml  
<StoreSurvey xmlns="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/StoreSurvey">  
  <AnnualSales>300000</AnnualSales>  
  <AnnualRevenue>30000</AnnualRevenue>  
  <BankName>International Bank</BankName>  
  <BusinessType>BM</BusinessType>  
  <YearOpened>1970</YearOpened>  
  <Specialty>Road</Specialty>  
  <SquareFeet>7000</SquareFeet>  
  <Brands>3</Brands>  
  <Internet>T1</Internet>  
  <NumberEmployees>2</NumberEmployees>  
</StoreSurvey>  
```  
  
```csharp  
using System;  
using System.Data;  
using Microsoft.Data.SqlClient;  
using System.Xml;  
using System.Data.SqlTypes;  
  
class Class1  
{  
    static void Main()  
    {  
        using (SqlConnection connection = new SqlConnection(GetConnectionString()))  
       {  
        connection.Open();  
        //  Create a sample table (dropping first if it already  
        //  exists.)  
  
        string commandNewTable =   
            "IF EXISTS (SELECT * FROM dbo.sysobjects " +   
            "WHERE id = " +  
                  "object_id(N'[dbo].[XmlDataTypeSample]') " +   
            "AND OBJECTPROPERTY(id, N'IsUserTable') = 1) " +   
            "DROP TABLE [dbo].[XmlDataTypeSample];" +   
            "CREATE TABLE [dbo].[XmlDataTypeSample](" +   
            "[SalesID] [int] IDENTITY(1,1) NOT NULL, " +   
            "[SalesInfo] [xml])";  
        SqlCommand commandAdd =   
                   new SqlCommand(commandNewTable, connection);  
        commandAdd.ExecuteNonQuery();  
        string commandText =   
            "INSERT INTO [dbo].[XmlDataTypeSample] " +   
            "([SalesInfo] ) " +   
            "VALUES(@xmlParameter )";  
        SqlCommand command =   
                  new SqlCommand(commandText, connection);  
  
        //  Read the saved XML document as a   
        //  SqlXml-data typed variable.  
        SqlXml newXml =   
            new SqlXml(new XmlTextReader("MyTestStoreData.xml"));  
  
        //  Supply the SqlXml value for the value of the parameter.  
        command.Parameters.AddWithValue("@xmlParameter", newXml);  
  
        int result = command.ExecuteNonQuery();  
        Console.WriteLine(result + " row was added.");  
        Console.WriteLine("Press Enter to continue.");  
        Console.ReadLine();  
    }  
  }  
  
    private static string GetConnectionString()  
    {  
        // To avoid storing the connection string in your code,              
        // you can retrieve it from a configuration file.   
        return "Data Source=(local);Integrated Security=true;" +  
        "Initial Catalog=AdventureWorks; ";  
    }  
}  
```  
  
## <a name="next-steps"></a>後續步驟
- <xref:System.Data.SqlTypes.SqlXml>
- [SQL Server 中的 XML 資料](xml-data-sql-server.md)
