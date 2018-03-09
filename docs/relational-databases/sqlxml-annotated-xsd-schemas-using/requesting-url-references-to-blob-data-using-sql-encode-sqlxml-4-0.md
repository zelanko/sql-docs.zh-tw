---
title: "要求的 URL 參考 BLOB 資料使用 sql： 編碼 (SQLXML 4.0) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: sqlxml
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
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
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2f67c2f00aaed2d9a619de7a82565daa756976df
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/12/2018
---
# <a name="requesting-url-references-to-blob-data-using-sqlencode-sqlxml-40"></a>使用 sql:encode 要求指向 BLOB 資料的 URL 參考 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
在註解式 XSD 結構描述中，當屬性 (或元素) 對應到 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的 BLOB 資料行時，將會以 XML 中的 Base 64 編碼格式傳回資料。  
  
 如果您想要之資料的參考 (URI) 會傳回，可以稍後可用於擷取二進位格式的 BLOB 資料，請指定**sql： 編碼**註解。 您可以指定**sql： 編碼**的屬性或簡單類型的項目。  
  
 指定**sql： 編碼**註解可指示應該傳回欄位的 URL，而不是欄位的值。 **sql： 編碼**取決於 URL 中產生的單一選取的主索引鍵。 可以使用指定的主索引鍵**sql: key-fields-欄位**註解。  
  
 **Sql： 編碼**可以指派註釋，"url"或"default"值。 "default" 值會傳回 Base 64 編碼格式的資料。  
  
 **Sql： 編碼**註釋不能與**sql: use-cdata-cdata**或是在 ID、 IDREF、 IDREFS、 NMTOKEN 或 NMTOKENS 屬性類型。 它也不能搭配 XSD**固定**屬性。  
  
> [!NOTE]  
>  BLOB 類型的資料行不能當做索引鍵或外部索引鍵的一部分使用。  
  
## <a name="examples"></a>範例  
 若要使用下列範例建立工作範例，您必須符合某些需求。 如需詳細資訊，請參閱[執行 SQLXML 範例的需求](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md)。  
  
### <a name="a-specifying-sqlencode-to-obtain-a-url-reference-to-blob-data"></a>A. 指定 sql:encode 來取得指向 BLOB 資料的 URL 參考  
 在此範例中，指定對應結構描述**sql： 編碼**上**LargePhoto**来擷取 （而不是擷取二進位資料在基底 64-特定產品相片的 URI 參考屬性編碼格式）。  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
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
  
     如需詳細資訊，請參閱[ADO to Execute SQLXML 4.0](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
 以下是結果：  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
   <ProductPhoto ProductPhotoID="100"  
                 LargePhoto="dbobject/Production.ProductPhoto[@ProductPhotoID="100"]/@LargePhoto" />   
</ROOT>  
```  
  
  
