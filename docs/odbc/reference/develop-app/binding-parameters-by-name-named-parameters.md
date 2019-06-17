---
title: 繫結參數 （具名參數） 的名稱 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- named parameters [ODBC]
- binding parameters by name [ODBC]
ms.assetid: e2c3da5a-6c10-4dd5-acf9-e951eea71a6b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 68dfb8976312016ee7f2e42fc4fcdecb93fd28cf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63199373"
---
# <a name="binding-parameters-by-name-named-parameters"></a>依名稱繫結參數 (具名參數)
某些 Dbms 允許應用程式名稱，而非在程序呼叫中的位置來指定預存程序的參數。 這種參數稱為*具名參數*。 ODBC 支援具名參數使用。 在 ODBC 中，具名的參數僅用於預存程序的呼叫，並不能用於其他 SQL 陳述式。  
  
 驅動程式會檢查以判斷是否名為使用參數 IPD SQL_DESC_UNNAMED 欄位的值。 如果 SQL_DESC_UNNAMED 未設定為 sql_unnamed 時，驅動程式會使用在 IPD 與 SQL_DESC_NAME 欄位名稱來識別參數。 若要將參數繫結，應用程式可以呼叫**SQLBindParameter**以指定的參數資訊，然後可以呼叫**SQLSetDescField**設 IPD 與 SQL_DESC_NAME 欄位。 當使用具名的參數時，程序呼叫中參數的順序並不重要，並忽略參數的記錄號碼。  
  
 未命名的參數和具名的參數之間的差異是描述元中記錄的數目和程序中的參數號碼之間的關聯性。 當使用未命名的參數時，第一個參數標記被與參數描述元，這被與程序呼叫 （依建立順序） 的第一個參數中的第一筆記錄。 具名的參數使用時，第一個參數標記仍與參數描述項，第一筆記錄，但已不存在之描述項的記錄編號程序中的參數號碼之間的關聯性。 具名的參數請勿使用描述項記錄編號的對應至程序的參數位置;相反地，描述項記錄名稱會對應至程序參數名稱。  
  
> [!NOTE]  
>  如果已啟用自動填入 IPD，驅動程式將會填入描述元描述項記錄的順序會比對程序定義中，參數的順序，即使使用具名的參數。  
  
 如果使用具名的參數，所有參數必須被都具名參數。 如果任何參數不被具名的參數，沒有任何參數 ca 被具名參數。 如果有混合的具名的參數和未命名的參數，則行為會驅動程式相關。  
  
 為具名參數的範例，假設 SQL Server 預存程序已定義，如下所示：  
  
```  
CREATE PROCEDURE test @title_id int = 1, @quote char(30) AS <blah>  
```  
  
 在此程序的第一個參數， @title_id，其預設值為 1。 應用程式可以使用下列程式碼叫用此程序，它會指定只有一個動態參數。 這個參數是具名的參數名稱"\@報價"。  
  
```  
// Prepare the procedure invocation statement.  
SQLPrepare(hstmt, "{call test(?)}", SQL_NTS);  
  
// Populate record 1 of ipd.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR,  
                  30, 0, szQuote, 0, &cbValue);  
  
// Get ipd handle and set the SQL_DESC_NAMED and SQL_DESC_UNNAMED fields  
// for record #1.  
SQLGetStmtAttr(hstmt, SQL_ATTR_IMP_PARAM_DESC, &hIpd, 0, 0);  
SQLSetDescField(hIpd, 1, SQL_DESC_NAME, "@quote", SQL_NTS);  
  
// Assuming that szQuote has been appropriately initialized,  
// execute.  
SQLExecute(hstmt);  
```
