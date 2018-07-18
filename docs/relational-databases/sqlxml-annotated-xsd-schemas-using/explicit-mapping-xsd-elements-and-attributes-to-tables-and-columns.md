---
title: 明確的對應 XSD 元素和屬性對資料表和資料行 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- explicit schema mapping [SQLXML]
- XPath queries [SQLXML], annotated XSD schemas in queries
- sql:field
- row mapping [SQLXML]
- attribute mapping [SQLXML], explicit mapping
- field annotation
- XSD schemas [SQLXML], mapping attributes and elements
- names [SQLXML]
- relation annotation
- table/view mapping [SQLXML], explicit mapping
- sql:relation
- mapping schema [SQLXML], explicit mapping
- annotated XSD schemas, mapping attributes and elements
- column mapping [SQLXML]
- element mapping [SQLXML], explicit mapping
- table mapping [SQLXML], explicit mapping
- element/attribute mapping [SQLXML]
ms.assetid: 7a5ebeb6-7322-4141-a307-ebcf95976146
caps.latest.revision: 28
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 1836db12438017023637185d6e8ba24a6e533a77
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "38050201"
---
# <a name="explicit-mapping-xsd-elements-and-attributes-to-tables-and-columns"></a>明確的對應 XSD 元素和屬性對資料表和資料行
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  使用 XSD 結構描述提供關聯式資料庫的 XML 檢視表時，必須將結構描述的元素但屬性對應到資料庫的資料表和資料行。 資料庫資料表/檢視表中的資料列將會對應到 XML 文件中的元素。 資料庫中的資料行值會對應到屬性或元素。  
  
 針對註解式 XSD 結構描述指定 XPath 查詢時，結構描述中元素和屬性的資料會從所對應的資料表和資料行對應。 若要從資料庫取得單一值，在 XSD 結構描述中指定的對應必須同時擁有關聯和欄位規格。 如果元素/屬性的名稱不是所對應，資料表/檢視表或資料行名稱與同名**sql: relation**並**sql: field**註解用來指定項目之間的對應或XML 文件和資料表 （檢視） 或在資料庫中的資料行中的屬性。  
  
## <a name="sql-relation"></a>sql-relation  
 **Sql: relation**註解加入至資料庫資料表中對應的 XSD 結構描述中的 XML 節點。 資料表 （檢視） 名稱指定的值為**sql: relation**註釋。  
  
 當**sql: relation**元素上指定，此註釋的範圍會套用到所有的屬性和子項目，該項目，因此可提供以書面捷徑的複雜型別定義中所述註釋。  
  
 **Sql: relation**註解時也很有用的識別項，中的有效值[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]在 XML 中無效。 例如，"Order Details" 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中是有效的資料表名稱，但是在 XML 中是無效的。 在此情況下， **sql: relation**註釋可以用來指定對應，例如：  
  
```  
<xsd:element name="OD" sql:relation="[Order Details]">  
```  
  
## <a name="sql-field"></a>sql-field  
 **Sql 欄位**註解會將元素或屬性對應至資料庫資料行。 **Sql: field**註釋加入結構描述中的 XML 節點對應至資料庫資料行。 您無法指定**sql: field**空內容元素上。  
  
## <a name="examples"></a>範例  
 若要使用下列範例建立工作範例，您必須符合某些需求。 如需詳細資訊，請參閱 <<c0> [ 如需執行 SQLXML 範例的需求](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md)。  
  
### <a name="a-specifying-the-sqlrelation-and-sqlfield-annotations"></a>A. 指定 sql:relation 和 sql:field 註解  
 在此範例中，XSD 結構描述所組成**\<連絡人 >** 複雜類型元素 **\<FName >** 並 **\<LName >** 子項目和**ContactID**屬性。  
  
 **Sql: relation**註解 maps **\<連絡人 >** 至 AdventureWorks 資料庫中的 Person.Contact 資料表的項目。 **Sql: field**註解 maps  **\<FName >** FirstName 資料行的項目與 **\<LName >** LastName 的項目資料行。  
  
 指定任何註釋**ContactID**屬性。 這會導致將屬性預設對應到具有相同名稱的資料行。  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="Contact" sql:relation="Person.Contact" >  
   <xsd:complexType>  
     <xsd:sequence>  
        <xsd:element name="FName"  
                     sql:field="FirstName"   
                     type="xsd:string" />   
        <xsd:element name="LName"    
                     sql:field="LastName"    
                     type="xsd:string" />  
     </xsd:sequence>  
        <xsd:attribute name="ContactID"   
                       type="xsd:integer" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>針對結構描述測試範例 XPath 查詢  
  
1.  複製上述的結構描述程式碼，並將其貼到文字檔中。 將檔案儲存為 MySchema-annotated.xml。  
  
2.  複製下列範本，並將其貼到文字檔中。 將檔案儲存為 MySchema-annotatedT.xml 並放在與儲存 MySchema-annotated.xml 相同的目錄中。  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="MySchema-annotated.xml">  
        /Contact  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     針對對應結構描述 (MySchema-annotated.xml) 指定的目錄路徑，與儲存範本之目錄相關。 您也可以指定絕對路徑，例如：  
  
    ```  
    mapping-schema="C:\SqlXmlTest\MySchema-annotated.xml"  
    ```  
  
3.  建立和使用 SQLXML 4.0 測試指令碼 (Sqlxml4test.vbs) 以執行範本。  
  
     如需詳細資訊，請參閱 < [Ba6e326154d2"&gt;using ADO to Execute SQLXML Queries&lt](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
 部分結果集如下：  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">   
 <Contact ContactID="1">   
    <FName>Gustavo</FName>   
    <LName>Achong</LName>   
 </Contact>   
  .....  
</ROOT>  
```  
  
  
