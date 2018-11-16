---
title: 'CDATA 區段使用 sql: use-cdata 建立-(SQLXML 4.0) |Microsoft Docs'
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- markup characters [SQLXML]
- special characters [SQLXML]
- use-cdata annotation
- plain text [SQLXML]
- CDATA sections
- escaping blocks of text [SQLXML]
- annotated XSD schemas, CDATA sections
- sql:use-cdata
ms.assetid: 26d2b9dc-f857-44ff-bcd4-aaf64ff809d0
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8ed36a17744c9626b54de7439af20cdd76c2bc18
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/15/2018
ms.locfileid: "51667397"
---
# <a name="creating-cdata-sections-using-sqluse-cdata-sqlxml-40"></a>使用 sql:use-cdata 建立 CDATA 區段 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  在 XML 中，CDATA 區段可用來逸出包含字元的文字區塊，否則這些字元會被辨識為標記字元。  
  
 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的資料庫有時可以包含由 XML 剖析器視為標記字元的字元；例如，角括弧 (< 和 >)、小於或等於符號 (<=) 及連字號 (&) 會被視為標記字元。 但是，您可以將這類型的特殊字元包裝在 CDATA 區段內，以免被視為標記字元。 XML 剖析器會將 CDATA 區段內的文字視為純文字。  
  
 **Sql: use-cdata-cdata**註解用來指定所傳回之資料[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]應該包裝在 CDATA 區段 (也就是它會指出資料行的值是否由指定**sql: field**應放在 CDATA 區段)。 **Sql: use-cdata-cdata**註解，請指定只在對應至資料庫資料行的項目上。  
  
 **Sql: use-cdata-cdata**註解接受布林值 (0 = false,1 = true)。 可接受的值為 0、1、true 和 false。  
  
 此註解不能搭配**sql: url-encode-編碼**或是在 ID、 IDREF、 IDREFS、 NMTOKEN 和 NMTOKENS 屬性類型。  
  
## <a name="examples"></a>範例  
 若要使用下列範例建立工作範例，您必須符合某些需求。 如需詳細資訊，請參閱 <<c0> [ 如需執行 SQLXML 範例的需求](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md)。  
  
### <a name="a-specifying-sqluse-cdata-on-an-element"></a>A. 在元素上指定 sql:use-cdata  
 在下列結構描述中， **sql: use-cdata-cdata**設為 1 (True)，如 **\<AddressLine1 >** 內**\<位址 >** 項目。 因此，資料會在 CDATA 區段內傳回。  
  
```  
<xsd:schema xmlns:xsd="https://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="Address"   
               sql:relation="Person.Address"   
               sql:key-fields="AddressID" >  
   <xsd:complexType>  
        <xsd:sequence>  
          <xsd:element name="AddressID"  type="xsd:string" />  
          <xsd:element name="AddressLine1" type="xsd:string"   
                       sql:use-cdata="1" />  
        </xsd:sequence>  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>針對結構描述測試範例 XPath 查詢  
  
1.  複製上述的結構描述程式碼，並將其貼到文字檔中。 將檔案儲存為 UseCData.xml。  
  
2.  複製下列範本，並將其貼到文字檔中。 將檔案儲存為 UseCDataT.xml 並放在與 UseCData.xml 相同的目錄中。  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
        <sql:xpath-query mapping-schema="UseCData.xml">  
            /Address[AddressID < 11]  
        </sql:xpath-query>  
    </ROOT>  
    ```  
  
     針對對應結構描述 (UseCData.xml) 指定的目錄路徑，相對於儲存範本的目錄。 您也可以指定絕對路徑，例如：  
  
    ```  
    mapping-schema="C:\SqlXmlTest\UseCData.xml"  
    ```  
  
3.  建立和使用 SQLXML 4.0 測試指令碼 (Sqlxml4test.vbs) 以執行範本。  
  
     如需詳細資訊，請參閱 <<c0> [ 使用 ADO 執行 SQLXML 4.0 查詢](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
 這是部分結果集：  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">   
  <Address>   
    <AddressID>1</CustomerID>   
    <AddressLine1>   
      <![CDATA[ 1970 Napa Ct.  ]]>   
    </AddressLine1>   
  </Address>  
  <Address>  
    <AddressLine1>   
      <![CDATA[ 9833 Mt. Dias Blv. ]]>   
    </AddressLine1>   
  </Address>  
  ...  
</ROOT>  
```  
  
  
