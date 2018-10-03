---
title: 註解解譯 (SQLXML 4.0) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- annotated XSD schemas, XML Bulk Load
- XML Bulk Load [SQLXML], annotation intepretations
- annotations [SQLXML]
- bulk load [SQLXML], annotation interpretations
- annotated XDR schemas, XML Bulk Load
ms.assetid: 1c46bdb6-2812-4a13-b60b-7101c04b299f
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 310829f6e4e38d051942180d87f1e1566cadf7c7
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48225748"
---
# <a name="annotation-interpretation-sqlxml-40"></a>註解的解譯 (SQLXML 4.0)
  本章節的主題描述 XML 大量載入要如何解譯 XSD 結構描述中的註解。 這裡所述的行為也適用於 XDR 結構描述中的註解。  
  
> [!NOTE]  
>  這些主題的資訊只會描述 XML 大量載入在處理時所使用的註解。 SQLXML 4.0 支援之 XSD 結構描述註解的完整清單，請參閱 <<c0> [ 使用的註解 XSD 結構描述中&#40;SQLXML 4.0&#41;](../../sqlxml-annotated-xsd-schemas-using/using-annotations-in-xsd-schemas-sqlxml-4-0.md)。</c0> 如需支援的註解 XDR 結構描述的清單，請參閱 < [Annotated XDR Schemas&#40;在 SQLXML 4.0 中已被取代&#41;](../../sqlxml/annotated-xsd-schemas/annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md)。  
  
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
  
  
