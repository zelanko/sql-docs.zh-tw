---
title: 使用巢狀 FOR XML 查詢組成 XML | Microsoft 文件
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- FOR XML query
- queries [XML in SQL Server], nested FOR XML
- XML [SQL Server], FOR XML queries
ms.assetid: 8dc42c05-16e8-4b7b-a5d3-550b55acae26
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 7097babca47f3d7867b98a8865c23d38566dd73a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47640057"
---
# <a name="shape-xml-with-nested-for-xml-queries"></a>使用巢狀 FOR XML 查詢組成 XML
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  以下範例會查詢 `Production.Product` 資料表，以擷取特定產品的 `ListPrice` 及 `StandardCost` 值。 兩個價格都會以 <`Price`> 元素傳回，而且每個 <`Price`> 元素都有一個 `PriceType` 屬性，使查詢值得關注。  
  
## <a name="example"></a>範例  
 以下是預期的 XML 外觀：  
  
```  
<xsd:schema xmlns:schema="urn:schemas-microsoft-com:sql:SqlRowSet2" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:sqltypes="http://schemas.microsoft.com/sqlserver/2004/sqltypes" targetNamespace="urn:schemas-microsoft-com:sql:SqlRowSet2" elementFormDefault="qualified">  
  <xsd:import namespace="http://schemas.microsoft.com/sqlserver/2004/sqltypes" schemaLocation="http://schemas.microsoft.com/sqlserver/2004/sqltypes/sqltypes.xsd" />  
  <xsd:element name="Production.Product" type="xsd:anyType" />  
</xsd:schema>  
<Production.Product xmlns="urn:schemas-microsoft-com:sql:SqlRowSet2" ProductID="520">  
  <Price xmlns="" PriceType="ListPrice">133.34</Price>  
  <Price xmlns="" PriceType="StandardCost">98.77</Price>  
</Production.Product>  
```  
  
 以下是巢狀 FOR XML 查詢：  
  
```  
USE AdventureWorks2012;  
GO  
SELECT Product.ProductID,   
          (SELECT 'ListPrice' as PriceType,   
                   CAST(CAST(ListPrice as NVARCHAR(40)) as XML)   
           FROM    Production.Product Price   
           WHERE   Price.ProductID=Product.ProductID   
           FOR XML AUTO, TYPE),  
          (SELECT  'StandardCost' as PriceType,   
                   CAST(CAST(StandardCost as NVARCHAR(40)) as XML)   
           FROM    Production.Product Price   
           WHERE   Price.ProductID=Product.ProductID   
           FOR XML AUTO, TYPE)  
FROM Production.Product  
WHERE ProductID=520  
for XML AUTO, TYPE, XMLSCHEMA  
```  
  
 請注意下列項目是從上一個查詢而來：  
  
-   外部 SELECT 陳述式會建構擁有 **ProductID** 屬性的 <`Product`> 元素，以及兩個 <`Price`> 子元素。  
  
-   兩個內部 SELECT 陳述式會建構兩個 <`Price`> 元素，每個都具有一個 **PriceType** 屬性與會傳回產品價格的 XML。  
  
-   外部 SELECT 陳述式中的 XMLSCHEMA 指示詞會產生內嵌的 XSD 結構描述，描述產生之 XML 的外觀。  
  
 您可以撰寫 FOR XML 查詢，然後對結果撰寫 XQuery 以重新安排 XML 的外觀，使查詢值得關注，如以下查詢所述：  
  
```  
SELECT ProductID,   
 ( SELECT p2.ListPrice, p2.StandardCost  
   FROM Production.Product p2   
   WHERE Product.ProductID = p2.ProductID  
   FOR XML AUTO, ELEMENTS XSINIL, type ).query('  
                                   for $p in /p2/*  
                                   return   
                                    <Price PriceType = "{local-name($p)}">  
                                     { data($p) }  
                                    </Price>  
                                  ')  
FROM Production.Product  
WHERE ProductID = 520  
FOR XML AUTO, TYPE  
```  
  
 先前的範例使用  資料類型的 **query()** 方法，以查詢內部 FOR XML 查詢傳回的 XML，並建構預期的結果。  
  
 以下是結果：  
  
```  
<Production.Product ProductID="520">  
  <Price PriceType="ListPrice">133.3400</Price>  
  <Price PriceType="StandardCost">98.7700</Price>  
</Production.Product>  
```  
  
## <a name="see-also"></a>另請參閱  
 [使用巢狀 FOR XML 查詢](../../relational-databases/xml/use-nested-for-xml-queries.md)  
  
  
