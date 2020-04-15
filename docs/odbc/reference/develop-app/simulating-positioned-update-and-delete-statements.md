---
title: 類比定位更新與刪除語句 |微軟文件
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
ms.openlocfilehash: e1eb498a99180d145147e67c8955eeb7a0027024
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301989"
---
# <a name="simulating-positioned-update-and-delete-statements"></a>模擬定點更新和刪除陳述式
如果數據來源不支援定位更新和刪除語句,驅動程式可以類比這些語句。 例如,ODBC 游標庫類比定位更新和刪除語句。 類比定位更新和刪除語句的一般策略是將定位語句轉換為搜索的語句。 這是通過將**WHERE CURRENT OF**子句替換為標識當前行的搜索**WHERE**子句來實現的。  
  
 例如,由於 CustID 列唯一識別了「客戶」表中的每一行,因此定位刪除語句  
  
```  
DELETE FROM Customers WHERE CURRENT OF CustCursor  
```  
  
 可能轉換為  
  
```  
DELETE FROM Customers WHERE (CustID = ?)  
```  
  
 驅動程式可以使用**WHERE**子句中的以下*行標識符*之一:  
  
-   其值用於唯一標識表中每行的列。 例如,使用SQL_BEST_ROWID調用**SQL 特別列**將返回用於此目的的最佳列或列集。  
  
-   偽列,由某些數據源提供,用於唯一標識每行。 通過調用**SQL 特殊列,** 也可以檢索這些。  
  
-   唯一索引(如果可用)。  
  
-   結果集中的所有列。  
  
 驅動程式在它構造的**WHERE**子句中應使用的確切列取決於驅動程式。 在某些數據源上,確定行標識符可能成本高昂。 但是,執行並保證類比語句最多更新或刪除一行會更快。 根據基礎 DBMS 的功能,使用行標識符設置可能非常昂貴。 但是,執行速度更快,並且保證類比語句將僅更新或刪除一行。 使用結果集中的所有列的選項通常更易於設置。 但是,執行速度較慢,如果列不唯一標識行,則可能導致意外更新或刪除行,尤其是當結果集的 Select 清單不包含基礎表中存在的所有列時。  
  
 根據驅動程式支援的前策略,應用程式可以選擇希望驅動程式與SQL_ATTR_SIMULATE_CURSOR語句屬性一起使用的策略。 儘管應用程式可能會無意中更新或刪除行,但應用程式可以通過確保結果集中的列唯一標識結果集中的每一行來消除此風險。 這節省了驅動程式必須執行此操作的努力。  
  
 如果驅動程式選擇使用行識別碼,它將攔截建立結果集的**選擇更新**「語句。 如果選擇清單中的列無法有效地識別行,則驅動程式將必要的列添加到選擇清單的末尾。 某些資料源具有一個列,該列始終唯一標識行,例如 Oracle 中的 ROWID 列;如果此類列可用,驅動程式將使用此列。 否則,驅動程式會為**FROM**子句中的每個表調用**SQL 特別列**,以檢索唯一標識每一行的列的清單。 此技術產生的一個常見限制是,如果**FROM**子句中有多個表,則游標類比將失敗。  
  
 無論驅動程式如何標識行,它通常會在將"選擇更新"語句發送到資料源之前,將**FOR UPDATE OF**子句從 **"選擇更新"** 語句中剝離。 **FOR 更新子**句僅用於定位的更新和刪除語句。 不支援定位更新和刪除語句的數據來源通常不支援它。  
  
 當應用程式提交定位的更新或刪除語句以執行時,驅動程式將**WHERE CURRENT OF**子句替換為包含行標識符的**WHERE**子句。 這些列的值是從驅動程式為其在**WHERE**子句中使用的每個列維護的緩存中檢索的。 驅動程式替換**WHERE**子句后,它將語句發送到數據源進行執行。  
  
 例如,假設應用程式提交以下文句以建立結果集:  
  
```  
SELECT Name, Address, Phone FROM Customers FOR UPDATE OF Phone, Address  
```  
  
 如果應用程式已設置SQL_ATTR_SIMULATE_CURSOR請求唯一性保證,並且資料源未提供始終唯一標識行的偽列,則驅動程式將調用客戶表的**SQL 特別列**,發現 CustID 是客戶表的鍵,並將其添加到選擇清單中,並刪除**FOR UPDATE OF**子句:  
  
```  
SELECT Name, Address, Phone, CustID FROM Customers  
```  
  
 如果應用程式未請求唯一性保證,則驅動程式僅刪除 FOR 更新**OF**子句:  
  
```  
SELECT Name, Address, Phone FROM Customers  
```  
  
 假設應用程式滾動瀏覽結果集並提交以下定位的更新語句進行執行,其中 Cust 是結果集上的游標名稱:  
  
```  
UPDATE Customers SET Address = ?, Phone = ? WHERE CURRENT OF Cust  
```  
  
 如果應用程式未請求唯一性保證,驅動程式將替換**WHERE**子句並將 CustID 參數綁定到其緩存中的變數:  
  
```  
UPDATE Customers SET Address = ?, Phone = ? WHERE (CustID = ?)  
```  
  
 如果應用程式未請求唯一性保證,驅動程式將替換**WHERE**子句,並將此子句中的名稱、位址和 Phone 參數綁定到其緩存中的變數:  
  
```  
UPDATE Customers SET Address = ?, Phone = ?  
   WHERE (Name = ?) AND (Address = ?) AND (Phone = ?)  
```
