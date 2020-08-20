---
description: 模擬定點更新和刪除陳述式
title: 模擬定位的 Update 和 Delete 語句 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- positioned deletes [ODBC]
- data updates [ODBC], positioned update or delete
- row identifiers [ODBC]
- positioned updates [ODBC]
- updating data [ODBC], positioned update or delete
ms.assetid: b24ed59f-f25b-4646-a135-5f3596abc1a4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 06f6faad1b5b6cb83616575ea8732cac98b88ed0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499811"
---
# <a name="simulating-positioned-update-and-delete-statements"></a>模擬定點更新和刪除陳述式
如果資料來源不支援定位的 update 和 delete 語句，驅動程式就可以模擬這些語句。 例如，ODBC 資料指標程式庫會模擬定位的 update 和 delete 語句。 模擬定位 update 和 delete 語句的一般策略是將定位語句轉換成搜尋的語句。 這是藉由將 **WHERE CURRENT** of 子句取代為用來識別目前資料列的搜尋 **where** 子句來完成。  
  
 例如，因為 CustID 資料行會唯一識別 Customers 資料表中的每個資料列，所以定位的 delete 語句  
  
```  
DELETE FROM Customers WHERE CURRENT OF CustCursor  
```  
  
 可能會轉換成  
  
```  
DELETE FROM Customers WHERE (CustID = ?)  
```  
  
 驅動程式可能會在**WHERE**子句中使用下列其中一個資料*列識別碼*：  
  
-   值可在資料表中唯一識別每個資料列的資料行。 例如，使用 SQL_BEST_ROWID 呼叫 **SQLSpecialColumns** 會傳回提供此用途的最佳資料行或資料行集合。  
  
-   由某些資料來源提供的虛擬資料行，目的是要唯一識別每個資料列。 您也可以藉由呼叫 **SQLSpecialColumns**來進行這些呼叫。  
  
-   唯一索引（如果有的話）。  
  
-   結果集中的所有資料行。  
  
 驅動程式應該在其所建立之 **WHERE** 子句中使用的資料行，取決於驅動程式。 在某些資料來源上，判斷資料列識別碼的成本可能會很高。 但是，執行和保證模擬的語句最多會更新或刪除最多一個資料列，因此執行速度更快。 根據基礎 DBMS 的功能而定，使用資料列識別碼的設定成本可能很高。 但是，執行和保證模擬的語句只會更新或刪除一個資料列，會更快。 在結果集中使用所有資料行的選項通常更容易設定。 不過，執行速度較慢，而且如果資料行不會唯一識別資料列，可能會導致資料列不慎更新或刪除，特別是當結果集的選取清單未包含基礎資料表中的所有資料行時。  
  
 根據驅動程式所支援的前述策略而定，應用程式可以選擇要讓驅動程式搭配 SQL_ATTR_SIMULATE_CURSOR 語句屬性使用的策略。 雖然應用程式可能會因為無意地更新或刪除資料列而產生奇怪的風險，但應用程式可以藉由確保結果集中的資料行能唯一識別結果集中的每個資料列，來移除這項風險。 這樣就可以節省驅動程式。  
  
 如果驅動程式選擇使用資料列識別碼，就會攔截建立結果集的 **SELECT FOR UPDATE** 語句。 如果選取清單中的資料行無法有效識別資料列，驅動程式就會將必要的資料行加入至選取清單的結尾。 某些資料來源具有單一資料行，此資料行一律會唯一識別資料列，例如 Oracle 中的 ROWID 資料行;如果有這類資料行可供使用，則驅動程式會使用此資料行。 否則，驅動程式會針對**FROM**子句中的每個資料表呼叫**SQLSpecialColumns** ，以取得可唯一識別每個資料列的資料行清單。 這項技術所產生的常見限制是，如果 **from** 子句中有多個資料表，則資料指標模擬會失敗。  
  
 無論驅動程式如何識別資料列，它通常會將 **update** of 子句從 **SELECT for update** 語句中移除，然後再傳送到資料來源。 **FOR update** of 子句僅適用于定位的 update 和 delete 語句。 不支援定點更新和刪除語句的資料來源通常不支援。  
  
 當應用程式提交定位的 update 或 delete 語句以執行時，驅動程式會以包含資料列識別碼的**where**子句取代**where CURRENT** of 子句。 這些資料行的值是從驅動程式針對 **WHERE** 子句中使用的每個資料行所維護的快取中抓取。 在驅動程式取代 **WHERE** 子句之後，它會將語句傳送到資料來源以供執行。  
  
 例如，假設應用程式提交下列語句來建立結果集：  
  
```  
SELECT Name, Address, Phone FROM Customers FOR UPDATE OF Phone, Address  
```  
  
 如果應用程式已將 SQL_ATTR_SIMULATE_CURSOR 設定為要求唯一性保證，且資料來源未提供一律可唯一識別資料列的虛擬資料行，則驅動程式會呼叫 Customers 資料表的 **SQLSpecialColumns** ，探索 CustID 是 customers 資料表的索引鍵，並將其新增至選取清單，並移除子句的 **UPDATE** ：  
  
```  
SELECT Name, Address, Phone, CustID FROM Customers  
```  
  
 如果應用程式未要求唯一性保證，驅動程式只會移除子句的 **UPDATE** ：  
  
```  
SELECT Name, Address, Phone FROM Customers  
```  
  
 假設應用程式會滾動整個結果集，並提交下列已定位的 update 語句來執行，其中，在結果集上的是資料指標的名稱：  
  
```  
UPDATE Customers SET Address = ?, Phone = ? WHERE CURRENT OF Cust  
```  
  
 如果應用程式未要求唯一性保證，驅動程式會取代 **WHERE** 子句，並將 CustID 參數系結至其快取中的變數：  
  
```  
UPDATE Customers SET Address = ?, Phone = ? WHERE (CustID = ?)  
```  
  
 如果應用程式未要求唯一性保證，驅動程式會取代 **WHERE** 子句，並將此子句中的名稱、位址和電話參數系結至其快取中的變數：  
  
```  
UPDATE Customers SET Address = ?, Phone = ?  
   WHERE (Name = ?) AND (Address = ?) AND (Phone = ?)  
```
