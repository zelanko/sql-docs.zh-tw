---
title: XSL 快取 (SQLXML 4.0) |Microsoft 文件
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- registry keys [SQLXML]
- cache [SQLXML]
- XSL caching [SQLXML]
ms.assetid: 91994142-32f0-4d8d-a8cf-eb0d8b1f1999
caps.latest.revision: 24
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 7dcb5aa54b7cca2c5d76096c5c819e31889293db
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
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
  
 XSL 快取大小應該根據可用的記憶體以及您要使用的 XSL 樣式表數目來設定。 預設值是**XSLCacheSize**大小為 31。 如果 XSL 存取速度似乎緩慢，您可以增加快取大小，或者如果記憶體不足，則減少快取大小。  
  
 如需更好的效能，建議您設定**XSLCacheSize**比您通常使用的 XSL 樣式表數目高。 如果**XSLCacheSize**是小於的數目 XSL 樣式的表，在效能降低的 XSL 樣式表增加而增加數字。 **XSLCacheSize**可以設為上限 128。  
  
 每次使用快取的 XSL 樣式表時，就會檢查 XSL 檔的修改時間以判斷該 XSL 檔是否需要重新整理。 這是因為磁碟副本比快取副本新的緣故。  
  
## <a name="see-also"></a>另請參閱  
 [範本快取 & #40;SQLXML 4.0 & #41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/template-caching-sqlxml-4-0.md)   
 [結構描述快取 & #40;SQLXML 4.0 & #41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/schema-caching-sqlxml-4-0.md)  
  
  
