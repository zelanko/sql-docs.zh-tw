---
title: 插入資料使用 XML Updategram (SQLXML 4.0) |Microsoft 文件
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- xsi:nil attribute
- unique values
- <after> block
- id attribute
- data insertions [SQLXML]
- nil attribute
- <before> block
- updg:guid attribute
- multiple record insertions
- returnid attribute
- updategrams [SQLXML], inserting data
- updg:at-identity attribute
- invalid characters [SQLXML]
- updg:returnid attribute
- updg:id attribute
- namespaces [SQLXML], updategrams
- IDENTITY-type column
- guid attribute
- record insertion [SQLXML]
- null values [SQLXML]
- at-identity attribute
- xml data type [SQL Server], SQLXML
ms.assetid: 4dc48762-bc12-43fb-b356-ea1b9c1e287e
caps.latest.revision: 33
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 563a79b68a39a886d70234f2e9f6eaae118d11ca
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="inserting-data-using-xml-updategrams-sqlxml-40"></a>使用 XML Updategram 插入資料 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  當記錄執行個體中出現時，updategram 代表插入作業**\<之後 >** 區塊，但不是在對應**\<之前 >** 區塊。 在此情況下，updategram 會插入在記錄**\<之後 >** 區塊至資料庫。  
  
 下列是插入作業的 Updategram 格式：  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync [mapping-schema="SampleSchema.xml"]  >  
   [<updg:before>  
   </updg:before>]  
    <updg:after [updg:returnid="x y ...] >  
       <ElementName [updg:id="value"]   
                   [updg:at-identity="x"]   
                   [updg:guid="y"]  
                   attribute="value"   
                   attribute="value"  
                   ...  
       />  
      [<ElementName .../>... ]  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
## <a name="before-block"></a>\<之前 > 區塊  
 **\<之前 >** 區塊可以省略插入作業。 如果選擇性**對應結構描述**未指定屬性，  **\<ElementName >** 指定在 updategram 並對應至資料庫資料表和子元素或屬性會對應到資料表中的資料行。  
  
## <a name="after-block"></a>\<之後 > 區塊  
 您可以指定一或多個記錄中的**\<之後 >** 區塊。  
  
 如果**\<之後 >** 區塊並不提供特定的資料行的值，updategram 會使用預設值 （如果已指定結構描述） 中的註解式結構描述所指定。 如果結構描述未指定資料行的預設值，updategram 未指定任何明確的值，這個資料行，而是指派[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]到此資料行預設值 （如果有指定）。 如果沒有 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 預設值，而資料行接受 NULL 值，則 Updategram 會將資料行值設定為 NULL。 如果資料行沒有預設值，也不接受 NULL 值，則命令會失敗，而 Updategram 傳回錯誤。 選擇性**updg: returnid**屬性用來傳回一筆記錄加入具有 IDENTITY 類型資料行的資料表時，由系統產生的識別值。  
  
## <a name="updgid-attribute"></a>updg:id 屬性  
 如果 updategram 只插入記錄，就不需要**updg: id**屬性。 如需有關**updg: id**，請參閱[更新資料使用 XML Updategram &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/updating-data-using-xml-updategrams-sqlxml-4-0.md)。  
  
## <a name="updgat-identity-attribute"></a>updg:at-identity 屬性  
 Updategram 時 updategram 在具有 IDENTITY 類型資料行的資料表中插入記錄，可以使用選擇性來擷取系統指派值**updg： 在識別**屬性。 Updategram 接著可以在後續作業中使用此值。 您可以在執行 updategram 時，傳回產生藉由指定的識別值**updg: returnid**屬性。  
  
## <a name="updgguid-attribute"></a>updg:guid 屬性  
 **Updg: guid**屬性是選擇性屬性，會產生全域唯一識別碼。 這個值保持在範圍內，整個**\<同步 >** 中其指定的區塊。 您可以使用此值任何位置，在**\<同步 >** 區塊。 該屬性會呼叫**newguid （)** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]函式來產生的唯一識別碼。  
  
## <a name="examples"></a>範例  
 若要建立工作範例使用下列範例，您必須符合指定的需求[執行 SQLXML 範例的需求](../../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md)。  
  
 使用 Updategram 範例之前，請注意下列事項：  
  
-   大部分的範例都會使用預設對應 (也就是說，Updategram 中不會指定任何對應結構描述)。 如需使用對應結構描述的 updategram 的範例，請參閱[在 Updategram 中指定註解式對應結構描述&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md)。  
  
-   大部分的範例都會使用 [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)] 範例資料庫。 所有的更新都會套用到此資料庫內的資料表。  
  
### <a name="a-inserting-a-record-by-using-an-updategram"></a>A. 使用 Updategram 插入記錄  
 這個屬性中心的 Updategram 會在 [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)] 資料庫中的 HumanResources.Employee 資料表內插入記錄。  
  
 在此範例中，Updategram 不會指定對應結構描述。 因此 Updategram 會使用預設對應，其中元素的名稱會對應到資料表名稱，而屬性或子元素則會對應到該資料表中的資料行。  
  
 HumanResources.Department 資料表的 [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)] 結構描述會對所有資料行賦予 'not null' 限制。 因此 Updategram 必須包含針對所有資料行所指定的值。 DepartmentID 是 IDENTITY 類型的資料行。 因此不會為它指定任何值。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync >  
    <updg:before>  
    </updg:before>  
    <updg:after>  
       <HumanResources.Department   
            Name="New Product Research"   
            GroupName="Research and Development"   
            ModifiedDate="2010-08-31"/>  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>針對結構描述測試範例 XPath 查詢  
  
1.  複製上述的 Updategram，並將其貼到文字檔中。 將檔案儲存為 MyUpdategram.xml。  
  
2.  建立和使用 SQLXML 4.0 測試指令碼 (Sqlxml4test.vbs) 以執行範本。  
  
     如需詳細資訊，請參閱[ADO to Execute SQLXML 4.0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
 在元素中心的對應中，Updategram 與下列類似：  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync >  
    <updg:before>  
    </updg:before>  
    <updg:after>  
       <HumanResources.Department>  
            <Name> New Product Research </Name>  
            <GroupName> Research and Development </GroupName>  
            <ModifiedDate>2010-08-31</ModifiedDate>  
       </HumanResources.Department>  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
 在混合模式 (元素中心和屬性中心) 的 Updategram 中，元素可以同時具有屬性和子元素，如以下 Updategram 所示：  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync >  
    <updg:before>  
    </updg:before>  
    <updg:after>  
       <HumanResources.Department   
            Name=" New Product Research "   
            <GroupName>Research and Development</GroupName>  
            <ModifiedDate>2010-08-31</ModifiedDate>  
       </HumanResources.Department>  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
### <a name="b-inserting-multiple-records-by-using-an-updategram"></a>B. 使用 Updategram 插入多筆記錄  
 這個 Updategram 會將兩筆新的值班記錄加入至 HumanResources.Shift 資料表。 Updategram 未指定選擇性**\<之前 >** 區塊。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync>  
    <updg:after >  
       <HumanResources.Shift Name="Day-Evening"  
                        StartTime="1900-01-01 11:00:00.000"  
                        EndTime="1900-01-01 19:00:00.000"  
                        ModifiedDate="2004-01-01 00:00:00.000" />  
       <HumanResources.Shift Name="Evening-Night"  
                        StartTime="1900-01-01 19:00:00.000"  
                        EndTime="1900-01-01 03:00:00.000"  
                        ModifiedDate="2004-01-01 00:00:00.000" />  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>針對結構描述測試範例 XPath 查詢  
  
1.  複製上述的 Updategram，並將其貼到文字檔中。 將檔案儲存為 Updategram-AddShifts.xml。  
  
2.  建立和使用 SQLXML 4.0 測試指令碼 (Sqlxml4test.vbs) 以執行範本。  
  
     如需詳細資訊，請參閱[ADO to Execute SQLXML 4.0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
 此範例中的另一個版本是使用兩個個別的 updategram **\<之後 >** 而不是要插入這兩個員工的一個區塊的區塊。 這是有效的方法，編碼方式如下：  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync>  
    <updg:after >  
       <HumanResources.Shift Name="Day-Evening"  
                        StartTime="1900-01-01 11:00:00.000"  
                        EndTime="1900-01-01 19:00:00.000"  
                        ModifiedDate="2004-01-01 00:00:00.000" />  
    </updg:after>  
    <updg:before>  
    </updg:before>  
    <updg:after >  
       <HumanResources.Shift Name="Evening-Night"  
                        StartTime="1900-01-01 19:00:00.000"  
                        EndTime="1900-01-01 03:00:00.000"  
                        ModifiedDate="2004-01-01 00:00:00.000" />  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
### <a name="c-working-with-valid-sql-server-characters-that-are-not-valid-in-xml"></a>C. 使用在 XML 中無效的有效 SQL Server 字元  
 在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中，資料表名稱可以包含空格，例如 Northwind 資料庫中的 Order Details 資料表。 不過，這不是有效的 XML 字元中有效[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]識別碼但不是有效的 XML 識別項，則可以使用編碼 '__xHHHH\_\_' 當做編碼值，其中 HHHH 代表四位數十六進位 ucs-2 碼最大顯著性位元第一順序的字元。  
  
> [!NOTE]  
>  此範例會使用 Northwind 資料庫。 您可以從這個下載中使用 SQL 指令碼，可用來安裝 Northwind 資料庫[Microsoft 寍鯚](http://go.microsoft.com/fwlink/?LinkId=30196)。  
  
 此外，項目名稱必須括在括號 ([]) 內。 因為字元 [和] 在 XML 中無效，您就必須將它們編碼為 _x005B\_和 _x005D\_分別。 (如果您使用對應結構描述，則可以提供不包含空格之類無效字元的元素。 對應結構描述會進行必要的對應，因此您就不必進行這些字元的編碼)。  
  
 下列 Updategram 會在 Northwind 資料庫的 Order Details 資料表中加入記錄：  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync >  
    <updg:before>  
    </updg:before>  
    <updg:after>  
      <_x005B_Order_x0020_Details_x005D_ OrderID="1"  
            ProductID="11"  
            UnitPrice="$1.0"  
            Quantity="1"  
            Discount="0.0" />  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
 Order Details 資料表中的 UnitPrice 資料行是**money**型別。 若要套用適當的類型轉換 (從**字串**類型**money**型別)、 錢幣符號字元 （$） 都必須加入為值的一部分。 如果 updategram 未指定對應結構描述的第一個字元**字串**值都會進行評估。 如果第一個字元為錢幣符號 ($)，則會套用適當的轉換。  
  
 如果 updategram 針對資料行適當地標示為對應結構描述指定**dt:type="fixed.14.4"** 或**sql: datatype ="money"**，就不需要錢幣符號 （$） 和轉換是由對應來處理。 這是建議的方式，可確保進行的是適當的類型轉換。  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>針對結構描述測試範例 XPath 查詢  
  
1.  複製上述的 Updategram，並將其貼到文字檔中。 將檔案儲存為 UpdategramSpacesInTableName.xml。  
  
2.  建立和使用 SQLXML 4.0 測試指令碼 (Sqlxml4test.vbs) 以執行範本。  
  
     如需詳細資訊，請參閱[ADO to Execute SQLXML 4.0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
### <a name="d-using-the-at-identity-attribute-to-retrieve-the-value-that-has-been-inserted-in-the-identity-type-column"></a>D. 使用 at-identity 屬性來擷取插入至 IDENTITY 類型之資料行的值  
 下列 Updategram 會插入兩筆記錄：在 Sales.SalesOrderHeader 資料表中插入一筆，而在 Sales.SalesOrderDetail 資料表中插入另一筆。  
  
 首先，Updategram 會將記錄加入至 Sales.SalesOrderHeader 資料表。 在這個資料表中，SalesOrderID 資料行是 IDENTITY 類型的資料行。 因此，當您將這筆記錄加入至資料表時，updategram 會使用**在身分識別**屬性來擷取指派的 SalesOrderID 值為"x"（預留位置值）。 Updategram 接著指定這個**在身分識別**變數中的 SalesOrderID 屬性的值作為\<Sales.SalesOrderDetail > 項目。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
 <updg:sync >  
  <updg:before>  
  </updg:before>  
  <updg:after>  
   <Sales.SalesOrderHeader updg:at-identity="x"   
             RevisionNumber="1"  
             OrderDate="2001-07-01 00:00:00.000"  
             DueDate="2001-07-13 00:00:00.000"  
             OnlineOrderFlag="0"  
             CustomerID="676"  
             ContactID="378"  
             BillToAddressID="985"  
             ShipToAddressID="985"  
             ShipMethodID="5"  
             SubTotal="24643.9362"  
             TaxAmt="1971.5149"  
             Freight="616.0984"  
             rowguid="00001111-2222-3333-4444-556677889900"  
             ModifiedDate="2001-07-08 00:00:00.000" />  
      <Sales.SalesOrderDetail SalesOrderID="x"  
                LineNumber="1"  
                OrderQty="1"  
                ProductID="776"  
                SpecialOfferID="1"  
                UnitPrice="2429.9928"  
                UnitPriceDiscount="0.00"  
                rowguid="aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee"  
                ModifiedDate="2001-07-01 00:00:00.000" />  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
 如果您想要傳回所產生的識別值**updg： 在識別**屬性，您可以使用**updg: returnid**屬性。 下列是經過修改的 Updategram，會傳回這個識別值  (此 Updategram 會加入兩筆訂單記錄和兩筆訂單詳細資料的記錄，以稍微增加範例的複雜度)。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
 <updg:sync>  
  <updg:before>  
  </updg:before>  
  <updg:after updg:returnid="x y" >  
       <HumanResources.Shift updg:at-identity="x" Name="Day-Evening"  
                        StartTime="1900-01-01 11:00:00.000"  
                        EndTime="1900-01-01 19:00:00.000"  
                        ModifiedDate="2004-01-01 00:00:00.000" />  
       <HumanResources.Shift updg:at-identity="y" Name="Evening-Night"  
                        StartTime="1900-01-01 19:00:00.000"  
                        EndTime="1900-01-01 03:00:00.000"  
                        ModifiedDate="2004-01-01 00:00:00.000" />  
  </updg:after>  
 </updg:sync>  
</ROOT>  
```  
  
 Updategram 在執行時會傳回類似下列的結果，其中包含所產生的識別值 (可用於資料表識別的 ShiftID 資料行產生值)：  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">   
  <returnid>   
    <x>4</x>   
    <y>5</y>   
  </returnid>   
</ROOT>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>針對結構描述測試範例 XPath 查詢  
  
1.  複製上述的 Updategram，並將其貼到文字檔中。 將檔案儲存為 Updategram-returnId.xml。  
  
2.  建立和使用 SQLXML 4.0 測試指令碼 (Sqlxml4test.vbs) 以執行範本。  
  
     如需詳細資訊，請參閱[ADO to Execute SQLXML 4.0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
### <a name="e-using-the-updgguid-attribute-to-generate-a-unique-value"></a>E. 使用 updg:guid 屬性來產生唯一值  
 在這個範例中，Updategram 會在 Cust 和 CustOrder 資料表中插入記錄， 此外，updategram 會產生唯一值來為 CustomerID 屬性使用**updg: guid**屬性。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync >  
    <updg:before>  
    </updg:before>  
    <updg:after updg:returnid="x" >  
      <Cust updg:guid="x" >  
         <CustID>x</CustID>  
         <LastName>Fuller</LastName>  
      </Cust>  
      <CustOrder>  
         <CustID>x</CustID>  
         <OrderID>1</OrderID>  
      </CustOrder>  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
 Updategram 會指定**returnid**屬性。 因此會傳回所產生的 GUID：  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <returnid>  
    <x>7111BD1A-7F0B-4CEE-B411-260DADFEFA2A</x>   
  </returnid>  
</ROOT>  
```  
  
##### <a name="to-test-the-updategram"></a>若要測試 Updategram  
  
1.  複製上述的 Updategram，並將其貼到文字檔中。 將檔案儲存為 Updategram-GenerateGuid.xml。  
  
2.  建立這些資料表：  
  
    ```  
    USE tempdb  
    CREATE TABLE Cust (CustID uniqueidentifier, LastName varchar(20))  
    CREATE TABLE CustOrder (CustID uniqueidentifier, OrderID int)  
    ```  
  
3.  建立和使用 SQLXML 4.0 測試指令碼 (Sqlxml4test.vbs) 以執行範本。  
  
     如需詳細資訊，請參閱[ADO to Execute SQLXML 4.0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
### <a name="f-specifying-a-schema-in-an-updategram"></a>F. 在 Updategram 中指定結構描述  
 這個範例中的 Updategram 會在下列資料表中插入記錄：  
  
```  
CustOrder(OrderID, EmployeeID, OrderType)  
```  
  
 這個 Updategram 中指定了 XSD 結構描述 (也就是說，沒有 Updategram 元素和屬性的預設對應)。 該結構描述提供元素和屬性對資料庫資料表和資料行的必要對應。  
  
 下列的結構描述 (CustOrderSchema.xml) 描述 **\<CustOrder >** 所組成的項目**OrderID**和**EmployeeID**屬性。 為了讓結構描述更有可看性，預設值指派給**EmployeeID**屬性。 Updategram 只會將屬性的預設值用於插入作業，而且只有在 Updategram 未指定該屬性時才會這麼做。  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="CustOrder" >  
   <xsd:complexType>  
        <xsd:attribute name="OrderID"     type="xsd:integer" />   
        <xsd:attribute name="EmployeeID"  type="xsd:integer" />  
        <xsd:attribute name="OrderType  " type="xsd:integer" default="1"/>  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 這個 Updategram 會將記錄插入至 CustOrder 資料表。 Updategram 只會指定 OrderID 和 EmployeeID 屬性值， 而不會指定 OrderType 屬性值。 因此，Updategram 會使用在前述結構描述中所指定之 EmployeeID 屬性的預設值。  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql"  
             xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync mapping-schema='CustOrderSchema.xml'>  
<updg:after>  
       <CustOrder OrderID="98000" EmployeeID="1" />  
</updg:after>  
</updg:sync>  
</ROOT>  
```  
  
 如需指定對應結構描述的 updategram 的範例，請參閱[在 Updategram 中指定註解式對應結構描述&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md)。  
  
##### <a name="to-test-the-updategram"></a>若要測試 Updategram  
  
1.  建立這個資料表中的**tempdb**資料庫：  
  
    ```  
    USE tempdb  
    CREATE TABLE CustOrder(  
                     OrderID int,   
                     EmployeeID int,   
                     OrderType int)  
    ```  
  
2.  複製上述的結構描述，並將其貼到文字檔中。 然後將檔案儲存為 CustOrderSchema.xml。  
  
3.  複製上述的 Updategram，並將其貼到文字檔中。 然後將檔案在前述步驟所使用的相同資料夾中，儲存為 CustOrderUpdategram.xml。  
  
4.  建立及使用 SQLXML 4.0 測試指令碼 (Sqlxml4test.vbs) 以執行 Updategram。  
  
     如需詳細資訊，請參閱[ADO to Execute SQLXML 4.0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
 這是相等的 XDR 結構描述：  
  
```  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"  
        xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
 <ElementType name="CustOrder" >  
    <AttributeType name="OrderID" />  
    <AttributeType name="EmployeeID" />  
    <AttributeType name="OrderType" default="1" />  
    <attribute type="OrderID"  />  
    <attribute type="EmployeeID" />  
    <attribute type="OrderType" />  
  </ElementType>  
</Schema>  
```  
  
### <a name="g-using-the-xsinil-attribute-to-insert-null-values-in-a-column"></a>G. 使用 xsi:nil 屬性在資料行中插入 Null 值  
 如果您想要在資料表中的對應資料行中插入 null 值，您可以指定**xsi: nil**在 updategram 中的項目上的屬性。 在對應的 XSD 結構描述，XSD **nillable**也必須指定屬性。  
  
 例如，請考慮下列 XSD 結構描述：  
  
```  
<?xml version="1.0"?>  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:element name="Student" sql:relation="Students">  
  <xsd:complexType>  
    <xsd:all>  
      <xsd:element name="fname" sql:field="first_name"   
                                type="xsd:string"   
                                 nillable="true"/>  
    </xsd:all>  
    <xsd:attribute name="SID"   
                        sql:field="StudentID"  
                        type="xsd:ID"/>      
    <xsd:attribute name="lname"       
                        sql:field="last_name"  
                        type="xsd:string"/>  
    <xsd:attribute name="minitial"    
                        sql:field="middle_initial"   
                        type="xsd:string"/>  
    <xsd:attribute name="years"       
                         sql:field="no_of_years"  
                         type="xsd:integer"/>  
  </xsd:complexType>  
 </xsd:element>  
</xsd:schema>  
```  
  
 XSD 結構描述指定**nillable ="true"** 如 **\<fname >** 項目。 下列 Updategram 會使用這個結構描述：  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql"  
      xmlns:updg="urn:schemas-microsoft-com:xml-updategram"  
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
  
<updg:sync mapping-schema='StudentSchema.xml'>  
  <updg:before/>  
  <updg:after>  
    <Student SID="S00004" lname="Elmaci" minitial="" years="2">  
      <fname xsi:nil="true">  
    </fname>  
    </Student>  
  </updg:after>  
</updg:sync>  
  
</ROOT>  
```  
  
 Updategram 會指定**xsi: nil**如 **\<fname >** 中的項目**\<之後 >** 區塊。 因此，這個 Updategram 在執行時，會為資料表中的 first_name 資料行插入 NULL 值。  
  
##### <a name="to-test-the-updategram"></a>若要測試 Updategram  
  
1.  建立下列資料表中的**tempdb**資料庫：  
  
    ```  
    USE tempdb  
    CREATE TABLE Students (  
       StudentID char(6)NOT NULL ,  
       first_name varchar(50),  
       last_name varchar(50),  
       middle_initial char(1),  
       no_of_years int NULL)  
    GO  
    ```  
  
2.  複製上述的結構描述，並將其貼到文字檔中。 然後將檔案儲存為 StudentSchema.xml。  
  
3.  複製上述的 Updategram，並將其貼到文字檔中。 然後將檔案在前述步驟所使用的相同資料夾中，儲存為 StudentUpdategram.xml 以儲存 StudentSchema.xml。  
  
4.  建立及使用 SQLXML 4.0 測試指令碼 (Sqlxml4test.vbs) 以執行 Updategram。  
  
     如需詳細資訊，請參閱[ADO to Execute SQLXML 4.0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
### <a name="h-specifying-namespaces-in-an-updategram"></a>H. 在 Updategram 中指定命名空間  
 您在 Updategram 中所擁有的元素，可能會屬於在 Updategram 的相同元素中宣告的命名空間。 在這種情況下，相對應的結構描述必須也要宣告相同的命名空間，且元素必須屬於該目標命名空間。  
  
 例如，在下列 updategram (Updategram-elementhavingnamespace.xml)， **\<順序 >** 元素屬於項目中所宣告的命名空間。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync mapping-schema='XSD-ElementHavingNameSpace.xml'>  
    <updg:after>  
       <x:Order  xmlns:x="http://server/xyz/schemas/"  
             updg:at-identity="SalesOrderID"   
             RevisionNumber="1"  
             OrderDate="2001-07-01 00:00:00.000"  
             DueDate="2001-07-13 00:00:00.000"  
             OnlineOrderFlag="0"  
             CustomerID="676"  
             ContactID="378"  
             BillToAddressID="985"  
             ShipToAddressID="985"  
             ShipMethodID="5"  
             SubTotal="24643.9362"  
             TaxAmt="1971.5149"  
             Freight="616.0984"  
             rowguid="00009999-8888-7777-6666-554433221100"  
             ModifiedDate="2001-07-08 00:00:00.000" />  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
 在這種情況下，結構描述必須也要宣告命名空間，如下列結構描述所示：  
  
 下列結構描述 (XSD-ElementHavingNamespace.xml) 顯示相對應元素和屬性的宣告方式。  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
     xmlns:dt="urn:schemas-microsoft-com:datatypes"   
     xmlns:sql="urn:schemas-microsoft-com:mapping-schema"    
     xmlns:x="http://server/xyz/schemas/"   
     targetNamespace="http://server/xyz/schemas/" >  
  <xsd:element name="Order" sql:relation="Sales.SalesOrderHeader" type="x:Order_type"/>  
  <xsd:complexType name="Order_type">  
    <xsd:attribute name="SalesOrderID"  type="xsd:ID"/>  
    <xsd:attribute name="RevisionNumber" type="xsd:unsignedByte"/>  
    <xsd:attribute name="OrderDate" type="xsd:dateTime"/>  
    <xsd:attribute name="DueDate" type="xsd:dateTime"/>  
    <xsd:attribute name="ShipDate" type="xsd:dateTime"/>  
    <xsd:attribute name="Status" type="xsd:unsignedByte"/>  
    <xsd:attribute name="OnlineOrderFlag" type="xsd:boolean"/>  
    <xsd:attribute name="SalesOrderNumber" type="xsd:string"/>  
    <xsd:attribute name="PurchaseOrderNumber" type="xsd:string"/>  
    <xsd:attribute name="AccountNumber" type="xsd:string"/>  
    <xsd:attribute name="CustomerID" type="xsd:int"/>  
    <xsd:attribute name="ContactID" type="xsd:int"/>  
    <xsd:attribute name="SalesPersonID" type="xsd:int"/>  
    <xsd:attribute name="TerritoryID" type="xsd:int"/>  
    <xsd:attribute name="BillToAddressID" type="xsd:int"/>  
    <xsd:attribute name="ShipToAddressID" type="xsd:int"/>  
    <xsd:attribute name="ShipMethodID" type="xsd:int"/>  
    <xsd:attribute name="CreditCardID" type="xsd:int"/>  
    <xsd:attribute name="CreditCardApprovalCode" type="xsd:string"/>  
    <xsd:attribute name="CurrencyRateID" type="xsd:int"/>  
    <xsd:attribute name="SubTotal" type="xsd:decimal"/>  
    <xsd:attribute name="TaxAmt" type="xsd:decimal"/>  
    <xsd:attribute name="Freight" type="xsd:decimal"/>  
    <xsd:attribute name="TotalDue" type="xsd:decimal"/>  
    <xsd:attribute name="Comment" type="xsd:string"/>  
    <xsd:attribute name="rowguid" type="xsd:string"/>  
    <xsd:attribute name="ModifiedDate" type="xsd:dateTime"/>  
  </xsd:complexType>  
</xsd:schema>  
```  
  
##### <a name="to-test-the-updategram"></a>若要測試 Updategram  
  
1.  複製上述的結構描述，並將其貼到文字檔中。 將檔案儲存為 XSD-ElementHavingNamespace.xml。  
  
2.  複製上述的 Updategram，並將其貼到文字檔中。 在用來儲存 XSD-ElementHavingnamespace.xml 的相同資料夾中，將檔案儲存為 Updategram-ElementHavingNamespace.xml。  
  
3.  建立及使用 SQLXML 4.0 測試指令碼 (Sqlxml4test.vbs) 以執行 Updategram。  
  
     如需詳細資訊，請參閱[ADO to Execute SQLXML 4.0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
### <a name="i-inserting-data-into-an-xml-data-type-column"></a>I. 將資料插入至 XML 資料類型資料行  
 **Xml**資料型別在引進[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]。 您可以使用 updategram 來插入及更新資料儲存在**xml**資料類型資料行具有下列規定：  
  
-   **Xml**資料行無法用於識別現有的資料列。 因此，不能包含在**updg： 之前**updategram 的區段。  
  
-   命名空間範圍中的 XML 片段插入**xml**資料行，將會保留並將其命名空間宣告加入到所插入片段的最上層元素。  
  
 例如，在下列 updategram (SampleUpdateGram.xml)，  **\<Desc >** 元素會更新在生產環境中的 ProductDescription 資料行 > 的 Production>productmodel 資料表內[!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)]範例資料庫。 這個 updategram 的結果是，ProductDescription 資料行的 XML 內容的 XML 內容的更新 **\<Desc >** 項目。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
    <updg:sync mapping-schema="SampleSchema.xml" >  
       <updg:before>  
<ProductModel ProductModelID="19">  
   <Name>Mountain-100</Name>  
</ProductModel>  
    </updg:before>  
    <updg:after>  
 <ProductModel>  
    <Name>Mountain-100</Name>  
    <Desc><?xml-stylesheet href="ProductDescription.xsl" type="text/xsl"?>  
        <p1:ProductDescription xmlns:p1="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription"   
              xmlns:wm="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain"   
              xmlns:wf="http://www.adventure-works.com/schemas/OtherFeatures"   
              xmlns:html="http://www.w3.org/1999/xhtml"   
              xmlns="">  
  <p1:Summary>  
     <html:p>Insert Example</html:p>  
  </p1:Summary>  
  <p1:Manufacturer>  
    <p1:Name>AdventureWorks</p1:Name>  
    <p1:Copyright>2002</p1:Copyright>  
    <p1:ProductURL>HTTP://www.Adventure-works.com</p1:ProductURL>  
  </p1:Manufacturer>  
  <p1:Features>These are the product highlights.   
    <wm:Warranty>  
       <wm:WarrantyPeriod>3 years</wm:WarrantyPeriod>  
       <wm:Description>parts and labor</wm:Description>  
    </wm:Warranty>  
    <wm:Maintenance>  
       <wm:NoOfYears>10 years</wm:NoOfYears>  
       <wm:Description>maintenance contract available through your dealer or any AdventureWorks retail store.</wm:Description>  
    </wm:Maintenance>  
    <wf:wheel>High performance wheels.</wf:wheel>  
    <wf:saddle>  
      <html:i>Anatomic design</html:i> and made from durable leather for a full-day of riding in comfort.</wf:saddle>  
    <wf:pedal>  
       <html:b>Top-of-the-line</html:b> clipless pedals with adjustable tension.</wf:pedal>  
    <wf:BikeFrame>Each frame is hand-crafted in our Bothell facility to the optimum diameter and wall-thickness required of a premium mountain frame. The heat-treated welded aluminum frame has a larger diameter tube that absorbs the bumps.</wf:BikeFrame>  
    <wf:crankset> Triple crankset; alumunim crank arm; flawless shifting. </wf:crankset>  
   </p1:Features>  
   <p1:Picture>  
      <p1:Angle>front</p1:Angle>  
      <p1:Size>small</p1:Size>  
      <p1:ProductPhotoID>118</p1:ProductPhotoID>  
   </p1:Picture>  
   <p1:Specifications> These are the product specifications.  
     <Material>Almuminum Alloy</Material>  
     <Color>Available in most colors</Color>  
     <ProductLine>Mountain bike</ProductLine>  
     <Style>Unisex</Style>  
     <RiderExperience>Advanced to Professional riders</RiderExperience>  
   </p1:Specifications>  
  </p1:ProductDescription>  
 </Desc>  
      </ProductModel>  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
 Updategram 會參考下列的註解 XSD 結構描述 (SampleSchema.xml)。  
  
```  
<?xml version="1.0" encoding="utf-8" ?>  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
           xmlns:sql="urn:schemas-microsoft-com:mapping-schema"  
           xmlns="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">   
  <xsd:element name="ProductModel"  sql:relation="Production.ProductModel" >  
     <xsd:complexType>  
       <xsd:sequence>  
          <xsd:element name="Name" type="xsd:string"></xsd:element>  
          <xsd:element name="Desc" sql:field="CatalogDescription" sql:datatype="xml">  
           <xsd:complexType>  
            <xsd:sequence>  
              <xsd:element name="ProductDescription">  
                 <xsd:complexType>  
                   <xsd:sequence>  
                     <xsd:element name="Summary" type="xsd:anyType">  
                     </xsd:element>  
                   </xsd:sequence>  
                 </xsd:complexType>  
              </xsd:element>  
            </xsd:sequence>  
           </xsd:complexType>  
          </xsd:element>   
       </xsd:sequence>  
       <xsd:attribute name="ProductModelID" sql:field="ProductModelID"/>  
     </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-test-the-updategram"></a>若要測試 Updategram  
  
1.  複製上述的結構描述，並將其貼到文字檔中。 然後將檔案儲存為 XSD-SampleSchema.xml。  
  
    > [!NOTE]  
    >  因為 updategram 支援預設對應，所以沒有任何方法來識別開頭和結尾**xml**資料型別。 實際上，這表示，對應結構描述時，需要插入或更新資料表**xml**資料類型資料行。 如果沒有提供結構描述，則 SQLXML 會傳回錯誤，指出資料表中遺失其中一個資料行。  
  
2.  複製上述的 Updategram，並將其貼到文字檔中。 然後將檔案在用來儲存 SampleSchema.xml 的相同資料夾中，儲存為 SampleUpdategram.xml。  
  
3.  建立及使用 SQLXML 4.0 測試指令碼 (Sqlxml4test.vbs) 以執行 Updategram。  
  
     如需詳細資訊，請參閱[ADO to Execute SQLXML 4.0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Updategram 安全性考量&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
