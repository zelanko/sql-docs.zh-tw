---
title: "ODBC Core 子機碼 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- subkeys [ODBC], core subkey
- registry entries for components [ODBC], core subkey
- core subkey [ODBC]
ms.assetid: 055b31fc-f96c-450b-a596-d4570079fbf2
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ad7a45f0f3272e1e2d7ae799ab1ca86bfb90b9be
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

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

