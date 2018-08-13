---
title: '識別索引鍵資料行使用 sql: key-fields 來-欄位 (SQLXML 4.0) |Microsoft Docs'
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- nesting XML results
- proper nesting in results [SQLXML]
- sql:key-fields
- XSD schemas [SQLXML], key columns
- identifying key columns [SQLXML]
- annotated XSD schemas, key columns
- key columns [SQLXML]
- relationships [SQLXML], key columns
- hierarchical relationships [SQLXML]
- key-fields annotation
ms.assetid: 1a5ad868-8602-45c4-913d-6fbb837eebb0
caps.latest.revision: 27
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 3e75779626c8769c609fa27f97b44562d3e9a8aa
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/06/2018
ms.locfileid: "39535558"
---
# <a name="identifying-key-columns-using-sqlkey-fields-sqlxml-40"></a>使用 sql:key-fields 來識別索引鍵資料行 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  針對 XSD 結構描述指定 XPath 查詢時，在大部分情況下都需要索引鍵資訊，才能在結果中取得正確的巢狀結構。 指定**sql: key-fields 來-欄位**註解是一種確保會產生適當階層。  
  
> [!NOTE]  
>  若要確保適當的巢狀結構，建議您指定**sql: key-fields 來-欄位**對應至資料表的項目。 產生的 XML 會區分基礎結果集的排序。 如果**sql: key-fields 來-欄位**未指定，則產生的 XML 可能格式不正確。  
  
 值**sql: key-fields 來-欄位**識別可唯一識別關聯性中的資料列的資料行。 如果需要多個資料行才能唯一識別某個資料列，這些資料行值就會以空格隔開。  
  
 您必須使用**sql: key-fields 來-欄位**註解時項目中含有 **\<sql: relationship >** 的項目和子元素之間定義，但並不提供的主索引鍵父元素中指定的資料表。  
  
## <a name="examples"></a>範例  
 若要使用下列範例建立工作範例，您必須符合某些需求。 如需詳細資訊，請參閱 <<c0> [ 如需執行 SQLXML 範例的需求](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md)。  
  
### <a name="a-producing-the-appropriate-nesting-when-sqlrelationship-does-not-provide-sufficient-information"></a>A. 產生適當巢狀結構時\<sql: relationship > 不會提供足夠的資訊  
 此範例會示範何處**sql: key-fields 來-欄位**必須指定。  
  
 請考慮下列結構描述。 結構描述指定的階層之間**\<順序 >** 並**\<客戶 >** 中的項目**\<順序 >** 元素是父系和**\<客戶 >** 項目是子系。  
  
 **\<Sql: relationship >** 標記用來指定父子式關聯性。 它會將 Sales.SalesOrderHeader 資料表中的 CustomerID 識別為參考 Sales.Customer 資料表中 CustomerID 子索引鍵的父索引鍵。 中提供的資訊 **\<sql: relationship >** 不足以唯一識別父資料表 (Sales.SalesOrderHeader) 中的資料列。 因此，如果沒有**sql: key-fields 來-欄位**註解，產生的階層是不正確。  
  
 具有**sql: key-fields 來-欄位**上指定**\<順序 >**、 註解可唯一識別父系 （Sales.SalesOrderHeader 資料表） 中的資料列，而且其子項目會顯示其父代。  
  
 這是結構描述：  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="OrdCust"  
        parent="Sales.SalesOrderHeader"  
        parent-key="CustomerID"  
        child="Sales.Customer"  
        child-key="CustomerID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  <xsd:element name="Order" sql:relation="Sales.SalesOrderHeader"   
               sql:key-fields="SalesOrderID">  
   <xsd:complexType>  
     <xsd:sequence>  
     <xsd:element name="Customer" sql:relation="Sales.Customer"   
                       sql:relationship="OrdCust"  >  
       <xsd:complexType>  
         <xsd:attribute name="CustID" sql:field="CustomerID" />  
         <xsd:attribute name="SoldBy" sql:field="SalesPersonID" />  
       </xsd:complexType>  
     </xsd:element>  
     </xsd:sequence>  
     <xsd:attribute name="SalesOrderID" type="xsd:integer" />  
     <xsd:attribute name= "CustomerID" type="xsd:string" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-create-a-working-sample-of-this-schema"></a>若要建立這個結構描述的工作範例  
  
1.  複製上述的結構描述程式碼，並將其貼到文字檔中。 將檔案儲存為 KeyFields1.xml。  
  
2.  複製下列範本，並將其貼到文字檔中。 將檔案儲存為 KeyFields1T.xml，並放在儲存 KeyFields1.xml 的相同目錄中。 在範本中的 XPath 查詢會傳回所有**\<順序 >** customerid 小於 3 的項目。  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
        <sql:xpath-query mapping-schema="KeyFields1.xml">  
            /Order[@CustomerID < 3]  
        </sql:xpath-query>  
    </ROOT>  
    ```  
  
     針對對應結構描述 (KeyFields1.xml) 指定的目錄路徑相對於儲存範本的目錄。 您也可以指定絕對路徑，例如：  
  
    ```  
    mapping-schema="C:\MyDir\KeyFields1.xml"  
    ```  
  
3.  建立和使用 SQLXML 4.0 測試指令碼 (Sqlxml4test.vbs) 以執行範本。  
  
     如需詳細資訊，請參閱 < [Ba6e326154d2"&gt;using ADO to Execute SQLXML Queries&lt](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
 這是部分結果集：  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
    <Order SalesOrderID="43860" CustomerID="1">  
       <Customer CustID="1" SoldBy="280"/>  
    </Order>  
    <Order SalesOrderID="44501" CustomerID="1">  
       <Customer CustID="1" SoldBy="280"/>  
    </Order>  
    <Order SalesOrderID="45283" CustomerID="1">  
       <Customer CustID="1" SoldBy="280"/>  
    </Order>  
    .....  
</ROOT>  
```  
  
### <a name="b-specifying-sqlkey-fields-to-produce-proper-nesting-in-the-result"></a>B. 指定 sql:key-fields 在結果中產生適當的巢狀結構  
 在下列結構描述中，沒有使用指定的階層 **\<sql: relationship >**。 此結構描述仍然需要指定**sql: key-fields 來-欄位**註釋來唯一識別 HumanResources.Employee 資料表中的員工。  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="HumanResources.Employee" sql:key-fields="EmployeeID" >  
   <xsd:complexType>  
     <xsd:sequence>  
        <xsd:element name="Title">  
          <xsd:complexType>  
            <xsd:simpleContent>  
              <xsd:extension base="xsd:string">  
                 <xsd:attribute name="EmployeeID" type="xsd:integer" />  
              </xsd:extension>  
            </xsd:simpleContent>  
          </xsd:complexType>  
        </xsd:element>  
     </xsd:sequence>  
   </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-create-a-working-sample-of-this-schema"></a>若要建立這個結構描述的工作範例  
  
1.  複製上述的結構描述程式碼，並將其貼到文字檔中。 將檔案儲存為 KeyFields2.xml。  
  
2.  複製下列範本，並將其貼到文字檔中。 將檔案儲存為 KeyFields2T.xml，並放在儲存 KeyFields2.xml 的相同目錄中。 在範本中的 XPath 查詢會傳回所有 **\<HumanResources.Employee >** 項目：  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="KeyFields2.xml">  
        /HumanResources.Employee  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     針對對應結構描述 (KeyFields2.xml) 指定的目錄路徑相對於儲存範本的目錄。 您也可以指定絕對路徑，例如：  
  
    ```  
    mapping-schema="C:\MyDir\KeyFields2.xml"  
    ```  
  
3.  建立和使用 SQLXML 4.0 測試指令碼 (Sqlxml4test.vbs) 以執行範本。  
  
     如需詳細資訊，請參閱 < [Ba6e326154d2"&gt;using ADO to Execute SQLXML Queries&lt](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
 以下是結果：  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <HumanResources.Employee>  
    <Title EmployeeID="1">Production Technician - WC60</Title>   
  </HumanResources.Employee>  
  <HumanResources.Employee>  
    <Title EmployeeID="2">Marketing Assistant</Title>   
  </HumanResources.Employee>  
  <HumanResources.Employee>  
    <Title EmployeeID="3">Engineering Manager</Title>   
  </HumanResources.Employee>  
  ...  
</ROOT>  
```  
  
  
