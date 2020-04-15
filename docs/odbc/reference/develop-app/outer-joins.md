---
title: 外部聯接 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282441"
---
# <a name="outer-joins"></a>外部聯結
ODBC 支援 SQL-92 左、右和完整的外部聯接語法。 外部聯結的逸出序列是  
  
 **[oj** _外部聯接_**]**  
  
 *外部聯結*是  
  
 *表參考*(**左# A0 右&#124;完整] 外部連線**[*表參考*&#124;*外部連線*=_在搜尋條件_**上**  
  
 *表引用*指定表名稱,*搜尋條件*指定*表引用之間的*聯接條件。  
  
 外部聯接請求必須出現在**FROM**關鍵字之後和**WHERE**子句之前(如果存在)。 有關完整的語法資訊,請參閱附錄 C 中的[外部聯接轉義序列](../../../odbc/reference/appendixes/outer-join-escape-sequence.md):SQL 語法。  
  
 例如,以下 SQL 語句創建相同的結果集,該結果集列出所有客戶並顯示已打開的訂單。 第一個語句使用轉義序列語法。 第二個語句使用 Oracle 的本機語法,不可互通。  
  
```  
SELECT Customers.CustID, Customers.Name, Orders.OrderID, Orders.Status  
   FROM {oj Customers LEFT OUTER JOIN Orders ON Customers.CustID=Orders.CustID}  
   WHERE Orders.Status='OPEN'  
  
SELECT Customers.CustID, Customers.Name, Orders.OrderID, Orders.Status  
   FROM Customers, Orders  
   WHERE (Orders.Status='OPEN') AND (Customers.CustID= Orders.CustID(+))  
```  
  
 要確定資料源和驅動程式支援的外部聯接類型,應用程式使用SQL_OJ_CAPABILITIES標誌呼叫**SQLGetInfo。** 可能支援的外部聯接類型為左聯接、右聯接、完整聯接或嵌套外部聯接;**ON**子句中的列名稱與**OUTER JOIN**子句中的相應表名的順序不相同的外部聯接;內部聯接與外部聯接結合;和外部聯接使用任何 ODBC 比較運算符。 如果SQL_OJ_CAPABILITIES資訊類型返回 0,則不支援外部聯接子句。
