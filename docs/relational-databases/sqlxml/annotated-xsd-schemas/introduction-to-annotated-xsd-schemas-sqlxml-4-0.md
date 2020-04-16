---
title: 註解 XSD 架構 (SQLXML) 簡介
description: 瞭解如何使用 XML 架構定義 (XSD) 語言 (SQLXML 4.0) 創建關係數據的 XML 檢視。
ms.date: 01/11/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
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
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c165ca271c3230399d54363f22d2b220e5427830
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/15/2020
ms.locfileid: "81388650"
---
# <a name="introduction-to-annotated-xsd-schemas-sqlxml-40"></a>註解式 XSD 結構描述簡介 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  您可以使用 XML 結構描述定義 (XSD) 語言來建立關聯式資料的 XML 檢視。 接著，您就可以使用 XML 路徑語言 (XPath) 查詢來查詢這些檢視。 這類似於使用 CREATE VIEW 陳述式來建立檢視，然後針對檢視指定 SQL 查詢。  
  
 XML 結構描述會描述 XML 文件的結構，而且也會描述文件中資料的各種條件約束。 針對結構描述指定 XPath 查詢時，傳回之 XML 文件的結構取決於執行 XPath 查詢所針對的結構描述。  
  
 在 XSD 架構中**\<,xsd:架構>** 元素包含整個架構;所有元素聲明必須包含在**\<xsd:schema>** 元素中。 可以描述定義架構所在的命名空間的屬性以及架構中用作**\<xsd:schema>** 元素屬性的命名空間。  
  
 有效的 XSD 架構必須包含**\<xsd:schema>** 元素定義如下:  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<!-- additional schema definitions here -->  
</xsd:schema>  
```  
  
 xsd:schema>元素派生自http://www.w3.org/2001/XMLSchema中的 XML 架構命名**\<** 空間規範。  
  
## <a name="annotations-to-the-xsd-schema"></a>XSD 結構描述的註解  
 您可以使用 XSD 結構描述搭配描述資料庫對應的註解、查詢資料庫，並且以 XML 文件的格式傳回結果。 提供註解的目的是要將 XSD 結構描述對應至資料庫資料表和資料行。 您可以針對 XSD 結構描述所建立的 XML 檢視指定 XPath 查詢來查詢資料庫，並以 XML 的格式取得結果。  
  
> [!NOTE]  
>  在 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML 4.0 中，XSD 結構描述語言支援 [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] 中註解式 XML-Data Reduced (XDR) 結構描述語言所導入的註解。 註解式 XDR 在 SQLXML 4.0 中已被取代。  
  
 在關聯式資料庫的內容中，將任意的 XSD 結構描述對應到關聯式存放區相當實用。 封存的其中一種方式是為 XSD 結構描述註解。 帶有註釋的 XSD 架構稱為*映射架構*,它提供有關如何將 XML 數據映射到關係儲存的資訊。 實際上，對應結構描述就是關聯式資料的 XML 檢視。 這些對應可用於擷取關聯式資料做為 XML 文件。  
  
## <a name="namespace-for-annotations"></a>註解的命名空間  
 在 XSD 架構中,註釋通過使用命名空間**urn:架構-microsoft-com:映射架構**來指定。 如以下範例所示,指定命名空間的最簡單方法是在**\<xsd:schema>** 標記中指定命名空間。  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
...  
</xsd:schema>  
```  
  
 所使用的命名空間前置詞是任意的。 在本文件中 **,sql**首碼用於表示註釋命名空間,並區分此命名空間中的註釋與其他命名空間中的註釋。  
  
## <a name="example-of-an-annotated-xsd-schema"></a>註解式 XSD 結構描述的範例  
 在下面的示例中,XSD 架構由**\<Person.Contact.>** 元素組成。 使用者>元素具有**ContactID**屬性與**\<Name name>** 和**\<姓氏>** 子元素: ** \<**  
  
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
  
 在映射架構中,**\<使用** **sql:關係**註釋將連絡人>元素映射到範例 AdventureWorks 資料庫中的 Person.連絡人表。 屬性 ConID、FName 和 LName 透過**使用 sql:欄位**註釋映射到「連絡人」中的聯絡人 ID、Name 和姓氏列。  
  
 此註解式 XSD 結構描述會提供關聯式資料的 XML 檢視。 您可以使用 XPath 語言來查詢這個 XML 檢視。 XPath 查詢會傳回 XML 文件當做結果，而不是 SQL 查詢所傳回的資料列集。  
  
> [!NOTE]  
>  在對應結構描述中，指定的關聯式值 (例如，資料表名稱和資料行名稱) 是否區分大小寫會取決於 SQL Server 是否使用區分大小寫的定序設定。 如需詳細資訊，請參閱 [Collation and Unicode Support](../../../relational-databases/collations/collation-and-unicode-support.md)。  
  
## <a name="other-resources"></a>其他資源  
 您可以在下列網站上找到有關 XML 結構描述定義語言 (XSD)、XML 路徑語言 (XPath) 和可延伸樣式表語言轉換 (XSLT) 的資訊：  
  
-   XML 架構第 0 部分:引瑟、W3C 建議 (https://www.w3.org/TR/xmlschema-0/)  
  
-   XML 架構第 1 部分:結構,W3C 建議(https://www.w3.org/TR/xmlschema-1/)  
  
-   XML 架構第 2 部分:資料類型,W3C 建議( W3C) 建議( W3C) 建議(https://www.w3.org/TR/xmlschema-2/)  
  
-   XML 路徑語言 (XPath) (https://www.w3.org/TR/xpath)  
  
-   XSL 轉換 (XSLT) (https://www.w3.org/TR/xslt)  
  
## <a name="see-also"></a>另請參閱  
 [&#40;SQLXML 4.0&#41;注释的架构安全注意事项](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/annotated-schema-security-considerations-sqlxml-4-0.md)   
 [在 SQLXML 4.0&#41;中&#40;棄用註解的 XDR 架構](../../../relational-databases/sqlxml/annotated-xsd-schemas/annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md)  
  
  
