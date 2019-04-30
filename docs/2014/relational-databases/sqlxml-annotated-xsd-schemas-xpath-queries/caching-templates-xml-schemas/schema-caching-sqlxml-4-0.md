---
title: 快取 (SQLXML 4.0) 的結構描述 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- registry keys [SQLXML]
- cache [SQLXML]
- schemas [SQLXML]
ms.assetid: 7e5fda21-b435-41fd-b637-8b616560a93f
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2a9b4eced3cb4e02e2053a90edd701bda3139358
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63209640"
---
# <a name="schema-caching-sqlxml-40"></a>結構描述快取 (SQLXML 4.0)
  使用 XML for Microsoft SQL Server 2000 Web Release 1、 Microsoft SQLXML 2.0 和 SQLXML 3.0 的並排顯示安裝，您可以明確地控制所有版本中使用下列登錄機碼的快取的結構描述：  
  
 Web Release 1：  
  
```  
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SQLXMLX\SchemaCacheSize  
```  
  
 SQLXML 2.0:  
  
```  
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SQLXML2\SchemaCacheSize  
```  
  
 SQLXML 3.0：  
  
```  
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SQLXML3\SchemaCacheSize  
```  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteRegistry](../../../includes/ssnoteregistry-md.md)]  
  
 如需並排顯示安裝的詳細資訊，請參閱[What's New in SQLXML 4.0 SP1](../../sqlxml/what-s-new-in-sqlxml-4-0-sp1.md)。  
  
 結構描述快取能大幅提升 XPath 查詢的效能。 當 XPath 查詢針對對應結構描述執行時，結構描述會儲存在記憶體中，而且會在記憶體中建立所需的資料結構。 如果設定結構描述快取，結構描述仍會保留在記憶體中，藉以提升後續 XPath 查詢的效能。  
  
 您可以在登錄中加入上述機碼來設定結構描述快取大小  
  
 結構描述大小應該根據可用的記憶體以及您要使用的結構描述數目來設定。 預設值**SchemaCacheSize**大小為 31。 如果您設定**SchemaCacheSize**更高版本，會使用更多的記憶體。 因此，如果結構描述存取速度似乎緩慢，您可以增加快取大小，或者如果記憶體不足，則減少快取大小。  
  
 基於效能考量，建議您設定**SchemaCacheSize**比您通常會使用對應結構描述數目高。 當結構描述數目增加，如果**SchemaCacheSize**小於您擁有的結構描述數目，效能會降低。  
  
> [!NOTE]  
>  在開發期間，建議您不要快取結構描述，因為您對結構描述所做的變更，約有兩分鐘不會反映在快取中。  
  
## <a name="see-also"></a>另請參閱  
 [範本快取&#40;SQLXML 4.0&#41;](template-caching-sqlxml-4-0.md)   
 [XSL 快取&#40;SQLXML 4.0&#41;](xsl-caching-sqlxml-4-0.md)  
  
  
