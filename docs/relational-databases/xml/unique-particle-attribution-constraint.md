---
title: "唯一物件屬性條件約束 | Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: xml
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- unique particle attribution
helpviewer_keywords:
- schema collections [SQL Server], unique particle attribution
- XML schema collections [SQL Server], unique particle attribution
- UPA constraint rule
- unique particle attribution constraint rule
ms.assetid: 6bb879e9-a5ee-402e-94e4-fe8cec5966b0
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0e19f33b48fda8ef1a476ff78fac176722b7af9d
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/12/2018
---
# <a name="unique-particle-attribution-constraint"></a>唯一物件屬性條件約束
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
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
  
 ＜XML 結構描述第一部份：結構第二版，W3C 提出的編輯建議＞(英文)：  
  
-   第 3.8.6 節：模型群組結構描述元件的條件約束 (Section 3.8.6: Constraints on Model Group Schema Components)  
  
-   附錄 H：唯一物件屬性條件約束的分析 (非標準的) (Appendix H: Analysis of the Unique Particle Attribution Constraint (non-normative))  
  
 若要參閱該文件，請前往 [http://www.w3.org/TR/xmlschema-1](http://go.microsoft.com/fwlink/?linkid=48881)。  
  
## <a name="see-also"></a>另請參閱  
 [XML 結構描述集合 &#40;SQL Server&#41;](../../relational-databases/xml/xml-schema-collections-sql-server.md)  
  
  
