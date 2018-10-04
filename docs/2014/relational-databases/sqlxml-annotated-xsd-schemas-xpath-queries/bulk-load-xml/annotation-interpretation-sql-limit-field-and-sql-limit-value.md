---
title: 'sql: limit-value-欄位和 sql: limit-value-值 (SQLXML 4.0) |Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- limiting values [SQLXML]
- limit-value annotation
- limit-field annotation
- sql:limit-field
- sql:limit-value
- filtering [SQLXML]
ms.assetid: 402c21cf-9566-463f-a928-f94270c11db3
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 77415951f7f581eb75604668fca4f5d573a69675
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48200178"
---
# <a name="sqllimit-field-and-sqllimit-value-sqlxml-40"></a>sql:limit-field 和 sql:limit-value (SQLXML 4.0)
  XML 大量載入會根據 `sql:limit-field` 和 `sql:limit-value` 註解的定義來處理這些註解。 如需詳細資訊，請參閱 <<c0> [ 篩選值使用 sql: limit-value-欄位和 sql: limit-value-值&#40;SQLXML 4.0&#41;](annotation-interpretation-sql-limit-field-and-sql-limit-value.md)。</c0>  
  
 例如，假設資料庫包含下列資料表：  
  
-   Customer (CustomerID, CompanyName)  
  
-   Addresses (CustomerID, StreetAddress, AddressType)  
  
 客戶可能有許多地址，而每個地址都具有相關聯的地址類型 (例如，送貨地址或帳單地址)。  
  
 現在，請考慮這些資料表的這個 XML 檢視 (指定在下列註解 XSD 結構描述中)：  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="CustAddr"  
        parent="Customer"  
        parent-key="CustomerID"  
        child="Address"  
        child-key="CustomerID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Customer" sql:relation="Customer" >  
   <xsd:complexType>  
        <xsd:attribute name="CustomerID"   type="xsd:int" />   
        <xsd:attribute name="CompanyName"  type="xsd:string" />  
        <xsd:attribute name="BillTo"   
                       type="xsd:string"   
                       sql:relation="Address"   
                       sql:field="StreetAddress"  
                       sql:limit-field="AddressType"  
                       sql:limit-value="billing"  
                       sql:relationship="CustAddr" >  
        </xsd:attribute>  
        <xsd:attribute name="ShipTo"   
                       type="xsd:string"   
                       sql:relation="Address"   
                       sql:field="StreetAddress"  
                       sql:limit-field="AddressType"  
                       sql:limit-value="shipping"  
                       sql:relationship="CustAddr" >  
        </xsd:attribute>  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 在接到這個結構描述和 XML 資料時，XML 大量載入會將針對 BillTo 屬性所指定的值以及 AddressType 資料行的 "billing" 值插入至 CustAddress 資料表的 StreetAddress 資料行。  
  
 同樣地，XML 大量載入會將針對 ShipTo 屬性所指定的值以及 AddressType 資料行中的 "shipping" 值插入至 StreetAddress 資料行。  
  
### <a name="to-test-a-working-sample"></a>測試工作範例  
  
1.  將這個範例所提供的結構描述儲存為 SampleSchema.xml。  
  
2.  建立這些資料表：  
  
    ```  
    CREATE TABLE Customer(  
                     CustomerID     int         PRIMARY KEY,  
                     CompanyName    varchar(20) NOT NULL)  
    GO  
    CREATE TABLE Address(  
                      CustomerID     int        FOREIGN KEY REFERENCES   
                                                 Customer(CustomerID),   
                      StreetAddress  varchar(50),  
                      AddressType    varchar(10))  
    GO  
    ```  
  
3.  儲存下列範例資料為 SampleXMLData.xml：  
  
    ```  
    <Customer CustomerID="1111" CompanyName="Sean Chai" City="NY"   
                 BillTo="111 Maple (Billing) "   
                 ShipTo="111 Maple (Shipping)" />  
    <Customer CustomerID="1112" CompanyName="Dont Know" City="LA"   
                 BillTo="222 Spruce (Billing)"   
                 ShipTo="222 Spruce (Shipping)" />  
    ```  
  
4.  若要執行 XML 大量載入，請將這個 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic Scripting Edition (VBScript) 範例儲存為 Sample.vbs 並執行它：  
  
    ```  
    set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
    objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
    objBL.ErrorLogFile = "c:\error.log"  
    objBL.XMLFragment = True  
    objBL.CheckConstraints=True  
    objBL.Execute "c:\SampleSchema.xml", "c:\SampleXMLData.xml"  
    set objBL=Nothing  
    ```  
  
 這是相等的 XDR 結構描述：  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"  
        xmlns:dt="urn:schemas-microsoft-com:datatypes"  
        xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  
<ElementType name="Customer" sql:relation="Customer" >  
    <AttributeType name="CustomerID" />  
    <AttributeType name="CompanyName" />  
    <AttributeType name="BillTo" />  
    <AttributeType name="ShipTo" />  
  
    <attribute type="CustomerID" />  
    <attribute type="CompanyName" />  
    <attribute type="BillTo"   
                sql:limit-field="AddressType"  
                sql:limit-value="billing"  
                sql:field="StreetAddress"  
                sql:relation="Address" >  
                <sql:relationship   
                        key="CustomerID"  
                        key-relation="Customer"  
                        foreign-relation="Address"  
                        foreign-key="CustomerID" />  
    </attribute>  
    <attribute type="ShipTo"   
                sql:limit-field="AddressType"  
                sql:limit-value="shipping"  
                sql:field="StreetAddress"  
                sql:relation="Address" >  
                <sql:relationship   
                     key="CustomerID"  
                     key-relation="Customer"  
                     foreign-relation="Address"  
                     foreign-key="CustomerID" />  
    </attribute>  
</ElementType>  
</Schema>  
```  
  
  
