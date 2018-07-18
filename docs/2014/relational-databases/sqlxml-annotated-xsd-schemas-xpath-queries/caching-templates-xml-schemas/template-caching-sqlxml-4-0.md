---
title: 範本快取 (SQLXML 4.0) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- registry keys [SQLXML]
- cache [SQLXML]
- templates [SQLXML], caching
ms.assetid: 73e151c6-b24e-4422-a116-51e0846bc6f5
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 79d5d5ea1cd40d1a2fc167d16da4fa2e2af65a43
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37236578"
---
# <a name="template-caching-sqlxml-40"></a>範本快取 (SQLXML 4.0)
  範本快取會大幅改善效能。 如果設定範本快取，範本在第一次執行後仍會保留在記憶體中。 這樣可以增進後續執行範本的效能。  
  
 您可以在登錄中加入下列機碼來設定範本快取大小：  
  
```  
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SQLXML4\TemplateCacheSize  
```  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteRegistry](../../../includes/ssnoteregistry-md.md)]  
  
 範本大小應該根據可用的記憶體以及您要使用的範本數目來設定。 預設值是**TemplateCacheSize**大小為 31。 如果範本存取速度似乎緩慢，您可以增加快取大小，或者如果記憶體不足，則減少快取大小。  
  
 為了達到最佳效能，建議您設定**TemplateCacheSize**比您通常使用的範本數目高。 如果**TemlateCacheSize**小於您擁有的範本數目，效能會隨著範本增加數目。 **TemplateCacheSize**可以設為上限 128。  
  
 每次使用快取的範本時，就會檢查範本檔的修改時間以查看該範本檔是否需要重新整理。 這是因為磁碟副本比快取副本新的緣故。  
  
> [!NOTE]  
>  系統不會快取範本參數和命令屬性。  
  
## <a name="see-also"></a>另請參閱  
 [結構描述快取&#40;SQLXML 4.0&#41;](schema-caching-sqlxml-4-0.md)   
 [XSL 快取&#40;SQLXML 4.0&#41;](xsl-caching-sqlxml-4-0.md)  
  
  
