---
title: ORDER BY 運算式-list |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81291218"
---
# <a name="order-by-expression-list"></a>ORDER BY 運算式清單
運算式可以在 ORDER BY 子句中使用。 例如，在下列子句中，資料表是以三個索引鍵運算式排序： a + b、c + d 和 e。  
  
```  
SELECT * FROM emp  
ORDER BY a+b,c+d,e  
```  
  
 Set 函數或包含 set 函數的運算式不允許排序。
