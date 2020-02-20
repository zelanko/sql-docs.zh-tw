---
title: 步驟 3：使用 ADO.NET 連線到 SQL 的概念證明 | Microsoft Docs
description: 包含用來連線到 SQL Server、執行查詢及插入資料列的 C# 程式碼範例。
ms.custom: ''
ms.date: 08/15/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: v-kaywon
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: aebe3dc6-3ee4-4d11-8e43-5d32b3f91490
author: rothja
ms.author: jroth
ms.openlocfilehash: cff776c4881dcc012a825bcd48f6d6271b95bb75
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "75247522"
---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-adonet"></a>步驟 3：使用 ADO.NET 連線到 SQL 的概念證明

![Download-DownArrow-Circled](../../ssdt/media/download.png)[下載 ADO.NET](../sql-connection-libraries.md#anchor-20-drivers-relational-access)

- 上一篇文章：&nbsp;&nbsp;&nbsp;[步驟 2：建立用於 ADO.NET 開發的 SQL 資料庫](step-2-create-sql-database-ado-net-development.md)  
- 下一篇文章：&nbsp;&nbsp;&nbsp;[步驟 4：使用 ADO.NET 復原連線到 SQL](step-4-connect-resiliently-sql-ado-net.md)  

  
這個 C# 程式碼範例只應被視為一個概念證明。 為了清楚起見，已將範例程式碼簡化，而其不一定代表 Microsoft 建議的最佳做法。  
  
## <a name="step-1-connect"></a>步驟 1:連線
  
**SqlConnection.Open** 方法可用來連線到您的 SQL 資料庫。  


```csharp
// C# , ADO.NET  
using System;
using QC = Microsoft.Data.SqlClient;  // System.Data.dll  
  
namespace ProofOfConcept_SQL_CSharp  
{  
    public class Program  
    {  
        static public void Main()  
        {  
            using (var connection = new QC.SqlConnection(  
                "Server=tcp:YOUR_SERVER_NAME_HERE.database.windows.net,1433;" +
                "Database=AdventureWorksLT;User ID=YOUR_LOGIN_NAME_HERE;" +
                "Password=YOUR_PASSWORD_HERE;Encrypt=True;" +
                "TrustServerCertificate=False;Connection Timeout=30;"  
                ))  
            {  
                connection.Open();  
                Console.WriteLine("Connected successfully.");  

                Console.WriteLine("Press any key to finish...");  
                Console.ReadKey(true);  
            }  
        }  
    }  
}  
/**** Actual output:  
Connected successfully.  
Press any key to finish...  
****/  
```  


## <a name="step-2-execute-a-query"></a>步驟 2:執行查詢  
  
SqlCommand. ExecuteReader 方法：  
  
- 向 SQL 系統發出 SQL SELECT 陳述式。  
- 傳回 SqlDataReader 的執行個體，以提供對結果資料列的存取。  
  
  
  
```csharp
using System;  // C# , ADO.NET  
using DT = System.Data;            // System.Data.dll  
using QC = Microsoft.Data.SqlClient;  // System.Data.dll  
  
namespace ProofOfConcept_SQL_CSharp  
{  
    public class Program  
    {  
        static public void Main()  
        {  
            using (var connection = new QC.SqlConnection(  
                "Server=tcp:YOUR_SERVER_NAME_HERE.database.windows.net,1433;" +
                "Database=AdventureWorksLT;User ID=YOUR_LOGIN_NAME_HERE;" +
                "Password=YOUR_PASSWORD_HERE;Encrypt=True;" +
                "TrustServerCertificate=False;Connection Timeout=30;"  
                ))  
            {  
                connection.Open();  
                Console.WriteLine("Connected successfully.");  
  
                Program.SelectRows(connection);  
  
                Console.WriteLine("Press any key to finish...");  
                Console.ReadKey(true);  
            }  
        }  
  
        static public void SelectRows(QC.SqlConnection connection)  
        {  
            using (var command = new QC.SqlCommand())  
            {  
                command.Connection = connection;  
                command.CommandType = DT.CommandType.Text;  
                command.CommandText = @"  
SELECT  
    TOP 5  
        COUNT(soh.SalesOrderID) AS [OrderCount],  
        c.CustomerID,  
        c.CompanyName  
    FROM  
                        SalesLT.Customer         AS c  
        LEFT OUTER JOIN SalesLT.SalesOrderHeader AS soh  
            ON c.CustomerID = soh.CustomerID  
    GROUP BY  
        c.CustomerID,  
        c.CompanyName  
    ORDER BY  
        [OrderCount] DESC,  
        c.CompanyName; ";  
  
                QC.SqlDataReader reader = command.ExecuteReader();  
  
                while (reader.Read())  
                {  
                    Console.WriteLine("{0}\t{1}\t{2}",  
                        reader.GetInt32(0),  
                        reader.GetInt32(1),  
                        reader.GetString(2));  
                }  
            }  
        }  
    }  
}  
/**** Actual output:  
Connected successfully.  
1       29736   Action Bicycle Specialists  
1       29638   Aerobic Exercise Company  
1       29546   Bulk Discount Store  
1       29741   Central Bicycle Specialists  
1       29612   Channel Outlet  
Press any key to finish...  
****/  
```  
  
  
  
## <a name="step-3-insert-a-row"></a>步驟 3：插入資料列  
  
  
此範例示範如何：  
  
- 藉由傳遞參數來安全地執行 SQL INSERT 陳述式。  
  - 使用參數可防止 SQL 插入式攻擊。  
- 擷取自動產生的值。  
  
  
  
```csharp
using System;  // C# , ADO.NET  
using DT = System.Data;            // System.Data.dll  
using QC = Microsoft.Data.SqlClient;  // System.Data.dll  
  
namespace ProofOfConcept_SQL_CSharp  
{  
    public class Program  
    {  
        static public void Main()  
        {  
            using (var connection = new QC.SqlConnection(  
                "Server=tcp:YOUR_SERVER_NAME_HERE.database.windows.net,1433;" +
                "Database=AdventureWorksLT;User ID=YOUR_LOGIN_NAME_HERE;" +
                "Password=YOUR_PASSWORD_HERE;Encrypt=True;" +
                "TrustServerCertificate=False;Connection Timeout=30;"  
                ))  
            {  
                connection.Open();  
                Console.WriteLine("Connected successfully.");  
  
                Program.InsertRows(connection);  
  
                Console.WriteLine("Press any key to finish...");  
                Console.ReadKey(true);  
            }  
        }  
  
        static public void InsertRows(QC.SqlConnection connection)  
        {  
            QC.SqlParameter parameter;  
  
            using (var command = new QC.SqlCommand())  
            {  
                command.Connection = connection;  
                command.CommandType = DT.CommandType.Text;  
                command.CommandText = @"  
INSERT INTO SalesLT.Product  
        (Name,  
        ProductNumber,  
        StandardCost,  
        ListPrice,  
        SellStartDate  
        )  
    OUTPUT  
        INSERTED.ProductID  
    VALUES  
        (@Name,  
        @ProductNumber,  
        @StandardCost,  
        @ListPrice,  
        CURRENT_TIMESTAMP  
        ); ";  
  
                parameter = new QC.SqlParameter("@Name", DT.SqlDbType.NVarChar, 50);  
                parameter.Value = "SQL Server Express 2014";  
                command.Parameters.Add(parameter);  
  
                parameter = new QC.SqlParameter("@ProductNumber", DT.SqlDbType.NVarChar, 25);  
                parameter.Value = "SQLEXPRESS2014";  
                command.Parameters.Add(parameter);  
  
                parameter = new QC.SqlParameter("@StandardCost", DT.SqlDbType.Int);  
                parameter.Value = 11;  
                command.Parameters.Add(parameter);  
  
                parameter = new QC.SqlParameter("@ListPrice", DT.SqlDbType.Int);  
                parameter.Value = 12;  
                command.Parameters.Add(parameter);  
  
                int productId = (int)command.ExecuteScalar();  
                Console.WriteLine("The generated ProductID = {0}.", productId);  
            }  
        }  
    }  
}  
/**** Actual output:  
Connected successfully.  
The generated ProductID = 1000.  
Press any key to finish...  
****/  
```
