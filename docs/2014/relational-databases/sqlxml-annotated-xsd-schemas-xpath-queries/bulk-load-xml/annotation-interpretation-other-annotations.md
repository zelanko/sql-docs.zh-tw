---
title: 其他註解 (SQLXML 4.0) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: fff698fc4eb92dd1bade50274a289f861e07ede0
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/22/2019
ms.locfileid: "66013605"
---
# <a name="other-annotations-sqlxml-40"></a>其他註解 (SQLXML 4.0)
  除了本章節先前的主題所討論的註解以外，XML 大量載入還會解譯這些其他註解，如下所示：  
  
 `sql:id-prefix`  
 如果結構描述指定 XML 資料的前置詞，XML 大量載入會先移除這些前置詞，然後再將資料傳送給 Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
 `sql:use-cdata`  
 XML 大量載入會讀取 CDATA 區段中所儲存的文字，然後將其傳送給 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
 `sql:url-encode`  
 XML 大量載入不支援此註釋。 例如，您不能在 XML 資料輸入中指定 URL，然後預期 XML 大量載入會從該位置讀取資料，將它儲存在資料庫中。  
  
 `sql:is-mapping-schema`  
 XML 大量載入不支援此註解，也不支援 `sql:id`。  
  
> [!NOTE]  
>  XML 大量載入不支援內嵌對應結構描述。  
  
 `sql:key-fields`  
 XML 大量載入一定會忽略此註解。  
  
## <a name="see-also"></a>另請參閱  
 [註解解譯&#40;SQLXML 4.0&#41;](annotation-interpretation-sqlxml-4-0.md)  
  
  
