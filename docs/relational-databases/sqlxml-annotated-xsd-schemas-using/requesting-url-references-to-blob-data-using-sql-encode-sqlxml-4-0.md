---
title: 使用 sql:編碼 (SQLXML) 取得對 BLOB 資料的網址參考
description: 瞭解如何透過在 SQLXML 4.0 中指定 sql:編碼註釋來請求對 BLOB 資料的 URL 引用。
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
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
author: MightyPen
ms.author: genemi
ms.reviewer: ''
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 487ed2bbee997db22739bdeecd7e024b817ace80
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/15/2020
ms.locfileid: "81388112"
---
# <a name="requesting-url-references-to-blob-data-using-sqlencode-sqlxml-40"></a>使用 sql:encode 要求指向 BLOB 資料的 URL 參考 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  在註解式 XSD 結構描述中，當屬性 (或元素) 對應到 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的 BLOB 資料行時，將會以 XML 中的 Base 64 編碼格式傳回資料。  
  
 如果要返回對資料 (URI) 的引用,以便以後用於以二進位格式檢索 BLOB 資料,請指定**sql:encode**註解。 您可以在簡單類型的屬性或元素上指定**sql:編碼**。  
  
 指定**sql:編碼**註解以指示應返回欄位的 URL 而不是欄位的值。 **sql:編碼**取決於主鍵來生成 URL 中的單例選擇。 可以使用**sql:鍵欄位**註釋指定主鍵。  
  
 可以配置**sql:編碼**註釋的"url"或"預設" "default" 值會傳回 Base 64 編碼格式的資料。  
  
 **sql:編碼**註釋不能與**sql:使用-cdata**或 ID、IDREF、IDREFS、NMTOKEN 或 NMTOKENS 屬性類型一起使用。 它也不能與 XSD**固定**屬性一起使用。  
  
> [!NOTE]  
>  BLOB 類型的資料行不能當做索引鍵或外部索引鍵的一部分使用。  
  
## <a name="examples"></a>範例  
 若要使用下列範例建立工作範例，您必須符合某些需求。 有關詳細資訊,請參閱執行[SQLXML 範例的要求](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md)。  
  
### <a name="a-specifying-sqlencode-to-obtain-a-url-reference-to-blob-data"></a>A. 指定 sql:encode 來取得指向 BLOB 資料的 URL 參考  
 在此示例中,映射架構在**LargePhoto**屬性上指定**sql:encode,** 以檢索對特定產品照片的 URI 引用(而不是以基 64 編碼格式檢索二進位數據)。  
  
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
  
     有關詳細資訊,請參閱使用[ADO 執行 SQLXML 4.0 查詢](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
 以下是結果：  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
   <ProductPhoto ProductPhotoID="100"  
                 LargePhoto="dbobject/Production.ProductPhoto[@ProductPhotoID="100"]/@LargePhoto" />   
</ROOT>  
```  
  
  
