---
title: "模擬定位 Update 和 Delete 陳述式 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- positioned deletes [ODBC]
- data updates [ODBC], positioned update or delete
- row identifiers [ODBC]
- positioned updates [ODBC]
- updating data [ODBC], positioned update or delete
ms.assetid: b24ed59f-f25b-4646-a135-5f3596abc1a4
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 68fd71437779741489b5729379d3d5d3358915c0
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="simulating-positioned-update-and-delete-statements"></a>模擬定位的 Update 和 Delete 陳述式
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
  
-   其值是用來識別唯一資料表中的每個資料列的資料行。 例如，呼叫**SQLSpecialColumns** SQL_BEST_ROWID 傳回最佳資料行或一組提供此用途的資料行。  
  
-   虛擬資料行，提供的某些資料來源，以便用來唯一識別每個資料列。 它們也可能可以擷取藉由呼叫**SQLSpecialColumns**。  
  
-   唯一的索引，如果有的話。  
  
-   在結果中的所有資料行設定。  
  
 完全驅動程式應該使用哪些資料行**其中**子句建構取決於驅動程式。 針對某些資料來源，決定資料列識別碼可能會很費時。 不過，速度會執行，可確保模擬的陳述式會更新或刪除最多一個資料列。 根據基礎 DBMS 的功能，使用資料列識別碼費不貲設定。 不過，它會比執行，並保證模擬陳述式會更新或刪除只有一個資料列。 在結果集中使用的所有資料行的選項是通常更容易設定。 不過，若要執行的速度比較緩慢而且如果資料行可唯一識別資料列，可能會導致不小心被更新或刪除的資料列，特別是當結果的選取清單設定時，不包含存在基礎資料表中的所有資料行。  
  
 根據其中一個先前的策略驅動程式支援，應用程式可以選擇它想要 SQL_ATTR_SIMULATE_CURSOR 陳述式屬性搭配使用的驅動程式的策略。 它可能會看起來很奇怪的應用程式可能會不小心更新或刪除資料列，雖然應用程式可以確保結果集中的資料行可唯一識別結果集中的每個資料列，移除此風險。 這可以節省驅動程式執行這項操作的麻煩。  
  
 如果驅動程式選擇要使用資料列識別碼，它會攔截**SELECT FOR UPDATE**建立結果集的陳述式。 選取清單中的資料行不會有效地識別資料列，如果驅動程式會將必要的資料行加入選取清單的結尾。 某些資料來源有一定會唯一識別資料列，例如在 Oracle; ROWID 資料行的單一資料行如果這類資料行功能，此驅動程式會使用此。 否則，驅動程式會呼叫**SQLSpecialColumns**中每個資料表**FROM**子句用來擷取唯一識別每個資料列的資料行清單。 常見的限制所產生的這項技術是資料指標的模擬失敗時，如果有多個資料表中的**FROM**子句。  
  
 不論如何，驅動程式會識別資料列，它通常去除**FOR UPDATE OF** off 子句**SELECT FOR UPDATE**陳述式後再將它傳送至資料來源。 **為更新的**子句只能與定位 update 和 delete 陳述式。 不支援的資料來源定位 update 和 delete 陳述式通常不支援它。  
  
 當應用程式提交定位的 update 或 delete 陳述式執行時，驅動程式將會取代**WHERE CURRENT OF**子句搭配**其中**子句包含的資料列識別碼。 這些資料行的值會從其使用中的每個資料行的驅動程式所維護的快取擷取**其中**子句。 驅動程式已取代之後**其中**子句，它將陳述式傳送到資料來源執行。  
  
 例如，假設應用程式送出下列陳述式來建立結果集：  
  
```  
SELECT Name, Address, Phone FROM Customers FOR UPDATE OF Phone, Address  
```  
  
 如果應用程式設定要求的保證唯一性的 SQL_ATTR_SIMULATE_CURSOR，而且如果資料來源未提供一定會唯一識別資料列的虛擬資料行，驅動程式會呼叫**SQLSpecialColumns**的Customers 資料表中，會探索 CustID 是至 Customers 資料表的索引鍵並將其新增到選取清單中，並移除**FOR UPDATE OF**子句：  
  
```  
SELECT Name, Address, Phone, CustID FROM Customers  
```  
  
 如果應用程式尚未要求保證的唯一性，驅動程式只去除**FOR UPDATE OF**子句：  
  
```  
SELECT Name, Address, Phone FROM Customers  
```  
  
 假設應用程式中捲動的結果集，並提交下列定位的 update 陳述式執行，其中 Cust 是結果集的資料指標的名稱：  
  
```  
UPDATE Customers SET Address = ?, Phone = ? WHERE CURRENT OF Cust  
```  
  
 如果應用程式尚未要求保證的唯一性，驅動程式將會取代**其中**子句將 CustID 參數繫結至其快取中的變數：  
  
```  
UPDATE Customers SET Address = ?, Phone = ? WHERE (CustID = ?)  
```  
  
 如果應用程式尚未要求保證的唯一性，驅動程式將會取代**其中**子句以及繫結的名稱、 地址和電話的參數，這個子句以其快取中的變數：  
  
```  
UPDATE Customers SET Address = ?, Phone = ?  
   WHERE (Name = ?) AND (Address = ?) AND (Phone = ?)  
```
