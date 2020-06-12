---
title: sql： relationship 和索引鍵排序規則（SQLXML）
description: 瞭解如何使用 SQLXML 中的 sql： relationship 元素和索引鍵排序規則。
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- sql:relationship
- key ordering rules [SQLXML]
- relationship annotation
ms.assetid: 914cb152-09f5-4b08-b35d-71940e4e9986
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 9963058caa3c027a294fac5828b39990bb344f5f
ms.sourcegitcommit: 9921501952147b9ce3e85a1712495d5b3eb13e5b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/29/2020
ms.locfileid: "84215728"
---
# <a name="annotation-interpretation---sqlrelationship-and-key-ordering-rule"></a>註解解譯 - sql:relationship 和索引鍵順序規則
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  由於 XML 大量載入會產生記錄做為其節點進入範圍，並將這些記錄傳送到 Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 做為其節點離開範圍，因此用於記錄的資料必須存在於節點的範圍內。  
  
 請考慮下列 XSD 架構，其中和元素之間的一對多關聯性 **\<Customer>** **\<Order>** （一位客戶可以下多個訂單）是使用元素指定的 **\<sql:relationship>** ：  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"<>   
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
  
  <xsd:element name="Customers" sql:relation="Cust" >  
   <xsd:complexType>  
     <xsd:sequence>  
       <xsd:element name="CustomerID"  type="xsd:integer" />  
       <xsd:element name="CompanyName" type="xsd:string" />  
       <xsd:element name="City"        type="xsd:string" />  
       <xsd:element name="Order"   
                          sql:relation="CustOrder"  
                          sql:relationship="CustCustOrder" >  
         <xsd:complexType>  
          <xsd:attribute name="OrderID" type="xsd:integer" />  
         </xsd:complexType>  
       </xsd:element>  
     </xsd:sequence>  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 當 **\<Customer>** 元素節點進入範圍內時，XML 大量載入會產生客戶記錄。 此記錄會持續到 XML 大量載入讀取為止 **\</Customer>** 。 在處理專案 **\<Order>** 節點時，XML 大量載入 **\<sql:relationship>** 會使用從父元素取得 CustOrder 資料表之 CustomerID 外鍵資料行的值 **\<Customer>** ，因為此元素不 **\<Order>** 會指定**customerid**屬性。 這表示在定義 **\<Customer>** 元素時，您必須先在架構中指定**CustomerID**屬性，然後再指定 **\<sql:relationship>** 。 否則，當 **\<Order>** 元素進入範圍內時，Xml 大量載入會產生 CustOrder 資料表的記錄，而當 XML 大量載入到達 **\</Order>** 結束標記時，它會將記錄傳送至， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 而不含 CustomerID 外鍵資料行值。  
  
 將這個範例所提供的結構描述儲存為 SampleSchema.xml。  
  
### <a name="to-test-a-working-sample"></a>測試工作範例  
  
1.  建立這些資料表：  
  
    ```  
    CREATE TABLE Cust (  
                  CustomerID     int          PRIMARY KEY,  
               CompanyName    varchar(20)  NOT NULL,  
                  City           varchar(20)  DEFAULT 'Seattle')  
    GO  
    CREATE TABLE CustOrder (  
                  OrderID        varchar(10) PRIMARY KEY,  
               CustomerID     int         FOREIGN KEY REFERENCES                                          Cust(CustomerID))  
    GO  
    ```  
  
2.  儲存下列範例資料為 SampleXMLData.xml：  
  
    ```  
    <ROOT>    
      <Customers>  
        <CompanyName>Hanari Carnes</CompanyName>  
        <City>NY</City>  
        <Order OrderID="1" />  
        <Order OrderID="2" />  
        <CustomerID>1111</CustomerID>  
      </Customers>  
      <Customers>  
        <CompanyName>Toms Spezialitten</CompanyName>  
         <City>LA</City>    
        <Order OrderID="3" />  
        <CustomerID>1112</CustomerID>  
      </Customers>  
      <Customers>  
        <CompanyName>Victuailles en stock</CompanyName>  
        <Order OrderID="4" />  
        <CustomerID>1113</CustomerID>  
      </Customers>  
    </ROOT>  
    ```  
  
3.  若要執行 XML 大量載入，請儲存和執行下列 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic Scripting Edition (VBScript) 範例為 MySample.vbs：  

    ```  
    set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
    objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
    objBL.ErrorLogFile = "c:\error.log"  
    objBL.CheckConstraints = True  
    objBL.Transaction=True  
    objBL.Execute "c:\SampleSchema.xml", "c:\SampleXMLData.xml"  
    set objBL=Nothing  
    ```  
  
     結果是，XML 大量載入將 NULL 值插入到 CustOrder 資料表的 CustomerID 外部索引鍵資料行中。 如果您修改 XML 範例資料 **\<CustomerID>** ，使子項目出現在子專案之前 **\<Order>** ，您會得到預期的結果： XML 大量載入會將指定的外鍵值插入資料行。  
  
 這是相等的 XDR 結構描述：  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"   
        xmlns:dt="urn:schemas-microsoft-com:xml:datatypes"    
        xmlns:sql="urn:schemas-microsoft-com:xml-sql" >   
   <ElementType name="CustomerID"  />  
   <ElementType name="CompanyName" />  
   <ElementType name="City"        />  
  
   <ElementType name="root" sql:is-constant="1">  
      <element type="Customers" />  
   </ElementType>  
  
   <ElementType name="Customers" sql:relation="Cust" >  
      <element type="CustomerID" sql:field="CustomerID" />  
      <element type="CompanyName" sql:field="CompanyName" />  
      <element type="City" sql:field="City" />  
      <element type="Order" >  
                 <sql:relationship  
                        key-relation    ="Cust"  
                        key             ="CustomerID"  
                        foreign-key     ="CustomerID"  
                        foreign-relation="CustOrder" />  
      </element>  
   </ElementType>  
    <ElementType name="Order" sql:relation="CustOrder" >  
      <AttributeType name="OrderID" />  
      <AttributeType name="CustomerID" />  
      <attribute type="OrderID" />  
      <attribute type="CustomerID" />  
    </ElementType>  
</Schema>  
```  
  
  
