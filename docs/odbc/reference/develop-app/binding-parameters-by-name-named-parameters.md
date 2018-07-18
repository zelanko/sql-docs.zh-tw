---
title: 繫結參數 （具名參數） 的名稱 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- named parameters [ODBC]
- binding parameters by name [ODBC]
ms.assetid: e2c3da5a-6c10-4dd5-acf9-e951eea71a6b
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 41e5c18119e8ec3482e6cddbdaee26bf10d6b1d0
ms.sourcegitcommit: fd9c33b93c886dcb00a48967b6c245631fd559bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/14/2018
ms.locfileid: "35619515"
---
# <a name="binding-parameters-by-name-named-parameters"></a>繫結參數 （具名參數） 的名稱
特定 Dbms 允許應用程式名稱而不是在程序呼叫中的位置來指定預存程序的參數。 這種參數稱為*具名參數*。 ODBC 支援具名參數的使用。 在 ODBC 中，具名的參數僅用於預存程序的呼叫，並不能用於其他 SQL 陳述式。  
  
 驅動程式會檢查以判斷是否名為使用參數 IPD 的 SQL_DESC_UNNAMED 欄位的值。 如果 SQL_DESC_UNNAMED 未設定為 sql_unnamed 時，驅動程式會使用在 IPD 的 SQL_DESC_NAME 欄位名稱來識別參數。 若要將參數繫結，應用程式可以呼叫**SQLBindParameter**至指定的參數資訊，然後可以呼叫**SQLSetDescField**要設定的 IPD SQL_DESC_NAME 欄位。 當使用具名的參數時，程序呼叫中參數的順序不重要，參數的記錄編號會被忽略。  
  
 未命名的參數與具名的參數之間的差異是中的描述元的記錄編號程序中的參數號碼之間的關聯性。 未命名的參數使用時，第一個參數標記是與相關參數描述元，與程序呼叫 （依建立順序） 的第一個參數中的第一個記錄。 當使用具名的參數時，第一個參數標記仍然相關參數描述項的第一個記錄，但已經不存在的描述元的記錄編號程序中的參數號碼之間的關聯性。 具名的參數程序的參數位置; 請勿使用描述項記錄的數字對應相反地，描述項記錄名稱會對應到程序參數名稱。  
  
> [!NOTE]  
>  如果已啟用自動母體擴展的 IPD，驅動程式將會填入描述項描述項記錄的順序會比對程序定義中，參數的順序，即使使用具名的參數。  
  
 如果使用具名的參數，所有參數必須被都具名參數。 如果任何參數不被具名的參數，沒有任何參數 ca 被具名參數。 如果有個具名的參數和未命名的參數的混合，行為是驅動程式而定。  
  
 為具名參數的範例，假設 SQL Server 預存程序定義，如下所示：  
  
```  
CREATE PROCEDURE test @title_id int = 1, @quote char(30) AS <blah>  
```  
  
 在此程序的第一個參數， @title_id，預設值為 1。 應用程式可以使用下列程式碼來叫用此程序，它會指定只有一個動態參數。 這個參數是具名的參數具有名稱"\@引號"。  
  
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
