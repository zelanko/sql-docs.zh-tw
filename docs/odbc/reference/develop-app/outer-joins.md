---
title: "外部聯結 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- outer join escape sequences [ODBC]
- escape sequences [ODBC], outer join
ms.assetid: be1a0203-5da9-4871-9566-4bd3fbc0895c
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: aff4448df5ec42e29da6c49fe0ace7f0334a1174
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="outer-joins"></a>外部聯結
ODBC 支援以 sql-92 左、 右方和完整外部聯結語法。 外部聯結的逸出序列是  
  
 **{oj** *外部聯結***}**  
  
 其中*外部聯結*是  
  
 *資料表參考*{**左 &#124;權限 &#124;FULL} OUTER JOIN** {*資料表參考*&#124;*外部聯結*} **ON** *搜尋條件*  
  
 *資料表參考*指定資料表名稱，和*搜尋條件*指定之間的聯結條件*資料表參考*。  
  
 外部聯結要求必須出現在之後**FROM**關鍵字，以及之前**其中**子句 （如果有的話）。 如需完整語法的資訊，請參閱[外部聯結逸出序列](../../../odbc/reference/appendixes/outer-join-escape-sequence.md)附錄 c: SQL 文法中。  
  
 例如，下列 SQL 陳述式建立相同的結果集，列出所有客戶，並顯示具有開啟的訂單。 第一個陳述式會使用逸出序列語法。 第二個陳述式 Oracle 中使用原生的語法，並不互通。  
  
```  
SELECT Customers.CustID, Customers.Name, Orders.OrderID, Orders.Status  
   FROM {oj Customers LEFT OUTER JOIN Orders ON Customers.CustID=Orders.CustID}  
   WHERE Orders.Status='OPEN'  
  
SELECT Customers.CustID, Customers.Name, Orders.OrderID, Orders.Status  
   FROM Customers, Orders  
   WHERE (Orders.Status='OPEN') AND (Customers.CustID= Orders.CustID(+))  
```  
  
 若要判斷資料來源和驅動程式支援的外部聯結的類型，應用程式呼叫**SQLGetInfo** SQL_OJ_CAPABILITIES 具有旗標。 可能支援的外部聯結的類型左、 右、 完整或巢狀外部聯結。外部聯結中的資料行名稱中**ON**子句不會有個別的資料表名稱中的順序相同**OUTER JOIN**子句; 搭配外部聯結; 以及使用外部聯結的內部聯結任何 ODBC 的比較運算子。 如果 SQL_OJ_CAPABILITIES 資訊類型會傳回 0，則不支援任何外部聯結子句。

