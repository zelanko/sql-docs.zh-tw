---
title: 批註式 XSD 架構簡介（SQLXML 4.0） |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- namespaces [SQLXML], annotated XSD schemas
- mapping schema [SQLXML], about mapping schema
- views [SQLXML]
- valid XSD schemas [SQLXML]
- annotations [SQLXML]
- XSD schemas [SQLXML], creating XML views
- annotated XSD schemas, creating XML views
- minimum XSD schema
- annotated XSD schemas, examples
- XML views [SQLXML]
ms.assetid: 15282db1-65c4-43be-bdb7-e9ef49cb33a2
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 8b00f2a5f7d6bf9b0ac127b5df736d4a40c94219
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/01/2020
ms.locfileid: "82702931"
---
# <a name="introduction-to-annotated-xsd-schemas-sqlxml-40"></a>註解式 XSD 結構描述簡介 (SQLXML 4.0)
  您可以使用 XML 結構描述定義 (XSD) 語言來建立關聯式資料的 XML 檢視。 接著，您就可以使用 XML 路徑語言 (XPath) 查詢來查詢這些檢視。 這類似於使用 CREATE VIEW 陳述式來建立檢視，然後針對檢視指定 SQL 查詢。  
  
 XML 結構描述會描述 XML 文件的結構，而且也會描述文件中資料的各種條件約束。 針對結構描述指定 XPath 查詢時，傳回之 XML 文件的結構取決於執行 XPath 查詢所針對的結構描述。  
  
 在 XSD 架構中， ** \< xsd： schema>** 元素會括住整個架構; 所有元素宣告都必須包含在** \< XSD： schema>** 元素中。 您可以描述定義架構所在之命名空間的屬性，以及用於架構中的命名空間，做為** \< xsd： schema>** 元素的屬性。  
  
 有效的 XSD 架構必須包含定義如下的** \< xsd： schema>** 元素：  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<!-- additional schema definitions here -->  
</xsd:schema>  
```  
  
 ** \< Xsd： schema>** 元素衍生自的 XML 架構命名空間規格 http://www.w3.org/2001/XMLSchema 。  
  
## <a name="annotations-to-the-xsd-schema"></a>XSD 結構描述的註解  
 您可以使用 XSD 結構描述搭配描述資料庫對應的註解、查詢資料庫，並且以 XML 文件的格式傳回結果。 提供註解的目的是要將 XSD 結構描述對應至資料庫資料表和資料行。 您可以針對 XSD 結構描述所建立的 XML 檢視指定 XPath 查詢來查詢資料庫，並以 XML 的格式取得結果。  
  
> [!NOTE]  
>  在 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML 4.0 中，XSD 結構描述語言支援 [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] 中註解式 XML-Data Reduced (XDR) 結構描述語言所導入的註解。 註解式 XDR 在 SQLXML 4.0 中已被取代。  
  
 在關聯式資料庫的內容中，將任意的 XSD 結構描述對應到關聯式存放區相當實用。 封存的其中一種方式是為 XSD 結構描述註解。 具有批註的 XSD 架構稱為*對應架構*，它會提供有關如何將 XML 資料對應到關聯式存放區的資訊。 實際上，對應結構描述就是關聯式資料的 XML 檢視。 這些對應可用於擷取關聯式資料做為 XML 文件。  
  
## <a name="namespace-for-annotations"></a>註解的命名空間  
 在 XSD 架構中，批註是使用命名空間**urn：架構-microsoft-com：對應架構**來指定。 如下列範例所示，指定命名空間最簡單的方式，就是在** \< xsd： schema>** 標記中指定它。  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
...  
</xsd:schema>  
```  
  
 所使用的命名空間前置詞是任意的。 在此檔中，會使用**sql**前置詞來表示批註命名空間，並區別此命名空間與其他命名空間中的批註。  
  
## <a name="example-of-an-annotated-xsd-schema"></a>註解式 XSD 結構描述的範例  
 在下列範例中，XSD 架構是由** \< Person. Contact>** 元素所組成。 ** \< Employee>** 元素具有**ContactID**屬性，而** \< FirstName>** 和** \< LastName>** 子項目：  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema">  
  <xsd:element name="Contact" >  
   <xsd:complexType>  
     <xsd:sequence>  
        <xsd:element name="FName"    
                     type="xsd:string" />   
        <xsd:element name="LName"  
                     type="xsd:string" />  
     </xsd:sequence>  
        <xsd:attribute name="ConID" type="xsd:integer" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 然後，將註解加入至這個 XSD 結構描述，以便將其元素和屬性對應至資料庫資料表和資料行：  
  
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
        <xsd:attribute name="ConID"   
                       sql:field="ContactID"   
                       type="xsd:integer" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 在對應架構中， ** \< Contact>** 元素會使用批註對應至範例 AdventureWorks 資料庫中的 Person 資料表。 `sql:relation` ConID、FName 和 LName 屬性會使用 `sql:field` 註解來對應至 Person.Contact 資料表中的 ContactID、FirstName 和 LastName 資料行。  
  
 此註解式 XSD 結構描述會提供關聯式資料的 XML 檢視。 您可以使用 XPath 語言來查詢這個 XML 檢視。 XPath 查詢會傳回 XML 文件當做結果，而不是 SQL 查詢所傳回的資料列集。  
  
> [!NOTE]  
>  在對應結構描述中，指定的關聯式值 (例如，資料表名稱和資料行名稱) 是否區分大小寫會取決於 SQL Server 是否使用區分大小寫的定序設定。 如需詳細資訊，請參閱 [Collation and Unicode Support](../../collations/collation-and-unicode-support.md)。  
  
## <a name="other-resources"></a>其他資源  
 您可以在下列網站上找到有關 XML 結構描述定義語言 (XSD)、XML 路徑語言 (XPath) 和可延伸樣式表語言轉換 (XSLT) 的資訊：  
  
-   XML 架構第0部分：入門、W3C 建議（http://www.w3.org/TR/xmlschema-0/)  
  
-   XML 架構第1部分：結構、W3C 建議（http://www.w3.org/TR/xmlschema-1/)  
  
-   XML 架構第2部分：資料類型、W3C 建議（http://www.w3.org/TR/xmlschema-2/)  
  
-   XML 路徑語言（XPath）（http://www.w3.org/TR/xpath)  
  
-   XSL 轉換（XSLT）（http://www.w3.org/TR/xslt)  
  
## <a name="see-also"></a>另請參閱  
 [&#40;SQLXML 4.0&#41;的批註式架構安全性考慮](../../sqlxml-annotated-xsd-schemas-xpath-queries/security/annotated-schema-security-considerations-sqlxml-4-0.md)   
 [批註式 XDR 架構 &#40;在 SQLXML 4.0 中被取代&#41;](annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md)  
  
  
