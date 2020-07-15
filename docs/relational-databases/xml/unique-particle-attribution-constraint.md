---
title: 唯一物件屬性條件約束 | Microsoft 文件
description: 了解唯一物件屬性 (UPA) 條件約束規則如何拒絕 XSD 結構描述 (若其包含具有可能模稜兩可內容模式的類型)。
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
f1_keywords:
- unique particle attribution
helpviewer_keywords:
- schema collections [SQL Server], unique particle attribution
- XML schema collections [SQL Server], unique particle attribution
- UPA constraint rule
- unique particle attribution constraint rule
ms.assetid: 6bb879e9-a5ee-402e-94e4-fe8cec5966b0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9d7b6de76fdb5310a5121908779d4565a4b6ff1c
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85729831"
---
# <a name="unique-particle-attribution-constraint"></a>唯一物件屬性條件約束
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  在 XSD 中，會以唯一物件屬性 (UPA) 條件約束規則來限制複雜的內容模型。 此規則要求執行個體文件中的每個元素，都要明確地對應至其父系內容模型中的一個 `<xsd:element>` 或 `<xsd:any>` 物件。 若有任何結構描述，其包含的類型可能含有模稜兩可的內容模型，都會被拒絕。  
  
 導致內容模型模稜兩可的最常見原因，就是 `<xsd:any>` 萬用字元，以及具有變動出現範圍的物件，例如：minOccurs < maxOccurs。 例如，下列內容模型是模稜兩可的，因為 <`e1`> 元素可以符合 `<xsd:element>`，也可以符合 `<xsd:any>` 元素。  
  
```  
<xsd:element name="root">  
    <xsd:complexType>  
        <xsd:choice>  
            <xsd:element name="e1"/>  
            <xsd:any namespace="##any"/>  
        </xsd:choice>  
    </xsd:complexType>  
</xsd:element>  
```  
  
 下列內容模型也是不明確的：  
  
```  
<xsd:element name="root">  
    <xsd:complexType>  
        <xsd:sequence>  
            <xsd:element name="e1" maxOccurs="2"/>  
            <xsd:element name="e2" minOccurs="0"/>  
            <xsd:element name="e1"/>  
        </xsd:sequence>  
    </xsd:complexType>  
</xsd:element>  
```  
  
 雖然 `<root><e1/><e2/><e1/></root>` 這類文件可以明確地加以驗證，但是 `<root><e1/><e1/></root>` 這類文件沒有辦法，因為第二個 `<xsd:element>` 所對應的目標 `<e1/>` 並不清楚。 即使某些文件可以被明確地驗證，但是結構描述還是會被拒絕，因為它們潛藏著不明確性。  
  
 請注意，若要讓內容模型有效，需在不必往前查看的情況下，就能明確地驗證任何執行個體。 例如，請考量下列內容模型：  
  
```  
<xsd:element name="root">  
    <xsd:complexType>  
        <xsd:choice>  
           <xsd:sequence>  
               <xsd:element name="e1"/>  
               <xsd:element name="e2"/>  
           </xsd:sequence>  
           <xsd:sequence>  
               <xsd:element name="e1"/>  
               <xsd:element name="e3"/>  
           </xsd:sequence>  
       </xsd:choice>  
    </xsd:complexType>  
</xsd:element>  
```  
  
 像 `<root><e1/><e3/></root>`這類文件，序列 `<e1/><e3/>` 明確地符合第二個 `<xsd:sequence>`。 然而，因為 `<xsd:element>` 所對應的 `<e1/>` 在沒有往前查看 `<e3/>`的情況下，即無法做出判斷，所以內容模型違反了 UPA 條件約束規則。  
  
## <a name="finding-more-information"></a>尋找詳細資訊  
 下列文件是由全球資訊網協會 (W3C) 所發行，其中包含唯一物件屬性條件約束的技術說明：  
  
 "XML Schema Part 1:Structures Second Edition, W3C Proposed Edited Recommendation" (XML 結構描述第 1 部分：結構第二版，W3C 提出的編輯建議)：  
  
-   3\.8.6 節：Constraints on Model Group Schema Components (模型群組結構描述元件的條件約束)  
  
-   附錄 H：Analysis of the Unique Particle Attribution Constraint (non-normative) (唯一物件屬性條件約束的分析 (非標準))  
  
 若要查看文件，請瀏覽 [http://www.w3.org/TR/xmlschema-1](https://go.microsoft.com/fwlink/?linkid=48881)。  
  
## <a name="see-also"></a>另請參閱  
 [XML 結構描述集合 &#40;SQL Server&#41;](../../relational-databases/xml/xml-schema-collections-sql-server.md)  
  
  
