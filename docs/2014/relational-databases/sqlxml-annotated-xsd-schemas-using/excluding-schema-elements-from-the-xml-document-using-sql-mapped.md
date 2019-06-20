---
title: 結構描述元素排除產生 XML 文件使用 sql： 對應 (SQLXML 4.0) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- element does not map [SQLXML]
- annotated XSD schemas, excluding schema elements
- mapped annotation
- table mapping [SQLXML], excluding schema elements
- sql:mapped
- excluding schema elements
- element mapping [SQLXML], excluding schema elements
- column mapping [SQLXML]
- XSD schemas [SQLXML], excluding schema elements
- attribute mapping [SQLXML], excluding schema elements
- table/view mapping [SQLXML], excluding schema elements
ms.assetid: 7d2649dd-0038-4a2c-b16d-f80f7c306966
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 865a9af892f948e77aa593d3713766e7860349b0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66013865"
---
# <a name="excluding-schema-elements-from-the-resulting-xml-document-using-sqlmapped-sqlxml-40"></a>使用 sql:mapped 從產生的 XML 文件排除結構描述元素 (SQLXML 4.0)
  XSD 結構描述中的每個元素和屬性都會因為預設對應，而對應到資料庫資料表/檢視表和資料行。 如果您要在 XSD 結構中建立沒有對應到任何資料庫資料表 (檢視表) 或資料行，而且沒有出現在 XML 中的元素，您可以指定 `sql:mapped` 註解。  
  
 如果無法修改結構描述，或者如果結構描述用於驗證來自其他來源的 XML，而且不包含未儲存在資料庫中的資料，則 `sql:mapped` 註解特別實用。 `sql:mapped` 註解與 `sql:is-constant` 不同之處在於，未對應的元素和屬性不會出現在 XML 文件中。  
  
 `sql:mapped` 註解接受布林值 (0 = false，1 = true)。 可接受的值為 0、1、true 和 false。  
  
## <a name="examples"></a>範例  
 若要使用下列範例建立工作範例，您必須符合某些需求。 如需詳細資訊，請參閱 <<c0> [ 如需執行 SQLXML 範例的需求](../sqlxml/requirements-for-running-sqlxml-examples.md)。  
  
### <a name="a-specifying-the-sqlmapped-annotation"></a>A. 指定 sql:mapped 註解  
 假設您有來自其他來源的 XSD 結構描述。 此 XSD 結構描述組成 **\<Person.Contact >** 項目**ContactID**， **FirstName**， **LastName**，和**HomeAddress**屬性。  
  
 此 XSD 結構描述對應至 AdventureWorks 資料庫中的 Person.Contact 資料表中`sql:mapped`上指定**HomeAddress**屬性，因為 Employees 資料表不會儲存員工的住家地址。 因此，根據對應結構描述指定 XPath 查詢時，此屬性不會對應到資料庫，而且不會在產生的 XML 文件中傳回。  
  
 預設的對應發生於其餘的結構描述。 **\<Person.Contact >** 元素會對應至 Person.Contact 資料表中，而所有屬性都會都對應到 Person.Contact 資料表中的相同名稱的資料行。  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="Person.Contact">  
    <xsd:complexType>  
      <xsd:attribute name="ContactID"   type="xsd:string"/>  
      <xsd:attribute name="FirstName"    type="xsd:string" />  
      <xsd:attribute name="LastName"     type="xsd:string" />  
      <xsd:attribute name="HomeAddress" type="xsd:string"   
                     sql:mapped="false" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>針對結構描述測試範例 XPath 查詢  
  
1.  複製上述的結構描述程式碼，並將其貼到文字檔中。 將檔案儲存為 sql-mapped.xml。  
  
2.  複製下列範本，並將其貼到文字檔中。 將檔案儲存為 sql-mappedT.xml 並放在與儲存 sql-mapped.xml 相同的目錄中。  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
        <sql:xpath-query mapping-schema="sql-mapped.xml">  
            /Person.Contact[@ContactID < 10]  
        </sql:xpath-query>  
    </ROOT>  
    ```  
  
     針對對應結構描述 (MySchema.xml) 指定的目錄路徑，相對於儲存範本的目錄。 您也可以指定絕對路徑，例如：  
  
    ```  
    mapping-schema="C:\MyDir\sql-mapped.xml"  
    ```  
  
3.  建立和使用 SQLXML 4.0 測試指令碼 (Sqlxml4test.vbs) 以執行範本。  
  
     如需詳細資訊，請參閱 [使用ADO執行SQLXML查詢](../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
 結果集如下：  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Person.Contact ContactID="1" FirstName="Gustavo" LastName="Achong" />   
  <Person.Contact ContactID="2" FirstName="Catherine" LastName="Abel" />   
  <Person.Contact ContactID="3" FirstName="Kim" LastName="Abercrombie" />   
  <Person.Contact ContactID="4" FirstName="Humberto" LastName="Acevedo" />   
  <Person.Contact ContactID="5" FirstName="Pilar" LastName="Ackerman" />   
  <Person.Contact ContactID="6" FirstName="Frances" LastName="Adams" />   
  <Person.Contact ContactID="7" FirstName="Margaret" LastName="Smith" />   
  <Person.Contact ContactID="8" FirstName="Carla" LastName="Adams" />   
  <Person.Contact ContactID="9" FirstName="Jay" LastName="Adams" />   
</ROOT>  
```  
  
 請注意，ContactID、FirstName 和 LastName 存在，但是 HomeAddress 不存在，因為對應結構描述為 `sql:mapped` 屬性指定 0。  
  
## <a name="see-also"></a>另請參閱  
 [XSD 元素和屬性對資料表和資料行的預設對應&#40;SQLXML 4.0&#41;](default-mapping-of-xsd-elements-and-attributes-to-tables-and-columns-sqlxml-4-0.md)  
  
  
