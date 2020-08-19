---
description: 外部聯結
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
ms.openlocfilehash: a9be14c2b7c0dd6cdebc458fd22dc090862eb9dc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429120"
---
# <a name="outer-joins"></a>外部聯結
ODBC 支援 SQL-92 left、right 和 full outer join 語法。 外部聯結的 escape 序列是  
  
 **{oj** _outer-join_**}**  
  
 其中 *outer join* 是  
  
 *資料表參考* {**左 &#124; 右 &#124; FULL} 外部聯結** {*資料表參考* &#124; *外部聯結* **}** _搜尋條件_  
  
 *資料表參考* 會指定資料表名稱，而 *搜尋條件* 會指定 *資料表參考*之間的聯結條件。  
  
 外部聯結要求必須出現在 **FROM** 關鍵字之後，而 WHERE 子句 (**（** 如果有的話）存在) 。 如需完整的語法資訊，請參閱附錄 C： SQL 文法中的 [外部聯結 Escape 序列](../../../odbc/reference/appendixes/outer-join-escape-sequence.md) 。  
  
 例如，下列 SQL 語句會建立相同的結果集，其中會列出所有客戶並顯示有開啟訂單的所有客戶。 第一個語句使用 escape 序列語法。 第二個語句使用 Oracle 的原生語法，而且無法互通。  
  
```  
SELECT Customers.CustID, Customers.Name, Orders.OrderID, Orders.Status  
   FROM {oj Customers LEFT OUTER JOIN Orders ON Customers.CustID=Orders.CustID}  
   WHERE Orders.Status='OPEN'  
  
SELECT Customers.CustID, Customers.Name, Orders.OrderID, Orders.Status  
   FROM Customers, Orders  
   WHERE (Orders.Status='OPEN') AND (Customers.CustID= Orders.CustID(+))  
```  
  
 為了判斷資料來源和驅動程式支援的外部聯結類型，應用程式會使用 SQL_OJ_CAPABILITIES 旗標來呼叫 **SQLGetInfo** 。 可能支援的外部聯結類型為 left、right、full 或 nested outer join;在外部聯結中， **ON** 子句中的資料行名稱與 **外部聯結** 子句中的個別資料表名稱沒有相同的順序;內部聯結搭配外部聯結;以及使用任何 ODBC 比較運算子的外部聯結。 如果 SQL_OJ_CAPABILITIES 資訊類型傳回0，則不支援任何外部聯結子句。
