---
description: ORDER BY 運算式清單
title: ORDER BY 運算式清單 |Microsoft Docs
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
ms.openlocfilehash: fd084a1012d445c89cacba168f21267238bc250f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88340614"
---
# <a name="order-by-expression-list"></a>ORDER BY 運算式清單
運算式可以在 ORDER BY 子句中使用。 例如，在下列子句中，資料表是以三個索引鍵運算式排序： a + b、c + d 和 e。  
  
```  
SELECT * FROM emp  
ORDER BY a+b,c+d,e  
```  
  
 Set 函數或包含 set 函數的運算式上不允許排序。
