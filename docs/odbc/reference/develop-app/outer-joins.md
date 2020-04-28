---
title: 外部聯結 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- outer join escape sequences [ODBC]
- escape sequences [ODBC], outer join
ms.assetid: be1a0203-5da9-4871-9566-4bd3fbc0895c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 81988d34dca38d5c041ff9f87e9674d7c97d76cc
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81282441"
---
# <a name="outer-joins"></a>外部聯結
ODBC 支援 SQL-92 left、right 和 full outer join 語法。 外部聯結的 escape 序列是  
  
 **{oj** _outer-join_**}**  
  
 其中*外部聯結*是  
  
 *資料表-參考*{**LEFT &#124; RIGHT &#124; FULL} 外部聯結**{*資料表參考*&#124;*外部聯結*}**的**_搜尋條件_  
  
 *資料表參考*會指定資料表名稱，而*搜尋條件*會指定*資料表參考*之間的聯結條件。  
  
 外部聯結要求必須出現在**from**關鍵字之後和**WHERE**子句（如果有的話）的前面。 如需完整的語法資訊，請參閱附錄 C： SQL 文法中的[外部聯結轉義順序](../../../odbc/reference/appendixes/outer-join-escape-sequence.md)。  
  
 例如，下列 SQL 語句會建立相同的結果集，以列出所有客戶，並顯示有開啟訂單的。 第一個語句使用 escape 序列語法。 第二個語句使用 Oracle 的原生語法，而且無法互通。  
  
```  
SELECT Customers.CustID, Customers.Name, Orders.OrderID, Orders.Status  
   FROM {oj Customers LEFT OUTER JOIN Orders ON Customers.CustID=Orders.CustID}  
   WHERE Orders.Status='OPEN'  
  
SELECT Customers.CustID, Customers.Name, Orders.OrderID, Orders.Status  
   FROM Customers, Orders  
   WHERE (Orders.Status='OPEN') AND (Customers.CustID= Orders.CustID(+))  
```  
  
 為了判斷資料來源和驅動程式支援的外部聯結類型，應用程式會使用 SQL_OJ_CAPABILITIES 旗標來呼叫**SQLGetInfo** 。 可能支援的外部聯結類型包括 left、right、full 或 nested outer join;**ON**子句中的資料行名稱與**外部聯結**子句中的個別資料表名稱順序不相同的外部聯結;內部聯結搭配外部聯結使用;和使用任何 ODBC 比較運算子的外部聯結。 如果 SQL_OJ_CAPABILITIES 資訊類型傳回0，則不支援任何外部聯結子句。
