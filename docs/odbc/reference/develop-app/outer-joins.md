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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cd35a8bd0e2a9280d16614a3979dc2af05487e42
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47619606"
---
# <a name="outer-joins"></a>外部聯結
ODBC 支援 SQL-92 左、 右方和完整外部聯結語法。 外部聯結的逸出序列是  
  
 **{oj** *外部-聯結 *}**  
  
 何處*外部聯結*是  
  
 *資料表參考*{**LEFT&#124;權限&#124;完整} 外部聯結**{*資料表參考* &#124; *外部聯結*} **ON** *搜尋條件*  
  
 *資料表引用*指定資料表名稱，並*搜尋條件*指定之間的聯結條件*資料表參考*。  
  
 外部聯結要求必須出現在之後**FROM**關鍵字，以及之前**其中**子句 （如果有的話）。 如需完整語法的資訊，請參閱[外部聯結逸出序列](../../../odbc/reference/appendixes/outer-join-escape-sequence.md)附錄 c: SQL 文法中。  
  
 例如，下列 SQL 陳述式建立相同的結果集，會列出所有的客戶，並顯示具有開啟的訂單。 第一個陳述式會使用逸出序列的語法。 第二個陳述式會使用適用於 Oracle 的原生的語法，而且不具互通性。  
  
```  
SELECT Customers.CustID, Customers.Name, Orders.OrderID, Orders.Status  
   FROM {oj Customers LEFT OUTER JOIN Orders ON Customers.CustID=Orders.CustID}  
   WHERE Orders.Status='OPEN'  
  
SELECT Customers.CustID, Customers.Name, Orders.OrderID, Orders.Status  
   FROM Customers, Orders  
   WHERE (Orders.Status='OPEN') AND (Customers.CustID= Orders.CustID(+))  
```  
  
 若要判斷的外部資料來源及驅動程式支援的聯結類型，應用程式會呼叫**SQLGetInfo** SQL_OJ_CAPABILITIES 具有旗標。 可能支援的外部聯結類型會左右，、 完整或巢狀外部聯結;外部聯結中的資料行名稱在這**ON**子句不需要在其各自的資料表名稱的順序相同**OUTER JOIN**子句; 搭配外部聯結，以及使用的外部聯結的內部聯結任何 ODBC 的比較運算子。 如果 SQL_OJ_CAPABILITIES 資訊類型會傳回 0，則支援外部聯結子句。
