---
title: "&lt;xsd:redefine&gt; 元素 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-xml"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "xsd:redefine 元素"
ms.assetid: 5f3e9b65-f10e-4db2-a62c-b270ac11d04e
caps.latest.revision: 14
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 14
---
# &lt;xsd:redefine&gt; 元素
  W3C XSD **redefine** 元素支援重新定義結構描述的元件。 不過，此指示詞的支援可能會使效能大幅降低，而且 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 也需要重新驗證所有  資料類型執行個體 (其已與重新定義的結構描述建立關聯)。 因此，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不支援此元素。 伺服器將會拒絕包含 **\<xsd:redefine>** 元素的 XML 結構描述。  
  
 若要更新結構描述或是其元件，您可以改為執行下列動作：  
  
1.  使用修改過的結構描述元件建立新的 XML 結構描述集合。  
  
2.  重新輸入使用要重新定義之 XML 結構描述集合的所有 **xml** 資料類型 (XML DT)，以改用新的 XML 結構描述集合。 若要這樣做，請使用 ALTER TABLE 命令的 ALTER COLUMN 選項來重新輸入資料行，或是變更變數或參數上的 XML 結構描述集合條件約束。  
  
3.  捨棄舊版的 XML 結構描述集合。  
  
## 另請參閱  
 [伺服器上 XML 結構描述集合的需求與限制](../../relational-databases/xml/requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  