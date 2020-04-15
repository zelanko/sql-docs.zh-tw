---
title: 參數資料型態 :微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], parameters
- parameter data type [ODBC]
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
ms.assetid: fd7e99d8-d26a-408c-9733-6ffccde99f75
author: David-Engel
ms.author: v-daenge
ms.reviewer: ''
ms.openlocfilehash: f29bb70937df32e03480c13c7ef739eb273f15eb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303579"
---
# <a name="parameter-data-types"></a>參數資料類型
即使使用**SQLBind 參數**指定的每個參數都是使用 SQL 資料類型定義的,但 SQL 語句中的參數沒有內在數據類型。 因此,僅當參數標記的數據類型可以從語句中的另一個操作數推斷出來時,才能包含在 SQL 語句中。 例如,在算術表示式中,如 ? • COLUMN1,可以從 COLUMN1 表示的命名列的數據類型推斷參數的數據類型。 如果無法確定數據類型,則應用程式無法使用參數標記。  
  
 下表描述了如何根據 SQL-92 確定多種類型的參數的數據類型。 有關在使用其他 SQL 子句時推斷參數類型的更全面的規範,請參閱 SQL-92 規範。  
  
|參數的位置|假定資料型別|  
|---------------------------|-----------------------|  
|二進位元數或比較運算子的一個操作數|與其他操作數相同|  
|**在「之間」** 子句的第一個操作數|與第二個操作數相同|  
|**在 BETWEEN**子句的第二個或第三個操作數|與第一個操作數相同|  
|與**IN**一起使用的表示式|與子查詢的第一個值或結果列相同|  
|與**IN**一起使用的值|如果表示式中有參數標記,則與運算式或第一個值相同|  
|與**LIKE**一起使用的模式值|VARCHAR|  
|與**更新**一起使用的更新值|與更新欄位|
