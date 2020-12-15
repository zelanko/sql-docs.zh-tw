---
title: 'sql：溢位-field (SQLXML) '
description: 瞭解如何使用 sql：溢位欄位注釋將資料行識別為溢位資料行，以接收 XML 檔中所有未耗用的資料。
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- overflow-field annotation
- unconsumed data
- overflow data [SQLXML]
- sql:overflow-field
ms.assetid: f005182b-6151-432d-ab22-3bc025742cd3
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4d0fa21bcd570a5f5196dfbc1bdf8e1bb6186cb8
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97462939"
---
# <a name="annotation-interpretation---sqloverflow-field"></a>註解解譯 - sql:overflow-field
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  在結構描述中，您可以將資料行識別為溢位資料行，以便從 XML 文件中接收所有未耗用的資料。 您可以使用 **sql：溢位欄位** 注釋，在架構中指定這個資料行。 具有多個溢位資料行是可行的。  
  
 每當 XML 節點 (專案或屬性) ，其中有定義在範圍內的 **sql：溢位欄位** 注釋時，便會啟用溢位資料行，並接收未耗用的資料。 當此節點離開範圍時，此溢位資料行就不再處於使用中狀態，而且 XML 大量載入會讓之前的溢位欄位 (如果有的話) 變成使用中。  
  
 當它將資料儲存在溢位資料行時，XML 大量載入也會儲存定義了 **sql：溢位欄位** 之父元素的開頭和結束記號。  
  
 例如，下列架構會描述 **\<Customers>** 和 **\<CustOrder>** 元素。 每一個元素都可識別溢位資料行：  
  
```  
<?xml version="1.0" ?>  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
 <xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="CustCustOrder"  
        parent="Cust"  
        parent-key="CustomerID"  
        child="CustOrder"  
        child-key="CustomerID" />  
  </xsd:appinfo>  
 </xsd:annotation>  
 <xsd:element name="ROOT" sql:is-constant="1">  
  <xsd:complexType>  
    <xsd:sequence>   
      <xsd:element name="Customers"   
                   sql:relation="Cust"  
                   sql:overflow-field="OverflowColumn">  
        <xsd:complexType>  
             <xsd:sequence>   
             <xsd:element name="CustomerID" type="xsd:integer"/>  
             <xsd:element name="CompanyName"  type="xsd:string"/>  
             <xsd:element name="City" type="xsd:string"/>  
             <xsd:element name="Order"  
                          sql:relation="CustOrder"  
                          sql:relationship="CustCustOrder"  
                          sql:overflow-field="OverflowColumn">  
               <xsd:complexType>  
                 <xsd:attribute name="OrderID"/>  
                 <xsd:attribute name="CustomerID"/>  
               </xsd:complexType>  
             </xsd:element>  
          </xsd:sequence>   
        </xsd:complexType>  
      </xsd:element>  
    </xsd:sequence>  
  </xsd:complexType>  
 </xsd:element>  
</xsd:schema>  
```  
  
 在架構中，專案會 **\<Customer>** 對應至加入的資料表，而 **\<Order>** 元素則會對應到 CustOrder 資料表。  
  
 **\<Customer>** 和元素都會 **\<Order>** 識別溢位資料行。 因此，XML 大量載入會將元素的所有未耗用子項目和屬性儲存在「資料表」資料表的溢位資料 **\<Customer>** 行中，並將專案的所有未耗用子項目和屬性儲存在 **\<Order>** CustOrder 資料表的溢位資料行中。  
  
### <a name="to-test-a-working-sample"></a>測試工作範例  
  
1.  將這個範例所提供的結構描述儲存為 SampleSchema.xml。  
  
2.  建立這些資料表：  
  
    ```  
    CREATE TABLE Cust (  
              CustomerID     int         PRIMARY KEY,  
              CompanyName    varchar(20) NOT NULL,  
              City           varchar(20) DEFAULT 'Seattle',  
              OverflowColumn nvarchar(200))  
    GO  
    CREATE TABLE CustOrder (  
              OrderID        int         PRIMARY KEY,  
              CustomerID     int         FOREIGN KEY REFERENCES  
                                              Cust(CustomerID),  
              OverflowColumn nvarchar(200))  
    GO  
    ```  
  
3.  將下列 XML 資料範例儲存為 SampleXMLData.xml：  
  
    ```  
    <ROOT>  
      <Customers>  
        <CustomerID>1111</CustomerID>  
        <CompanyName>Hanari Carnes</CompanyName>  
        <City><![CDATA[NY]]> </City>  
          <Junk>garbage in overflow</Junk>  
        <Order OrderID="1" />  
        <Order OrderID="2" />  
     </Customers>  
     <Customers>  
       <CustomerID>1112</CustomerID>  
       <CompanyName>Toms Spezialitten</CompanyName>  
       <City><![CDATA[LA]]> </City>  
       <xyz><address>111 Maple, Seattle</address></xyz>     
       <Order OrderID="3" />  
     </Customers>  
       <Customers>  
       <CustomerID>1113</CustomerID>  
       <CompanyName>Victuailles en stock</CompanyName>  
       <Order OrderID="4" />  
      </Customers>  
    </ROOT>  
    ```  
  
4.  若要執行 XML 大量載入，請將這個 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic Scripting Edition (VBScript) 範例儲存為 Sample.vbs 並執行它：  
  
    ```  
    set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
    objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
    objBL.ErrorLogFile = "c:\error.log"  
    objBL.CheckConstraints = True  
    objBL.Execute "c:\SampleSchema.xml", "c:\SampleXMLData.xml"  
    set objBL=Nothing  
    ```  
  
  
