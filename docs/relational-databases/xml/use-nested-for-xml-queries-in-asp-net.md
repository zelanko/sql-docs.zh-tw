---
title: 在 ASP.NET 中使用巢狀 FOR XML 查詢 | Microsoft 文件
description: 了解如何在 ASP.NET 應用程式中使用巢狀 FOR XML 查詢來產生元素中心的 XML。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- FOR XML clause, nested FOR XML queries
- queries [XML in SQL Server], ASP.NET and
- nested FOR XML queries in ASP.NET
- ASP.NET [SQL Server]
ms.assetid: 691ac7dd-afc5-4760-932c-2b1dcd9394ed
author: MightyPen
ms.author: genemi
ms.openlocfilehash: def3cb5a9e77324a0d062ec26c0d042afcc0bc3a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85738381"
---
# <a name="use-nested-for-xml-queries-in-aspnet"></a>在 ASP.NET 中使用巢狀 FOR XML 查詢
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  在此範例中，ASP.NET 應用程式會藉由在 SQL Server 中執行預存程序來將 XML 傳回給瀏覽器。 此預存程序會使用巢狀查詢產生 XML。 [使用巢狀 AUTO 模式查詢產生同層級](../../relational-databases/xml/generate-siblings-with-a-nested-auto-mode-query.md)主題中有顯示類似的 SELECT 陳述式。 此範例將示範一個方式來使用巢狀 FOR XML 查詢，於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中產生元素中心的 XML。  
  
## <a name="example"></a>範例  
  
```  
CREATE PROC GetSalesOrderInfo AS  
SELECT   
      (SELECT top 2 SalesOrderID, SalesPersonID, CustomerID,  
         (select top 3 SalesOrderID, ProductID, OrderQty, UnitPrice  
           from Sales.SalesOrderDetail  
            WHERE  SalesOrderDetail.SalesOrderID = SalesOrderHeader.SalesOrderID  
            FOR XML AUTO, TYPE)  
      FROM  Sales.SalesOrderHeader  
        WHERE SalesOrderHeader.SalesOrderID = SalesOrder.SalesOrderID  
      for xml auto, type),  
        (SELECT *   
         FROM  (SELECT SalesPersonID, EmployeeID  
              FROM Sales.SalesPerson, HumanResources.Employee  
              WHERE SalesPerson.SalesPersonID = Employee.EmployeeID) As SalesPerson  
         WHERE  SalesPerson.SalesPersonID = SalesOrder.SalesPersonID  
       FOR XML AUTO, TYPE, ELEMENTS)  
FROM (SELECT SalesOrderHeader.SalesOrderID, SalesOrderHeader.SalesPersonID  
      FROM Sales.SalesOrderHeader, Sales.SalesPerson  
      WHERE SalesOrderHeader.SalesPersonID = SalesPerson.SalesPersonID  
     ) as SalesOrder  
ORDER BY SalesOrder.SalesOrderID  
FOR XML AUTO, TYPE  
GO  
```  
  
 這是 .aspx 應用程式。 其會執行預存程序並在瀏覽器中傳回 XML。  
  
```  
<%@LANGUAGE=C# Debug=true %>  
<%@import Namespace="System.Xml"%>  
<%@import namespace="System.Data.SqlClient" %><%  
Response.Expires = -1;  
Response.ContentType = "text/xml";  
%>  
  
<%  
using(System.Data.SqlClient.SqlConnection c = new System.Data.SqlClient.SqlConnection("Data Source=server;Database=AdventureWorks;Integrated Security=SSPI;"))  
using(System.Data.SqlClient.SqlCommand cmd = c.CreateCommand())  
{  
   cmd.CommandText = "GetSalesOrderInfo";  
   cmd.CommandType = CommandType.StoredProcedure;  
   cmd.Connection.Open();  
   System.Xml.XmlReader r = cmd.ExecuteXmlReader();  
   System.Xml.XmlTextWriter w = new System.Xml.XmlTextWriter(Response.Output);  
   w.WriteStartElement("Root");  
   r.MoveToContent();  
   while(! r.EOF)  
   {  
      w.WriteNode(r, true);  
   }  
   w.WriteEndElement();  
   w.Flush();  
}  
%>  
```  
  
##### <a name="to-test-the-application"></a>若要測試應用程式  
  
1.  在 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫中建立預存程序。  
  
2.  在 c:\inetpub\wwwroot 目錄中儲存 .aspx 應用程式 (GetSalesOrderInfo.aspx)。  
  
3.  執行應用程式 (`https://server/GetSalesOrderInfo.aspx`)。  
  
## <a name="see-also"></a>另請參閱  
 [使用巢狀 FOR XML 查詢](../../relational-databases/xml/use-nested-for-xml-queries.md)  
  
  
