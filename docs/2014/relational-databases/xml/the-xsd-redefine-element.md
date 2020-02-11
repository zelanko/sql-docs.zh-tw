---
title: '&lt;xsd:redefine&gt; 項目 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- xsd:redefine element
ms.assetid: 5f3e9b65-f10e-4db2-a62c-b270ac11d04e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7e9fa3dedafc05406dcc521429130f98a215d294
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62679968"
---
# <a name="the-ltxsdredefinegt-element"></a>&lt;xsd:redefine&gt; 項目
  W3C XSD **redefine** 元素支援重新定義結構描述的元件。 不過，對此指示詞的支援可能會耗用很高的效能[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，而且也需要重新`xml`驗證與重新定義的架構相關聯之資料類型的所有實例。 因此， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不支援此元素。 伺服器將會拒絕包含 **\<xsd:redefine>** 項目的 XML 結構描述。  
  
 若要更新結構描述或是其元件，您可以改為執行下列動作：  
  
1.  使用修改過的結構描述元件建立新的 XML 結構描述集合。  
  
2.  重新輸入可使用要重新定義之 XML 結構描述集合的所有 `xml` 資料類型 (XML DT)，以改用新的 XML 結構描述集合。 若要這樣做，請使用 ALTER TABLE 命令的 ALTER COLUMN 選項來重新輸入資料行，或是變更變數或參數上的 XML 結構描述集合條件約束。  
  
3.  捨棄舊版的 XML 結構描述集合。  
  
## <a name="see-also"></a>另請參閱  
 [伺服器上 XML 結構描述集合的需求與限制](requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
