---
title: "ORDER BY 運算式清單 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ORDER BY clause [ODBC]
- SQL grammar [ODBC], order by clause
ms.assetid: 5ef88186-a99f-4e2c-a3f3-98a42d4f03a5
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b64ad53abb02d04077548a1b4483d89307b0a5a0
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="order-by-expression-list"></a>ORDER BY 運算式清單
運算式可以使用 ORDER BY 子句中。 例如，下列子句中資料表會依據排序三個索引鍵的運算式： a + b、 c + d 和 e。  
  
```  
SELECT * FROM emp  
ORDER BY a+b,c+d,e  
```  
  
 沒有順序允許 set 函式或包含 set 函式的運算式。

