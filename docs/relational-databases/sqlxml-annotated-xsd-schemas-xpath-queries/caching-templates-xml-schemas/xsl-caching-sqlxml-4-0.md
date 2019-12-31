---
title: XSL 快取（SQLXML）
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- registry keys [SQLXML]
- cache [SQLXML]
- XSL caching [SQLXML]
ms.assetid: 91994142-32f0-4d8d-a8cf-eb0d8b1f1999
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 265ce1db6f57f378dfaa7c0818914edd121b7d30
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/19/2019
ms.locfileid: "75257327"
---
# <a name="xsl-caching-sqlxml-40"></a>XSL 快取 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  快取 XSL 樣式表可以改善效能。 第一次執行之後，如果 XSL 快取設定為 ON，XSL 樣式表仍保持在記憶體中；這樣可以改善後續處理的效能。 預設值是 ON。  
  
 您可以在登錄中加入下列機碼來設定 XSL 快取大小：  
  
```  
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SQLXML4\XSLCacheSize  
```  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteRegistry](../../../includes/ssnoteregistry-md.md)]  
  
 XSL 快取大小應該根據可用的記憶體以及您要使用的 XSL 樣式表數目來設定。 **XSLCacheSize**大小的預設值為31。 如果 XSL 存取速度似乎緩慢，您可以增加快取大小，或者如果記憶體不足，則減少快取大小。  
  
 為獲得較佳的效能，建議您將**XSLCacheSize**設定得高於通常使用的 XSL 樣式表單數目。 如果**XSLCacheSize**小於您擁有的 xsl 樣式表單數目，效能會隨著 xsl 樣式表單數目的增加而降低。 **XSLCacheSize**可以設定為最大值128。  
  
 每次使用快取的 XSL 樣式表時，就會檢查 XSL 檔的修改時間以判斷該 XSL 檔是否需要重新整理。 這是因為磁碟副本比快取副本新的緣故。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;SQLXML 4.0&#41;的範本快取](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/template-caching-sqlxml-4-0.md)   
 [架構快取 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/schema-caching-sqlxml-4-0.md)  
  
  
