---
title: XSD 元素和屬性對資料表和資料行 (SQLXML 4.0) 的明確對應 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 72dfbcbd1ff264e596eecfecb5ebf759c2cbf5e9
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/22/2019
ms.locfileid: "66013838"
---
# <a name="explicit-mapping-of-xsd-elements-and-attributes-to-tables-and-columns-sqlxml-40"></a>XSD 元素和屬性對資料表和資料行的明確對應 (SQLXML 4.0)
  使用 XSD 結構描述提供關聯式資料庫的 XML 檢視表時，必須將結構描述的元素但屬性對應到資料庫的資料表和資料行。 資料庫資料表/檢視表中的資料列將會對應到 XML 文件中的元素。 資料庫中的資料行值會對應到屬性或元素。  
  
 針對註解式 XSD 結構描述指定 XPath 查詢時，結構描述中元素和屬性的資料會從所對應的資料表和資料行對應。 若要從資料庫取得單一值，在 XSD 結構描述中指定的對應必須同時擁有關聯和欄位規格。 如果元素/屬性的名稱與資料表/檢視表或所對應的資料行名稱不同，則會將 `sql:relation` 和 `sql:field` 屬性用於指定 XML 文件中之元素或屬性和資料庫中之資料表 (檢視表) 或資料行之間的對應。  
  
## <a name="sql-relation"></a>sql-relation  
 加入 `sql:relation` 註解，將 XSD 結構描述中的 XML 節點對應至資料庫資料表。 資料表 (檢視表) 的名稱會指定為 `sql:relation` 註解的值。  
  
 在元素上指定 `sql:relation` 時，此註解的範圍會套用到該元素之複雜類型定義中描述的所有屬性和子元素中，因此可在撰寫註解時提供捷徑。  
  
 `sql:relation`註解時也很有用的識別項，中的有效值[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]在 XML 中無效。 例如，"Order Details" 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中是有效的資料表名稱，但是在 XML 中是無效的。 在這種情況下，可以使用 `sql:relation` 註解來指定對應，例如：  
  
```  
<xsd:element name="OD" sql:relation="[Order Details]">  
```  
  
## <a name="sql-field"></a>sql-field  
 `sql-field` 註解會將元素或屬性對應到資料庫資料行。 加入 `sql:field` 註解，將結構描述中的 XML 節點對應至資料庫資料行。 您無法在空內容元素上指定 `sql:field`。  
  
## <a name="examples"></a>範例  
 若要使用下列範例建立工作範例，您必須符合某些需求。 如需詳細資訊，請參閱 <<c0> [ 如需執行 SQLXML 範例的需求](../sqlxml/requirements-for-running-sqlxml-examples.md)。  
  
### <a name="a-specifying-the-sqlrelation-and-sqlfield-annotations"></a>A. 指定 sql:relation 和 sql:field 註解  
 在此範例中，XSD 結構描述所組成**\<連絡人 >** 複雜類型元素 **\<FName >** 並 **\<LName >** 子項目和**ContactID**屬性。  
  
 `sql:relation`註解 maps **\<連絡人 >** 至 AdventureWorks 資料庫中的 Person.Contact 資料表的項目。 `sql:field`註解 maps  **\<FName >** FirstName 資料行的項目和 **\<LName >** 到 LastName 資料行的項目。  
  
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
  
     如需詳細資訊，請參閱 [使用ADO執行SQLXML查詢](../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
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
  
  
