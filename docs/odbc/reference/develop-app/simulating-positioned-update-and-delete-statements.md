---
title: 模擬定位的 Update 和 Delete 陳述式 |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 6d98d40ae24c68f90a304edb0293febfe76fac2c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62445890"
---
# <a name="simulating-positioned-update-and-delete-statements"></a>模擬定點更新和刪除陳述式
如果資料來源不支援定位的 update 以及 delete 陳述式，可以模擬這些驅動程式。 比方說，ODBC 資料指標程式庫會模擬定位的 update 和 delete 陳述式。 模擬定位的 update 和 delete 陳述式的一般策略是要搜尋的項目轉換定位陳述式。 這是藉由取代**WHERE CURRENT OF**子句以搜尋**其中**子句可識別目前的資料列。  
  
 例如，因為 CustID 資料行可唯一識別 Customers 資料表中的每個資料列，定位 delete 陳述式  
  
```  
DELETE FROM Customers WHERE CURRENT OF CustCursor  
```  
  
 可能會轉換成  
  
```  
DELETE FROM Customers WHERE (CustID = ?)  
```  
  
 驅動程式可能會使用下列其中一種*資料列識別碼*中**其中**子句：  
  
-   其值是用來識別唯一資料表中的每個資料列的資料行。 例如，呼叫**SQLSpecialColumns** SQL_BEST_ROWID 會傳回最佳的資料行或一組提供此用途的資料行。  
  
-   虛擬資料行，某些資料來源，以用來唯一識別每個資料列所提供。 這些可能也會擷取藉由呼叫**SQLSpecialColumns**。  
  
-   唯一索引，如果有的話。  
  
-   在結果中的所有資料行設定。  
  
 完全驅動程式應該使用哪些資料行**其中**子句，它會建構取決於驅動程式。 針對某些資料來源，決定資料列識別碼可能成本高昂。 不過，它會是更快速執行，並保證模擬的陳述式會更新，或刪除最多一個資料列。 根據基礎 dbms 的功能，使用資料列識別碼可能會耗費資源的設定。 不過，它會是更快速執行，並保證模擬的陳述式會更新或刪除只有一個資料列。 使用結果集中的所有資料行的選項是通常更容易設定。 不過，執行速度慢且如果資料行可唯一識別資料列，可能會導致意外更新或刪除的資料列，特別是當選取結果清單設定時，不包含存在基礎資料表中的所有資料行。  
  
 根據其中一個先前的策略，驅動程式支援時，應用程式可以選擇哪一種策略它想要使用 SQL_ATTR_SIMULATE_CURSOR 陳述式屬性的驅動程式。 雖然看起來有點奇怪，應用程式可能會不小心更新或刪除資料列項目，應用程式可以去除此風險，確保結果集中的資料行可唯一識別結果集中的每個資料列。 這會儲存驅動程式不必這麼做的努力。  
  
 如果驅動程式選擇要使用的資料列識別碼，它會攔截**SELECT FOR UPDATE**建立結果集的陳述式。 如果選取清單中的資料行不會有效地識別資料列，驅動程式會加入必要的資料行至 select 清單的結尾。 某些資料來源有一定會唯一識別資料列，例如在 Oracle; ROWID 資料行的單一資料行如果使用這類資料行，驅動程式會使用此。 否則，此驅動程式會呼叫**SQLSpecialColumns**中每個資料表**FROM**子句來擷取唯一識別每個資料列的資料行清單。 常見的限制所產生的這項技術是資料指標模擬失敗時，如果有多個資料表中的**FROM**子句。  
  
 不論如何，驅動程式會識別資料列，它通常會去除**FOR UPDATE OF**關閉子句**SELECT FOR UPDATE**再將它傳送至資料來源的陳述式。 **的更新的**子句只能與定位的 update 和 delete 陳述式。 不支援的資料來源定位的 update 和 delete 陳述式通常都不支援它。  
  
 當應用程式提交定位的 update 或 delete 陳述式執行時，驅動程式會取代**WHERE CURRENT OF**子句**其中**子句包含的資料列識別碼。 這些資料行的值會從它會使用每個資料行的驅動程式所維護的快取擷取**其中**子句。 驅動程式已取代後**其中**子句，該陳述式傳送到資料來源，以便執行。  
  
 例如，假設應用程式提交下列陳述式來建立結果集：  
  
```  
SELECT Name, Address, Phone FROM Customers FOR UPDATE OF Phone, Address  
```  
  
 如果應用程式設定要求可保證唯一性的 SQL_ATTR_SIMULATE_CURSOR，而且如果資料來源未提供一定會唯一識別資料列的虛擬資料行，驅動程式會呼叫**SQLSpecialColumns**的Customers 資料表中，會探索 CustID 是 Customers 資料表的索引鍵並將其新增到選取清單中，並去除**FOR UPDATE OF**子句：  
  
```  
SELECT Name, Address, Phone, CustID FROM Customers  
```  
  
 如果應用程式未要求可保證唯一性，驅動程式只去除**FOR UPDATE OF**子句：  
  
```  
SELECT Name, Address, Phone FROM Customers  
```  
  
 假設應用程式捲動的結果集，並將下列定位的 update 陳述式來執行，其中 Cust 是結果集的資料指標的名稱：  
  
```  
UPDATE Customers SET Address = ?, Phone = ? WHERE CURRENT OF Cust  
```  
  
 如果應用程式未要求可保證唯一性，驅動程式將會取代**其中**子句將 CustID 參數繫結到它的快取中的變數：  
  
```  
UPDATE Customers SET Address = ?, Phone = ? WHERE (CustID = ?)  
```  
  
 如果應用程式未要求可保證唯一性，驅動程式將會取代**其中**子句和繫結的名稱、 地址和電話的參數，此子句可用於快取中的變數中：  
  
```  
UPDATE Customers SET Address = ?, Phone = ?  
   WHERE (Name = ?) AND (Address = ?) AND (Phone = ?)  
```
