---
title: 步驟 3： 使用 ADO.NET 的 sql 連接的概念證明 |Microsoft 文件
ms.custom: ''
ms.date: 08/08/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado-net
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: aebe3dc6-3ee4-4d11-8e43-5d32b3f91490
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 632edda3a32b286e74e8c36db647e22ed55c5da6
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-adonet"></a>步驟 3： 使用 ADO.NET 的 sql 連接的概念證明

- 前一篇文章：&nbsp;&nbsp;&nbsp;[步驟 2： 建立 SQL database 的 ADO.NET 程式開發](step-2-create-a-sql-database-for-ado-net-development.md)  
- 接下來文章：&nbsp;&nbsp;&nbsp;[步驟 4： 彈性地連接到使用 ADO.NET 的 SQL](step-4-connect-resiliently-to-sql-with-ado-net.md)  

  
這個 C# 程式碼範例都應該考慮只概念證明。 範例程式碼為了清楚起見，已簡化，並不一定代表由 Microsoft 所建議的最佳作法。  
  
## <a name="step-1-connect"></a>步驟 1： 連接
  
此方法**SqlConnection.Open**用來連接到您的 SQL 資料庫。  


```CSharp  
    // C# , ADO.NET  
    using System;
    using QC = System.Data.SqlClient;  // System.Data.dll  
      
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


## <a name="step-2--execute-a-query"></a>步驟 2： 執行查詢  
  
SqlCommand.ExecuteReader 方法：  
  
- SQL 系統會發出 SQL SELECT 陳述式。  
- 傳回 SqlDataReader 提供存取的結果資料列的執行個體。  
  
  
  
```CSharp  
    using System;  // C# , ADO.NET  
    using DT = System.Data;            // System.Data.dll  
    using QC = System.Data.SqlClient;  // System.Data.dll  
      
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
  
  
  
## <a name="step-3-insert-a-row"></a>步驟 3： 插入資料列  
  
  
這個範例會示範如何：  
  
- 安全地執行的 SQL INSERT 陳述式所傳遞的參數。  
  - 使用參數可防止 SQL 資料隱碼攻擊。  
- 擷取自動產生的值。  
  
  
  
```CSharp  
    using System;  // C# , ADO.NET  
    using DT = System.Data;            // System.Data.dll  
    using QC = System.Data.SqlClient;  // System.Data.dll  
      
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
