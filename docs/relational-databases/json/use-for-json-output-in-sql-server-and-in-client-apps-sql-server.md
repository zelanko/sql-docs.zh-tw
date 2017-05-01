---
title: "在 SQL Server 和用戶端應用程式中使用 FOR JSON 輸出 (SQL Server) | Microsoft 文件"
ms.custom:
- SQL2016_New_Updated
ms.date: 06/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- FOR JSON, using in client apps
- FOR JSON, using in SQL Server
ms.assetid: 302e5397-b499-4ea3-9a7f-c24ccad698eb
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 5331ff00081a7b79756ef14e771ab4a22d3e35ac
ms.lasthandoff: 04/11/2017

---
# <a name="use-for-json-output-in-sql-server-and-in-client-apps-sql-server"></a>在 SQL Server 和用戶端應用程式中使用 FOR JSON 輸出 (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  下列範例示範在 **或用戶端應用程式中使用** FOR JSON [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 子句或其輸出的部分方式。  
  
## <a name="use-for-json-output-in-sql-server-variables"></a>在 SQL Server 變數中使用 FOR JSON 輸出  
 FOR JSON 子句的輸出屬於 NVARCHAR(MAX) 類型，因此可以指派給任何變數，如下列範例所示。  
  
```tsql  
DECLARE @x NVARCHAR(MAX) = (SELECT TOP 10 * FROM Sales.SalesOrderHeader FOR JSON AUTO)  
```  
  
## <a name="use-for-json-output-in-sql-server-user-defined-functions"></a>在 SQL Server 使用者定義函數中使用 FOR JSON 輸出  
 您可以建立使用者定義函數，將結果集格式化為 JSON，再傳回此 JSON 輸出。 下列範例會建立使用者定義函數，以擷取一些銷售訂單詳細資料列，並將其格式化為 JSON 陣列。  
  
```tsql  
CREATE FUNCTION GetSalesOrderDetails(@salesOrderId int)  
 RETURNS NVARCHAR(MAX)  
AS  
BEGIN  
   RETURN (SELECT UnitPrice, OrderQty  
           FROM Sales.SalesOrderDetail  
           WHERE SalesOrderID = @salesOrderId  
           FOR JSON AUTO)  
END
```  
  
 您可以在批次或查詢中使用此函數，如下列範例所示。  
  
```tsql  
DECLARE @x NVARCHAR(MAX)=dbo.GetSalesOrderDetails(43659)

PRINT dbo.GetSalesOrderDetails(43659)

SELECT TOP 10
  H.*,dbo.GetSalesOrderDetails(H.SalesOrderId) AS Details
FROM Sales.SalesOrderHeader H
```  
  
## <a name="merge-parent-and-child-data-into-a-single-table"></a>將父資料和子資料合併至單一資料表中  
 在下列範例中，每組子資料列會格式化為 JSON 陣列，並成為父資料表中 [詳細資料] 資料行的值。  
  
```tsql  
SELECT TOP 10 SalesOrderId, OrderDate,  
      (SELECT TOP 3 UnitPrice, OrderQty  
         FROM Sales.SalesOrderDetail D  
         WHERE H.SalesOrderId = D.SalesOrderID  
         FOR JSON AUTO) as Details  
INTO SalesOrder  
FROM Sales.SalesOrderHeader H  
```  
  
## <a name="update-the-data-in-json-columns"></a>更新 JSON 資料行中的資料  
 下列範例示範如何更新包含 JSON 文字之資料行的值。  
  
```tsql  
UPDATE SalesOrder  
SET Details =  
     (SELECT TOP 1 UnitPrice, OrderQty  
       FROM Sales.SalesOrderDetail D  
       WHERE D.SalesOrderId = SalesOrder.SalesOrderId  
      FOR JSON AUTO 
```  
  
## <a name="use-for-json-output-in-a-c-client-app"></a>在 C# 用戶端應用程式中使用 FOR JSON 輸出  
 下列範例示範如何將查詢的 JSON 輸出，擷取至 C# 用戶端應用程式中的 StringBuilder 物件。 假設變數 queryWithForJson 包含 SELECT 陳述式的文字及 FOR JSON 子句。  
  
```csharp  
            var queryWithForJson = "SELECT ... FOR JSON";
            var conn = new SqlConnection("<connection string>");
            var cmd = new SqlCommand(queryWithForJson, conn);
            conn.Open();
            var jsonResult = new StringBuilder();
            var reader = cmd.ExecuteReader();
            if (!reader.HasRows)
            {
                jsonResult.Append("[]");
            }
            else
            {
                while (reader.Read())
                {
                    jsonResult.Append(reader.GetValue(0).ToString());
                }
            }
```  
  
## <a name="see-also"></a>另請參閱  
 [使用 FOR JSON 將查詢結果格式化為 JSON &#40;SQL Server&#41;](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)  
  
  

