---
title: '&lt;xsd:redefine&gt; 項目 | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- xsd:redefine element
ms.assetid: 5f3e9b65-f10e-4db2-a62c-b270ac11d04e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1b4a155e7f3c23508080a5fd55f15d05c5432c50
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68078118"
---
# <a name="the-ltxsdredefinegt-element"></a>&lt;xsd:redefine&gt; 項目
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  W3C XSD **redefine** 元素支援重新定義結構描述的元件。 不過，此指示詞的支援可能會使效能大幅降低，而且 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 也需要重新驗證所有  資料類型執行個體 (其已與重新定義的結構描述建立關聯)。 因此， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不支援此元素。 伺服器將會拒絕包含 **\<xsd:redefine>** 項目的 XML 結構描述。  
  
 若要更新結構描述或是其元件，您可以改為執行下列動作：  
  
1.  使用修改過的結構描述元件建立新的 XML 結構描述集合。  
  
2.  重新輸入使用要重新定義之 XML 結構描述集合的所有 **xml** 資料類型 (XML DT)，以改用新的 XML 結構描述集合。 若要這樣做，請使用 ALTER TABLE 命令的 ALTER COLUMN 選項來重新輸入資料行，或是變更變數或參數上的 XML 結構描述集合條件約束。  
  
3.  捨棄舊版的 XML 結構描述集合。  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

## <a name="see-also"></a>另請參閱  
 [伺服器上 XML 結構描述集合的需求與限制](../../relational-databases/xml/requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
