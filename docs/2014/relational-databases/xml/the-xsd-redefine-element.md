---
title: '&lt;xsd:redefine&gt; 項目 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- xsd:redefine element
ms.assetid: 5f3e9b65-f10e-4db2-a62c-b270ac11d04e
caps.latest.revision: 13
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 4ca94410d7011c30de0a5481451337d11fa57120
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36147104"
---
# <a name="the-ltxsdredefinegt-element"></a>&lt;xsd:redefine&gt; 項目
  W3C XSD **redefine** 元素支援重新定義結構描述的元件。 不過，支援此指示詞可能會使效能，也需要[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]重新驗證的所有執行個體`xml`與重新定義結構描述相關聯的資料類型。 因此， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不支援此元素。 伺服器將會拒絕包含 **\<xsd:redefine>** 項目的 XML 結構描述。  
  
 若要更新結構描述或是其元件，您可以改為執行下列動作：  
  
1.  使用修改過的結構描述元件建立新的 XML 結構描述集合。  
  
2.  重新輸入可使用要重新定義之 XML 結構描述集合的所有 `xml` 資料類型 (XML DT)，以改用新的 XML 結構描述集合。 若要這樣做，請使用 ALTER TABLE 命令的 ALTER COLUMN 選項來重新輸入資料行，或是變更變數或參數上的 XML 結構描述集合條件約束。  
  
3.  捨棄舊版的 XML 結構描述集合。  
  
## <a name="see-also"></a>另請參閱  
 [伺服器上 XML 結構描述集合的需求與限制](requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  