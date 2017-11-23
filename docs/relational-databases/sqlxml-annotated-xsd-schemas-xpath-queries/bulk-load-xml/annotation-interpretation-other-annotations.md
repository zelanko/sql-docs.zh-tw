---
title: "其他註解 (SQLXML 4.0) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: sqlxml
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-xml
ms.tgt_pltfrm: 
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
caps.latest.revision: "20"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7c66f2bb5bb89e2d8ac46fb8e6d20a8c79a49b27
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="annotation-interpretation---other-annotations"></a>註解的解譯-其他註解
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]除了之前的主題，這一節中討論的註解，XML 大量載入會將解譯這些其他註解，，如下所示：  
  
 **sql: id-prefix-前置詞**  
 如果結構描述指定 XML 資料的前置詞，XML 大量載入會先移除這些前置詞，然後再將資料傳送給 Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
 **sql: use-cdata-cdata**  
 XML 大量載入會讀取 CDATA 區段中所儲存的文字，然後將其傳送給 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
 **sql: url-encode-編碼**  
 XML 大量載入不支援此註釋。 例如，您不能在 XML 資料輸入中指定 URL，然後預期 XML 大量載入會從該位置讀取資料，將它儲存在資料庫中。  
  
 **sql： 為對應結構描述**  
 XML 大量載入不支援此註解，也不支援**sql: id-prefix**。  
  
> [!NOTE]  
>  XML 大量載入不支援內嵌對應結構描述。  
  
 **sql: key-fields-欄位**  
 XML 大量載入一定會忽略此註解。  
  
## <a name="see-also"></a>請參閱＜  
 [註解的解譯 &#40;SQLXML 4.0 &#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sqlxml-4-0.md)  
  
  
