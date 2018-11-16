---
title: 要求的 URL 參考 BLOB 資料使用 sql： 編碼 (SQLXML 4.0) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- sql:encode
- encode annotation
- URL references to BLOB data [SQLXML]
- references to BLOB data [SQLXML]
- annotated XSD schemas, URL references to BLOB data
- requesting URL references to BLOB data
- BLOBs, URL references
- Base 64-encoded format
ms.assetid: 2f8cd93b-c636-462b-8291-167197233ee0
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a2893ff05a82ae647fa3194c2d1c7427827939c5
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/15/2018
ms.locfileid: "51661737"
---
# <a name="requesting-url-references-to-blob-data-using-sqlencode-sqlxml-40"></a>使用 sql:encode 要求指向 BLOB 資料的 URL 參考 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  在註解式 XSD 結構描述中，當屬性 (或元素) 對應到 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的 BLOB 資料行時，將會以 XML 中的 Base 64 編碼格式傳回資料。  
  
 如果您想要資料的參考 (URI) 要傳回可稍後再擷取 BLOB 資料以二進位格式，指定**sql： 編碼**註釋。 您可以指定**sql： 編碼**上的屬性或簡單類型的元素。  
  
 指定**sql： 編碼**註解可指示應該傳回欄位的 URL，而不是欄位的值。 **sql： 編碼**取決於 URL 中產生的單一選取的主索引鍵。 您可以使用指定的主索引鍵**sql: key-fields 來-欄位**註釋。  
  
 **Sql： 編碼**可以指派註解，"url"或"default"值。 "default" 值會傳回 Base 64 編碼格式的資料。  
  
 **Sql： 編碼**註釋不能搭配**sql: use-cdata-cdata**或是在 ID、 IDREF、 IDREFS、 NMTOKEN 或 NMTOKENS 屬性類型。 它也不能搭配 XSD**修正**屬性。  
  
> [!NOTE]  
>  BLOB 類型的資料行不能當做索引鍵或外部索引鍵的一部分使用。  
  
## <a name="examples"></a>範例  
 若要使用下列範例建立工作範例，您必須符合某些需求。 如需詳細資訊，請參閱 <<c0> [ 如需執行 SQLXML 範例的需求](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md)。  
  
### <a name="a-specifying-sqlencode-to-obtain-a-url-reference-to-blob-data"></a>A. 指定 sql:encode 來取得指向 BLOB 資料的 URL 參考  
 在此範例中，指定對應結構描述**sql： 編碼**上**LargePhoto**擷取 （而不是擷取二進位的資料在 Base 64-特定產品相片的 URI 參考的屬性編碼格式）。  
  
```  
<xsd:schema xmlns:xsd="https://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  
  <xsd:element name="ProductPhoto" sql:relation="Production.ProductPhoto"   
               sql:key-fields="ProductPhotoID" >  
   <xsd:complexType>  
      <xsd:attribute name="ProductPhotoID"  type="xsd:int"  />  
     <xsd:attribute name="LargePhoto" type="xsd:string" sql:encode="url" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>針對結構描述測試範例 XPath 查詢  
  
1.  複製上述的結構描述程式碼，並將其貼到文字檔中。 將檔案儲存為 sqlEncode.xml。  
  
2.  複製下列範本，並將其貼到文字檔中。 將檔案儲存在與 sqlEncode.xml 相同的目錄中，並儲存為 sqlEncodeT.xml。  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
        <sql:xpath-query mapping-schema="sqlEncode.xml">  
            /ProductPhoto[@ProductPhotoID=100]  
        </sql:xpath-query>  
    </ROOT>  
    ```  
  
     針對對應結構描述 (sqlEncode.xml) 指定的目錄路徑相對於儲存範本的目錄。 您也可以指定絕對路徑，例如：  
  
    ```  
    mapping-schema="C:\SqlXmlTest\sqlEncode.xml"  
    ```  
  
3.  建立和使用 SQLXML 4.0 測試指令碼 (Sqlxml4test.vbs) 以執行範本。  
  
     如需詳細資訊，請參閱 <<c0> [ 使用 ADO 執行 SQLXML 4.0 查詢](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
 以下是結果：  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
   <ProductPhoto ProductPhotoID="100"  
                 LargePhoto="dbobject/Production.ProductPhoto[@ProductPhotoID="100"]/@LargePhoto" />   
</ROOT>  
```  
  
  
