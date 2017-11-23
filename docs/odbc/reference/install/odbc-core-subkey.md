---
title: "ODBC Core 子機碼 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- subkeys [ODBC], core subkey
- registry entries for components [ODBC], core subkey
- core subkey [ODBC]
ms.assetid: 055b31fc-f96c-450b-a596-d4570079fbf2
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 85c4e842ef48f412696c4a0c851480915f5d9b27
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="odbc-core-subkey"></a>ODBC Core 子機碼
ODBC Core 子機碼下的值提供的核心元件 （驅動程式管理員、 資料指標程式庫，安裝程式的 DLL，等等） 的使用計數。 下表顯示此值的格式。  
  
|名稱|資料類型|data|  
|----------|---------------|----------|  
|UsageCount|REG_DWORD|*計數*|  
  
 例如，假設已由三個不同的應用程式和兩個不同的驅動程式的安裝程式安裝的 ODBC 核心元件。 ODBC Core 子機碼下的值會是：  
  
```  
UsageCount : REG_DWORD : 0x5  
```
