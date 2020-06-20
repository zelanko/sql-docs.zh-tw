---
title: sql：溢位欄位（SQLXML 4.0） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- overflow-field annotation
- unconsumed data
- overflow data [SQLXML]
- sql:overflow-field
ms.assetid: f005182b-6151-432d-ab22-3bc025742cd3
author: rothja
ms.author: jroth
ms.openlocfilehash: 45f29994242d40bd91a05b68f7afc3dcc2a38384
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85068209"
---
# <a name="sqloverflow-field-sqlxml-40"></a>sql:overflow-field (SQLXML 4.0)
  在結構描述中，您可以將資料行識別為溢位資料行，以便從 XML 文件中接收所有未耗用的資料。 請藉由使用 `sql:overflow-field` 註解，在結構描述中指定這個資料行。 具有多個溢位資料行是可行的。  
  
 當有定義 `sql:overflow-field` 註解的 XML 節點 (元素或屬性) 進入範圍時，此溢位資料行就會啟動，並接收未耗用的資料。 當此節點離開範圍時，此溢位資料行就不再處於使用中狀態，而且 XML 大量載入會讓之前的溢位欄位 (如果有的話) 變成使用中。  
  
 當它將資料儲存在溢位資料行時，XML 大量載入也會儲存有定義 `sql:overflow-field` 之父元素的開頭標記與結束標記。  
  
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
  
 在架構中，專案會 **\<Customer>** 對應至 [加入至] 資料表，而元素則會 **\<Order>** 對應至 CustOrder 資料表。  
  
 **\<Customer>** 和元素都會 **\<Order>** 識別溢位資料行。 因此，XML 大量載入會將元素的所有未耗用的子項目和屬性儲存在「已在」資料表的溢位資料 **\<Customer>** 行中，並將專案的所有未耗用的子項目和屬性儲存在 **\<Order>** CustOrder 資料表的溢位資料行中。  
  
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
  
  
