---
title: 依表示式清單排序 :微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ORDER BY clause [ODBC]
- SQL grammar [ODBC], order by clause
ms.assetid: 5ef88186-a99f-4e2c-a3f3-98a42d4f03a5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 272fa0be844569d322679d444807f8c332b4837b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81291218"
---
# <a name="order-by-expression-list"></a>ORDER BY 運算式清單
表達式可以在 ORDER BY 子句中使用。 例如,在以下子句中,表按三個鍵表達式排序:a_b、c_d 和 e。  
  
```  
SELECT * FROM emp  
ORDER BY a+b,c+d,e  
```  
  
 不允許對集函數或包含集函數的運算式排序。
