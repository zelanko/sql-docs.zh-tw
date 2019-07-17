---
title: 其他註解 (SQLXML 4.0) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- url-encode annotation
- sql:key-fields
- use-cdata annotation
- sql:is-mapping-schema
- sql:url-encode
- sql:id-prefix
- sql:use-cdata
- key-fields annotation
- id-prefix annotation [SQLXML]
- is-mapping-schema annotation
ms.assetid: f7b4d37b-d6d3-4ac3-b2fd-a0b534a924e4
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a9a965ee5772ea3c2855a08d838c1d89da343e9d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68066866"
---
# <a name="annotation-interpretation---other-annotations"></a>註解解譯 - 其他註解
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  除了本章節先前的主題所討論的註解以外，XML 大量載入還會解譯這些其他註解，如下所示：  
  
 **sql:id-prefix**  
 如果結構描述指定 XML 資料的前置詞，XML 大量載入會先移除這些前置詞，然後再將資料傳送給 Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
 **sql:use-cdata**  
 XML 大量載入會讀取 CDATA 區段中所儲存的文字，然後將其傳送給 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
 **sql:url-encode**  
 XML 大量載入不支援此註釋。 例如，您不能在 XML 資料輸入中指定 URL，然後預期 XML 大量載入會從該位置讀取資料，將它儲存在資料庫中。  
  
 **sql:is-mapping-schema**  
 XML 大量載入不支援此註解，也不支援**sql: id-prefix**。  
  
> [!NOTE]  
>  XML 大量載入不支援內嵌對應結構描述。  
  
 **sql:key-fields**  
 XML 大量載入一定會忽略此註解。  
  
## <a name="see-also"></a>另請參閱  
 [註解解譯&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sqlxml-4-0.md)  
  
  
