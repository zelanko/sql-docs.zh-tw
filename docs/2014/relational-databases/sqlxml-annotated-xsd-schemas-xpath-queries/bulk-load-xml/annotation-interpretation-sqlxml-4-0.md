---
title: 註解的解譯 (SQLXML 4.0) |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- annotated XSD schemas, XML Bulk Load
- XML Bulk Load [SQLXML], annotation intepretations
- annotations [SQLXML]
- bulk load [SQLXML], annotation interpretations
- annotated XDR schemas, XML Bulk Load
ms.assetid: 1c46bdb6-2812-4a13-b60b-7101c04b299f
caps.latest.revision: 22
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: ba4c9e6506b67802a8a9571df80ff4db7d2b3934
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36035173"
---
# <a name="annotation-interpretation-sqlxml-40"></a>註解的解譯 (SQLXML 4.0)
  本章節的主題描述 XML 大量載入要如何解譯 XSD 結構描述中的註解。 這裡所述的行為也適用於 XDR 結構描述中的註解。  
  
> [!NOTE]  
>  這些主題的資訊只會描述 XML 大量載入在處理時所使用的註解。 如需註解的 XSD 結構描述支援的 SQLXML 4.0 的完整清單，請參閱[使用 XSD 結構描述中的註解&#40;SQLXML 4.0&#41;](../../sqlxml-annotated-xsd-schemas-using/using-annotations-in-xsd-schemas-sqlxml-4-0.md)。 如需支援的註解的 XDR 結構描述的清單，請參閱[Annotated XDR Schemas &#40;SQLXML 4.0 中已被取代&#41;](../../sqlxml/annotated-xsd-schemas/annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md)。  
  
## <a name="in-this-section"></a>本節內容  
 [sql: relationship 和關鍵識別碼順序規則&#40;SQLXML 4.0&#41;](annotation-interpretation-sql-relationship-and-key-ordering-rule.md)  
 描述如何在 XML 大量載入內解譯 `sql:relationship` 註解。  
  
 [sql： 對應&#40;SQLXML 4.0&#41;](annotation-interpretation-sql-mapped.md)  
 描述如何在 XML 大量載入內解譯 `sql:mapped` 註解。  
  
 [sql: limit-value-欄位和 sql: limit-value-值&#40;SQLXML 4.0&#41;](annotation-interpretation-sql-limit-field-and-sql-limit-value.md)  
 描述如何在 XML 大量載入內解譯 `sql:limit-field` 和 `sql:limit-value` 註解。  
  
 [sql: overflow-field-欄位&#40;SQLXML 4.0&#41;](annotation-interpretation-sql-overflow-field.md)  
 描述如何在 XML 大量載入內解譯 `sql:overflow` 註解。  
  
 [其他註解&#40;SQLXML 4.0&#41;](annotation-interpretation-other-annotations.md)  
 描述如何在 XML 大量載入內解譯下列註解：`sql:id-prefix`、`sql:use-cdata`、`sql:url-encode`、`sql:is-mapping-schema`、`sql:key-fields`。  
  
  