---
title: 萬用字元元件和內容驗證 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- wildcard components [XML]
- content validation [XML]
ms.assetid: ffa7d974-3645-446c-8425-f0b22b6b060a
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 7977b2590d833f87cc7703d8424f1aacaac54546
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37189955"
---
# <a name="wildcard-components-and-content-validation"></a>萬用字元元件和內容驗證
  萬用字元元件可用以增加可出現在內容模型中的內容彈性。 在 XSD 語言中，可透過下列方式支援這些元件：  
  
-   元素萬用字元元件。 這些是以 **\<xsd:any>** 項目表示。  
  
-   屬性萬用字元元件。 這些是以 **\<xsd:anyAttribute>** 項目表示。  
  
 **\<xsd:any>** 和 **\<xsd:anyAttribute>** 這兩個萬用字元項目都支援使用 **processContents** 屬性。 這可讓您指定一個值，以指出 XML 應用程式如何處理與這些萬用字元元素關聯的文件內容驗證。 以下是不同的值所產生的效果：  
  
-   **strict** 值指定完整驗證內容。  
  
-   **skip** 值指定不驗證內容。  
  
-   **lax** 值指定只會驗證可以使用結構描述定義的元素與屬性。  
  
## <a name="lax-validation-and-xsanytype-elements"></a>Lax 驗證和 xs:anyType 元素  
 XML 結構描述規格會針對 **anyType** 類型的元素使用 **lax** 驗證。 因為 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 不支援 Lax 驗證，因此會對 **anyType**的元素套用 Strict 驗證。 從 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]開始，Lax 驗證就有受到支援。 **anyType** 類型的元素內容將會使用 Lax 驗證加以驗證。  
  
 下列範例說明 Lax 驗證。 `e` 結構描述元素的類型為 **anyType** 。 此範例會建立具類型的 **xml** 變數，並說明 **anyType** 類型元素的 Lax 驗證。  
  
```  
CREATE XML SCHEMA COLLECTION SC AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema"   
        targetNamespace="http://ns">  
   <element name="e" type="anyType"/>  
   <element name="a" type="byte"/>  
   <element name="b" type="string"/>  
 </schema>'  
GO  
```  
  
 下列範例會成功，因為 `<e>` 的驗證是成功的：  
  
```  
DECLARE @var XML(SC)  
SET @var = '<e xmlns="http://ns"><a>1</a><b>data</b></e>'  
GO  
```  
  
 下列範例將會成功。 即使此結構描述中未定義任何 `<c>` 元素，還是可接受此結構描述：  
  
```  
DECLARE @var XML(SC)  
SET @var = '<e xmlns="http://ns"><a>1</a><c>Wrong</c><b>data</b></e>'  
GO  
```  
  
 下列範例中的 XML 執行個體會遭到拒絕，因為 `<a>` 元素的定義不允許字串值。  
  
```  
DECLARE @var XML(SC)  
SET @var = '<e xmlns="http://ns"><a>Wrong</a><b>data</b></e>'  
SELECT @var  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [伺服器上 XML 結構描述集合的需求與限制](requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
