---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 85d7642620d510ebba050a3fbc4348898e070070
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68107527"
---
# <a name="simulating-positioned-update-and-delete-statements"></a>模擬定點更新和刪除陳述式
如果資料來源不支援定位 update 和 delete 語句，驅動程式就可以模擬它們。 例如，ODBC 資料指標程式庫會模擬定位的 update 和 delete 語句。 模擬定位 update 和 delete 語句的一般策略，是將定位語句轉換成搜尋的語句。 這是藉由使用可識別目前資料列的搜尋**where**子句來取代**WHERE CURRENT** of 子句來完成。  
  
 例如，因為 CustID 資料行會唯一識別 Customers 資料表中的每個資料列，所以定位 delete 語句  
  
```  
DELETE FROM Customers WHERE CURRENT OF CustCursor  
```  
  
 可能會轉換為  
  
```  
DELETE FROM Customers WHERE (CustID = ?)  
```  
  
 此驅動程式可能會使用**WHERE**子句中的下列其中一個資料*列識別碼*：  
  
-   其值可以唯一識別資料表中每個資料列的資料行。 例如，使用 SQL_BEST_ROWID 呼叫**SQLSpecialColumns**會傳回服務此用途的最佳資料行或資料行集合。  
  
-   以唯一識別每個資料列的目的，是由某些資料來源提供的虛擬資料行。 您也可以藉由呼叫**SQLSpecialColumns**來加以抓取。  
  
-   唯一索引（如果有的話）。  
  
-   結果集中的所有資料行。  
  
 驅動程式在其所結構的**WHERE**子句中應該使用的資料行，會視驅動程式而定。 在某些資料來源上，判斷資料列識別碼可能會很耗費資源。 不過，執行並保證模擬的語句最多隻會更新或刪除一個資料列，會比較快速。 視基礎 DBMS 的功能而定，使用資料列識別碼可能會耗用很多成本來設定。 不過，執行並保證模擬的語句只會更新或刪除一個資料列，會比較快速。 在結果集中使用所有資料行的選項，通常很容易設定。 不過，執行速度較慢，而且如果資料行不能唯一識別資料列，可能會導致意外更新或刪除資料列，特別是當結果集的選取清單未包含基礎資料表中存在的所有資料行時。  
  
 視驅動程式支援的前述策略而定，應用程式可以選擇要讓驅動程式與 SQL_ATTR_SIMULATE_CURSOR 語句屬性搭配使用的策略。 雖然應用程式在意外更新或刪除資料列時可能會有奇怪的風險，但應用程式可以藉由確保結果集中的資料行唯一識別結果集中的每個資料列，來移除此風險。 這可節省驅動程式執行這項作業所需的工作。  
  
 如果驅動程式選擇使用資料列識別碼，它會攔截建立結果集的**SELECT FOR UPDATE**語句。 如果選取清單中的資料行無法有效地識別資料列，驅動程式會將必要的資料行新增至選取清單的結尾。 某些資料來源具有單一資料行，它一律會唯一識別一列，例如 Oracle 中的 ROWID 資料行。如果有這類資料行，驅動程式就會使用這個。 否則，驅動程式會針對**FROM**子句中的每個資料表呼叫**SQLSpecialColumns** ，以取得可唯一識別每個資料列的資料行清單。 這項技術所產生的常見限制是，如果**from**子句中有一個以上的資料表，資料指標模擬就會失敗。  
  
 無論驅動程式如何識別資料列，通常會先將**FOR update**子句從**SELECT FOR update**語句中去除，再將它傳送至資料來源。 子句的**FOR update**僅適用于定位的 update 和 delete 語句。 不支援定點更新和刪除語句的資料來源通常不支援。  
  
 當應用程式提交要執行的定點更新或 delete 語句時，驅動程式會以包含資料列識別碼的**where**子句取代**where CURRENT** of 子句。 這些資料行的值會從驅動程式針對**WHERE**子句中所使用的每個資料行所維護的快取中抓取。 在驅動程式取代了**WHERE**子句之後，它會將語句傳送到資料來源以供執行。  
  
 例如，假設應用程式提交下列語句來建立結果集：  
  
```  
SELECT Name, Address, Phone FROM Customers FOR UPDATE OF Phone, Address  
```  
  
 如果應用程式已將 SQL_ATTR_SIMULATE_CURSOR 設定為要求保證唯一性，而且如果資料來源未提供一律唯一識別資料列的虛擬資料行，則驅動程式會呼叫 Customers 資料表的**SQLSpecialColumns** 、發現 CustID 是 customers 資料表的索引鍵，並將它加入至選取清單，並去除子句的**for UPDATE** ：  
  
```  
SELECT Name, Address, Phone, CustID FROM Customers  
```  
  
 如果應用程式未要求保證唯一性，驅動程式只會去除子句的**UPDATE** ：  
  
```  
SELECT Name, Address, Phone FROM Customers  
```  
  
 假設應用程式會逐一查看結果集，並提交下列定位的 update 語句來執行，其中的「查詢」是結果集上的資料指標名稱：  
  
```  
UPDATE Customers SET Address = ?, Phone = ? WHERE CURRENT OF Cust  
```  
  
 如果應用程式未要求保證唯一性，驅動程式會取代**WHERE**子句，並將 CustID 參數系結至其快取中的變數：  
  
```  
UPDATE Customers SET Address = ?, Phone = ? WHERE (CustID = ?)  
```  
  
 如果應用程式未要求保證唯一性，驅動程式會取代**WHERE**子句，並將此子句中的名稱、位址和電話參數系結至其快取中的變數：  
  
```  
UPDATE Customers SET Address = ?, Phone = ?  
   WHERE (Name = ?) AND (Address = ?) AND (Phone = ?)  
```
