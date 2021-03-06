---
title: Updategram (SQLXML) 的批註式對應架構
description: 瞭解如何使用 SQLXML 4.0 updategram 中指定的批註式 XSD 或 XDR 對應架構來處理資料庫的更新。
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- annotated XSD schemas, updategrams
- data types [SQLXML], mapping schema in updategrams
- updategrams [SQLXML], annotated mapping schemas
- annotated XDR schemas, updategrams
- inverse attribute
- parent-child relationships [SQLXML]
- mapping-schema attribute
- mapping schema [SQLXML], updategrams
- sql:inverse
ms.assetid: 2e266ed9-4cfb-434a-af55-d0839f64bb9a
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8c8643c40f7b62c0a0fdc3d85d32111d05ee955f
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97405106"
---
# <a name="specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-40"></a>在 Updategram 中指定註解式對應結構描述 (SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  本主題說明 Updategram 中指定的對應結構描述 (XSD 或 XDR) 要如何用來處理更新。 在 updategram 中，您可以提供批註式對應架構的名稱，以便用來將 updategram 中的元素和屬性對應至中的資料表和資料行 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。 在 updategram 中指定對應結構描述時，此 updategram 中指定的元素和屬性名稱必須對應到對應結構描述內的元素和屬性。  
  
 若要指定對應架構，請使用元素的 **對應架構** 屬性 **\<sync>** 。 下列範例會示範兩個 updategram：使用簡單對應結構描述的 updategram 以及使用更複雜之結構描述的 updategram。  
  
> [!NOTE]  
>  本文件集假設您非常熟悉 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中的範本和對應結構描述支援。 如需詳細資訊，請參閱 [批註式 XSD 架構簡介 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml/annotated-xsd-schemas/introduction-to-annotated-xsd-schemas-sqlxml-4-0.md)。 針對使用 XDR 的繼承應用程式，請參閱 [SQLXML 4.0&#41;中 &#40;取代的批註式 XDR 架構 ](../../../relational-databases/sqlxml/annotated-xsd-schemas/annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md)。  
  
## <a name="dealing-with-data-types"></a>處理資料類型  
 如果架構指定了使用sql： datatype)  (的 image、 **binary** 或 **Varbinary** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料類型，而且沒有指定 xml 資料類型，則 updategram 會假設 xml 資料類型為 **二進位基底 64**。 如果您的資料是 **bin. 基底** 類型，您必須明確指定類型 (**dt： type = bin. base** 或 **Type = "xsd： hexBinary"**) 。  
  
 如果架構指定 **dateTime**、 **date** 或 **time** XSD 資料類型，您也必須 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 使用 **sql： datatype = "dateTime"** 來指定對應的資料類型。  
  
 處理 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **money** 類型的參數時，您必須在對應架構中的適當節點上明確指定 **sql： datatype = "money"** 。  
  
## <a name="examples"></a>範例  
 若要使用下列範例建立工作範例，您必須符合 [執行 SQLXML 範例的需求](../../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md)中所指定的需求。  
  
### <a name="a-creating-an-updategram-with-a-simple-mapping-schema"></a>A. 使用簡單對應結構描述建立 updategram  
 下列 XSD 架構 ( # A0) 是將專案對應 **\<Customer>** 至 Sales. Customer 資料表的對應架構：  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="Customer" sql:relation="Sales.Customer" >  
   <xsd:complexType>  
        <xsd:attribute name="CustID"    
                       sql:field="CustomerID"   
                       type="xsd:string" />  
        <xsd:attribute name="RegionID"    
                       sql:field="TerritoryID"    
                       type="xsd:string" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 下列 updategram 會將一筆記錄插入 Sales.Customer 資料表，並依賴之前的對應結構描述，適當地將此資料對應至資料表。 請注意，updategram 會使用相同的專案名稱， **\<Customer>** 如架構中所定義。 這是強制性的作法，因為 updategram 會指定特定的結構描述。  
  
##### <a name="to-test-the-updategram"></a>若要測試 Updategram  
  
1.  複製上述的結構描述程式碼，並將其貼到文字檔中。 將檔案儲存為 SampleUpdateSchema.xml。  
  
2.  複製底下的 updategram 範本，並將其貼到文字檔中。 將檔案儲存為 SampleUpdategram.xml 並放在與 SampleUpdateSchema.xml 相同的目錄中。  
  
    ```  
    <ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
      <updg:sync mapping-schema="SampleUpdateSchema.xml">  
        <updg:before>  
          <Customer CustID="1" RegionID="1"  />  
        </updg:before>  
        <updg:after>  
          <Customer CustID="1" RegionID="2" />  
        </updg:after>  
      </updg:sync>  
    </ROOT>  
    ```  
  
     針對對應結構描述 (SampleUpdateSchema.xml) 指定的目錄路徑相對於儲存範本的目錄。 您也可以指定絕對路徑，例如：  
  
    ```  
    mapping-schema="C:\SqlXmlTest\SampleUpdateSchema.xml"  
    ```  
  
3.  建立和使用 SQLXML 4.0 測試指令碼 (Sqlxml4test.vbs) 以執行範本。  
  
     如需詳細資訊，請參閱 [使用 ADO 執行 SQLXML 4.0 查詢](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
 這是相等的 XDR 結構描述：  
  
```  
<?xml version="1.0" ?>  
   <Schema xmlns="urn:schemas-microsoft-com:xml-data"   
         xmlns:dt="urn:schemas-microsoft-com:datatypes"   
         xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
     <ElementType name="Customer" sql:relation="Sales.Customer" >  
       <AttributeType name="CustID" />  
       <AttributeType name="RegionID" />  
  
       <attribute type="CustID" sql:field="CustomerID" />  
       <attribute type="RegionID" sql:field="TerritoryID" />  
     </ElementType>  
   </Schema>   
```  
  
### <a name="b-inserting-a-record-by-using-the-parent-child-relationship-specified-in-the-mapping-schema"></a>B. 使用對應結構描述內指定的父子式關聯性插入記錄  
 結構描述元素可以產生關聯。 專案會 **\<sql:relationship>** 指定架構元素之間的父子式關聯性。 這項資訊是用來更新具有主索引鍵與外部索引鍵關聯性的對應資料表。  
  
 下列對應架構 ( # A0) 是由兩個元素所 **\<Order>** 組成 **\<OD>** ：  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="OrderOD"  
          parent="Sales.SalesOrderHeader"  
          parent-key="SalesOrderID"  
          child="Sales.SalesOrderDetail"  
          child-key="SalesOrderID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Order" sql:relation="Sales.SalesOrderHeader" >  
   <xsd:complexType>  
     <xsd:sequence>  
        <xsd:element name="OD"   
                     sql:relation="Sales.SalesOrderDetail"  
                     sql:relationship="OrderOD" >  
           <xsd:complexType>  
              <xsd:attribute name="SalesOrderID"   type="xsd:integer" />  
              <xsd:attribute name="ProductID" type="xsd:integer" />  
             <xsd:attribute name="UnitPrice"  type="xsd:decimal" />  
             <xsd:attribute name="OrderQty"   type="xsd:integer" />  
             <xsd:attribute name="UnitPriceDiscount"   type="xsd:decimal" />  
  
           </xsd:complexType>  
        </xsd:element>  
     </xsd:sequence>  
        <xsd:attribute name="CustomerID"   type="xsd:string" />   
        <xsd:attribute name="SalesOrderID"  type="xsd:integer" />  
        <xsd:attribute name="OrderDate"  type="xsd:date" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 下列 updategram 會使用這個 XSD 架構來加入新的訂單詳細資料記錄， (**\<OD>** **\<after>** order 43860 的區塊) 中的元素。 **對應架構** 屬性是用來指定 updategram 中的對應架構。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync mapping-schema="SampleUpdateSchema.xml" >  
    <updg:before>  
       <Order SalesOrderID="43860" />  
    </updg:before>  
    <updg:after>  
      <Order SalesOrderID="43860" >  
           <OD ProductID="753" UnitPrice="$10.00"  
               Quantity="5" Discount="0.0" />  
      </Order>  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-the-updategram"></a>若要測試 Updategram  
  
1.  複製上述的結構描述程式碼，並將其貼到文字檔中。 將檔案儲存為 SampleUpdateSchema.xml。  
  
2.  複製上述的 updategram 範本，並將其貼到文字檔中。 將檔案儲存為 SampleUpdategram.xml 並放在與 SampleUpdateSchema.xml 相同的目錄中。  
  
     針對對應結構描述 (SampleUpdateSchema.xml) 指定的目錄路徑相對於儲存範本的目錄。 您也可以指定絕對路徑，例如：  
  
    ```  
    mapping-schema="C:\SqlXmlTest\SampleUpdateSchema.xml"  
    ```  
  
3.  建立和使用 SQLXML 4.0 測試指令碼 (Sqlxml4test.vbs) 以執行範本。  
  
     如需詳細資訊，請參閱 [使用 ADO 執行 SQLXML 4.0 查詢](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
 這是相等的 XDR 結構描述：  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"  
        xmlns:dt="urn:schemas-microsoft-com:datatypes"  
        xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  
<ElementType name="OD" sql:relation="Sales.SalesOrderDetail" >  
    <AttributeType name="SalesOrderID" />  
    <AttributeType name="ProductID" />  
    <AttributeType name="UnitPrice"  dt:type="fixed.14.4" />  
    <AttributeType name="OrderQty" />  
    <AttributeType name="UnitPriceDiscount" />  
  
    <attribute type="SalesOrderID" />  
    <attribute type="ProductID" />  
    <attribute type="UnitPrice" />  
    <attribute type="OrderQty" />  
    <attribute type="UnitPriceDiscount" />  
</ElementType>  
  
<ElementType name="Order" sql:relation="Sales.SalesOrderHeader" >  
    <AttributeType name="CustomerID" />  
    <AttributeType name="SalesOrderID" />  
    <AttributeType name="OrderDate" />  
  
    <attribute type="CustomerID" />  
    <attribute type="SalesOrderID" />  
    <attribute type="OrderDate" />  
    <element type="OD" >  
             <sql:relationship   
                   key-relation="Sales.SalesOrderHeader"  
                   key="SalesOrderID"  
                   foreign-key="SalesOrderID"  
                   foreign-relation="Sales.SalesOrderDetail" />  
    </element>  
</ElementType>  
</Schema>  
```  
  
### <a name="c-inserting-a-record-by-using-the-parent-child-relationship-and-inverse-annotation-specified-in-the-xsd-schema"></a>C. 使用 XSD 結構描述內指定的父子式關聯性和反向註解來插入記錄  
 此範例說明 updategram 邏輯如何使用 XSD 中指定的父子式關聯性來處理更新，以及如何使用 **反向** 注釋。 如需 **反向** 注釋的詳細資訊，請參閱 [在 sql： relationship &#40;SQLXML 4.0&#41;上指定 Sql：反向屬性](../../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-the-sql-inverse-attribute-on-sql-relationship-sqlxml-4-0.md)。  
  
 此範例假設下列資料表位於 **tempdb** 資料庫中：  
  
-   `Cust (CustomerID, CompanyName)`，其中 `CustomerID` 是主索引鍵  
  
-   `Ord (OrderID, CustomerID)`，其中 `CustomerID` 是參考 `CustomerID` 資料表內之 `Cust` 主索引鍵的外部索引鍵。  
  
 updategram 會使用以下 XSD 結構描述，將記錄插入 Cust 和 Ord 資料表中：  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
       <sql:relationship name="OrdCust" inverse="true"  
                  parent="Ord"  
                  parent-key="CustomerID"  
                  child-key="CustomerID"  
                  child="Cust"/>  
  </xsd:appinfo>  
</xsd:annotation>  
  
<xsd:element name="Order" sql:relation="Ord">  
  <xsd:complexType>  
    <xsd:sequence>  
      <xsd:element ref="Customer" sql:relationship="OrdCust"/>  
    </xsd:sequence>  
    <xsd:attribute name="OrderID"   type="xsd:int"/>  
    <xsd:attribute name="CustomerID" type="xsd:string"/>  
  </xsd:complexType>  
</xsd:element>  
  
<xsd:element name="Customer" sql:relation="Cust">  
  <xsd:complexType>  
     <xsd:attribute name="CustomerID"  type="xsd:string"/>  
    <xsd:attribute name="CompanyName" type="xsd:string"/>  
  </xsd:complexType>  
</xsd:element>  
  
</xsd:schema>  
```  
  
 此範例中的 XSD 架構具有 **\<Customer>** 和 **\<Order>** 元素，並指定兩個元素之間的父子式關聯性。 它會識別 **\<Order>** 為父元素和 **\<Customer>** 子項目。  
  
 此 updategram 處理邏輯會使用有關父子式關聯性的資訊來判斷哪些記錄會插入資料表中。 在此範例中，updategram 邏輯會先嘗試將記錄插入 Ord 資料表 (因為 **\<Order>** 是父) ，然後嘗試將記錄插入至「加入」資料表 (因為 **\<Customer>** 是子) 。 但是，由於包含在資料庫資料表結構描述內之主索引鍵/外部索引鍵資訊的緣故，這項插入作業會造成資料庫中的外部索引鍵違規，而使得插入失敗。  
  
 為了指示 updategram 邏輯在更新作業期間反轉父子式關聯性，會在元素上指定 **反向** 注釋 **\<relationship>** 。 因此，記錄會先加入到 Cust 資料表，然後再加入到 Ord 資料表，作業就會成功。  
  
 下列 updategram 會使用指定的 XSD 結構描述，將訂單 (OrderID=2) 插入到 Ord 資料表，並將客戶 (CustomerID='AAAAA') 插入到 Cust 資料表：  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync mapping-schema="SampleUpdateSchema.xml" >  
    <updg:before/>  
    <updg:after>  
      <Order OrderID="2" CustomerID="AAAAA" >  
        <Customer CustomerID="AAAAA" CompanyName="AAAAA Company" />  
      </Order>  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-the-updategram"></a>若要測試 Updategram  
  
1.  在 **tempdb** 資料庫中建立這些資料表：  
  
    ```  
    USE tempdb  
    CREATE TABLE Cust(CustomerID varchar(5) primary key,   
                      CompanyName varchar(20))  
    GO  
    CREATE TABLE Ord (OrderID int primary key,   
                      CustomerID varchar(5) references Cust(CustomerID))  
    GO  
    ```  
  
2.  複製上述的結構描述程式碼，並將其貼到文字檔中。 將檔案儲存為 SampleUpdateSchema.xml。  
  
3.  複製上述的 updategram 範本，並將其貼到文字檔中。 將檔案儲存為 SampleUpdategram.xml 並放在與 SampleUpdateSchema.xml 相同的目錄中。  
  
     針對對應結構描述 (SampleUpdateSchema.xml) 指定的目錄路徑相對於儲存範本的目錄。 您也可以指定絕對路徑，例如：  
  
    ```  
    mapping-schema="C:\SqlXmlTest\SampleUpdateSchema.xml"  
    ```  
  
4.  建立和使用 SQLXML 4.0 測試指令碼 (Sqlxml4test.vbs) 以執行範本。  
  
     如需詳細資訊，請參閱 [使用 ADO 執行 SQLXML 4.0 查詢](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Updategram &#40;SQLXML 4.0&#41;的安全性考慮 ](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
