---
title: 範本快取（SQLXML）
description: 瞭解如何使用 SQLXML 4.0 中的範本快取，在執行範本時大幅改善效能。
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- registry keys [SQLXML]
- cache [SQLXML]
- templates [SQLXML], caching
ms.assetid: 73e151c6-b24e-4422-a116-51e0846bc6f5
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8055210f85a23d37bb670091bd19cd4ce5c01663
ms.sourcegitcommit: 9921501952147b9ce3e85a1712495d5b3eb13e5b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/29/2020
ms.locfileid: "84215803"
---
# <a name="template-caching-sqlxml-40"></a>範本快取 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  範本快取會大幅改善效能。 如果設定範本快取，範本在第一次執行後仍會保留在記憶體中。 這樣可以增進後續執行範本的效能。  
  
 您可以在登錄中加入下列機碼來設定範本快取大小：  
  
```  
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SQLXML4\TemplateCacheSize  
```  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteRegistry](../../../includes/ssnoteregistry-md.md)]  
  
 範本大小應該根據可用的記憶體以及您要使用的範本數目來設定。 **TemplateCacheSize**大小的預設值為31。 如果範本存取速度似乎緩慢，您可以增加快取大小，或者如果記憶體不足，則減少快取大小。  
  
 為獲得較佳的效能，建議您將**TemplateCacheSize**設定為高於您通常使用的範本數目。 如果**TemlateCacheSize**小於您擁有的範本數目，效能會隨著範本數目的增加而降低。 **TemplateCacheSize**可以設定為最大值128。  
  
 每次使用快取的範本時，就會檢查範本檔的修改時間以查看該範本檔是否需要重新整理。 這是因為磁碟副本比快取副本新的緣故。  
  
> [!NOTE]  
>  系統不會快取範本參數和命令屬性。  
  
## <a name="see-also"></a>另請參閱  
 [架構快取 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/schema-caching-sqlxml-4-0.md)   
 [XSL Caching &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/xsl-caching-sqlxml-4-0.md)  
  
  
