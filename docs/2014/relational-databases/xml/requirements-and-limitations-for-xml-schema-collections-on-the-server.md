---
title: 伺服器上 XML 結構描述集合的需求與限制 | Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- identifiers [XML schema collections]
- XML schema collections [SQL Server], limitations
- substitution groups [XML in SQL Server]
- XML schema collections [SQL Server], guidelines
- lax validation
- enumeration facets [XML in SQL Server]
- decimal precision [XML in SQL Server]
- repeated XML schema collection values
- schema collections [SQL Server], limitations
- time zones [XML in SQL Server]
- precision decimals [XML in SQL Server]
- schema collections [SQL Server], guidelines
- lexical representation
ms.assetid: c2314fd5-4c6d-40cb-a128-07e532b40946
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 245b844872070ee16104a90ecc0734462bdad3b5
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "63241254"
---
# <a name="requirements-and-limitations-for-xml-schema-collections-on-the-server"></a>伺服器上 XML 結構描述集合的需求與限制
  XML 結構描述定義語言 (XSD) 驗證對於使用 `xml` 資料類型的 SQL 資料行具有某些相關限制。 下表提供這些限制的詳細資料以及修改 XSD 結構描述以便讓它可以搭配 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用的指導方針。 本章節的主題提供有關特定限制的其他資訊，以及處理這些限制的指導方針。  
  
|Item|限制|  
|----------|----------------|  
|**minOccurs** 與 **maxOccurs**|**minOccurs** 與 **maxOccurs** 屬性值必須符合 4 位元組的整數。 伺服器將會拒絕不符合的結構描述。|  
|**\<xsd:choice>**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會拒絕沒有子系的 **\<xsd:choice>** 物件之結構描述，除非以零的 **minOccurs** 屬性值定義該物件。|  
|**\<xsd:include>**|目前， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不支援這個元素。 伺服器將會拒絕包含此元素的 XML 結構描述。<br /><br /> 若要解決此問題，您可以預先處理包含 **\<xsd:include>** 指示詞的 XML 結構描述，將任何所包含的結構描述內容複製並合併成單一結構描述，以便上傳至伺服器。 如需詳細資訊，請參閱 [前置處理結構描述以合併包含的結構描述](preprocess-a-schema-to-merge-included-schemas.md)。|  
|**\<xsd:key>** 、 **\<xsd:keyref>** 和 **\<xsd:unique>**|目前， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不支援這些以 XSD 為基礎的條件約束，以強制執行唯一性或建立索引鍵及索引鍵參考。 無法註冊包含這些元素的 XML 結構描述。|  
|**\<xsd:redefine>**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不支援這個元素。 如需更新結構描述之其他做法的資訊，請參閱 [&#60;xsd:redefine&#62; 元素](the-xsd-redefine-element.md)使用的指導方針。|  
|**\<xsd:simpleType>** 值|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 只支援具有 `xs:time` 和 `xs:dateTime` 以外之第二個元件的簡單類型毫秒有效位數，以及 `xs:time` 和 `xs:dateTime` 100 奈秒的有效位數。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會對所有可辨識的 XSD 簡單類型列舉做出限制。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不支援在 **\<xsd:simpleType>** 宣告中使用 "NaN" 值。<br /><br /> 如需詳細資訊，請參閱[&#60;xsd:simpleType&#62; 宣告的值](values-for-xsd-simpletype-declarations.md)使用的指導方針。|  
|**xsi:schemaLocation** 與 **xsi:noNamespaceSchemaLocation**|如果這些屬性出現在插入 `xml` 資料類型之資料行或變數的 XML 執行個體資料中，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 將會忽略這些屬性。|  
|**xs:QName**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不支援使用 XML 結構描述限制元素且從 **xs:QName** 衍生的類型。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不支援 **xs:QName** 為成員元素的聯集類型。<br /><br /> 如需詳細資訊，請參閱 [xs:QName 類型](the-xs-qname-type.md)。|  
|將成員加入現有替代群組|您無法在 XML 結構描述集合中將成員加入現有的替代群組。 在 XML 結構描述中的替代群組是限制成標頭元素，而且所有其成員元素都必須定義在相同的 {CREATE &#124; ALTER} XML SCHEMA COLLECTION 陳述式中。|  
|標準格式與模式限制|值的標準表示法不能違反其類型的模式限制。 如需詳細資訊，請參閱 [標準格式與模式限制](canonical-forms-and-pattern-restrictions.md)。|  
|列舉 Facet|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不支援類型含有模式 Facet 或列舉違反這些 Facet 的 XML 結構描述。|  
|Facet 長度|**Length**、 **minLength**和**maxLength** facet 會儲存為`long`類型。 此類型是 32 位元的類型。 因此，這些值的可接受值範圍為 2<sup>^</sup>31。|  
|ID 屬性|每個 XML 結構描述元件都可擁有識別碼屬性。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會針對 **ID\< 類型的** **xsd:attribute>** 宣告強制唯一性，但不會儲存這些值。 唯一性的強制範圍是 {CREATE &#124; ALTER} XML SCHEMA COLLECTION 陳述式。|  
|ID 類型|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不支援 **xs:ID**、 **xs:IDREF**或 **xs:IDREFS**類型的元素。 結構描述不能宣告此類型的元素，或者宣告由限制此類型或從此類型衍生的元素。|  
|區域命名空間|您必須為 **\<xsd:any>** 項目明確指定本機命名空間。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會拒絕使用空字串 ("") 作為命名空間屬性值的結構描述。 不過， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會要求明確使用 "##local"，將不完整的元素或屬性指示成萬用字元的執行個體。|  
|混合的類型與簡單的內容|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不支援將混合類型限制為簡單內容。 如需詳細資訊，請參閱 [混合的類型與簡單的內容](mixed-type-and-simple-content.md)。|  
|NOTATION 類型|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不支援 NOTATION 類型。|  
|記憶體不足的情況|在處理大型的 XML 結構描述集合時，有可能發生記憶體不足的情況。 如需這個問題的解決方案，請參閱 [大型的 XML 結構描述集合與記憶體不足的情況](large-xml-schema-collections-and-out-of-memory-conditions.md)。|  
|重複值|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會拒絕 block 或 final 屬性有重複值的結構描述，例如 "restriction restriction" 與 "extension extension"。|  
|結構描述元件識別碼|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會將結構描述元件識別碼的最大長度限制為 1000 個 Unicode 字元。 另外，不支援在識別碼中的 Surrogate 字元組。|  
|時區資訊|在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 和更新版本中進行 XML 結構描述驗證時，`xs:date`、`xs:time` 和 `xs:dateTime` 值可完全支援時區資訊。 在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 回溯相容性模式下，時區資訊一定會正規化為國際標準時間 (格林威治標準時間)。 若為 `dateTime` 類型的元素，伺服器就會使用位移值 ("-05:00") 和傳回對應的 GMT 時間，藉以將提供的時間轉換為 GMT。|  
|聯集類型|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不支援聯集類型的限制。|  
|可變的有效位數小數|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不支援可變的有效位數小數。 **xs:decimal** 類型表示任意有效位數的小數位數。 符合 XML 處理器的最低限度必須支援最少為 `totalDigits=18`的十進位數字。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援 `totalDigits=38,` ，但是會將小數點後數字限制為 10。 伺服器對於所有的 **xs:decimal** 執行個體值在內部都是使用 SQL 類型數值 (38, 10) 來表示。|  
  
## <a name="in-this-section"></a>本節內容  
  
|主題|描述|  
|-----------|-----------------|  
|[標準格式與模式限制](canonical-forms-and-pattern-restrictions.md)|說明標準格式與模式限制。|  
|[萬用字元元件和內容驗證](wildcard-components-and-content-validation.md)|描述搭配 XML 結構描述集合使用萬用字元、Lax 驗證和 anyType 元素的限制。|  
|[&#60;xsd:redefine&#62; 元素](the-xsd-redefine-element.md)|說明使用 \<xsd:redefine> 項目的限制及描述因應措施。|  
|[xs:QName 類型](the-xs-qname-type.md)|描述有關 xs:QName 類型的限制。|  
|[&#60;xsd:simpleType&#62; 宣告的值](values-for-xsd-simpletype-declarations.md)|描述適用於 \<xsd:simpleType> 宣告的限制。|  
|[列舉 Facet](enumeration-facets.md)|描述有關列舉 Facet 的限制。|  
|[混合的類型與簡單的內容](mixed-type-and-simple-content.md)|描述將混合類型限制為簡單內容的限制。|  
|[大型的 XML 結構描述集合與記憶體不足的情況](large-xml-schema-collections-and-out-of-memory-conditions.md)|提供有時在處理大型結構描述集合時，可能發生之記憶體不足狀況的解決方案。|  
|[不具決定性的內容模型](non-deterministic-content-models.md)|描述有關不具決定性之內容模型的限制。|  
  
## <a name="see-also"></a>另請參閱  
 [XML 資料 &#40;SQL Server&#41;](xml-data-sql-server.md)   
 [比較具類型的 XML 與不具類型的 XML](compare-typed-xml-to-untyped-xml.md)   
 [授與 XML 結構描述集合的權限](grant-permissions-on-an-xml-schema-collection.md)   
 [唯一物件屬性條件約束](unique-particle-attribution-constraint.md)   
 [XML 結構描述集合 &#40;SQL Server&#41;](xml-schema-collections-sql-server.md)  
  
  
