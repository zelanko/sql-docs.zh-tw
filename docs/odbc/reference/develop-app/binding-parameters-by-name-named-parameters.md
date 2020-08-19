---
description: 依名稱繫結參數 (具名參數)
title: 依名稱 (具名引數將參數系結) |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 75227b26b5f9f060089e6568e233d327e3f7faa7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476840"
---
# <a name="binding-parameters-by-name-named-parameters"></a>依名稱繫結參數 (具名參數)
某些 Dbms 可讓應用程式依名稱指定預存程式的參數，而不是依照程序呼叫中的位置。 這類參數稱為「 *具名引數*」。 ODBC 支援使用具名引數。 在 ODBC 中，具名引數只會用於預存程式的呼叫，且不能在其他 SQL 語句中使用。  
  
 驅動程式會檢查 IPD 的 SQL_DESC_UNNAMED 欄位值，以判斷是否使用具名引數。 如果 SQL_DESC_UNNAMED 未設定為 SQL_UNNAMED，驅動程式會使用 IPD 的 SQL_DESC_NAME 欄位中的名稱來識別參數。 若要系結參數，應用程式可以呼叫 **SQLBindParameter** 來指定參數資訊，然後可以呼叫 **SQLSETDESCFIELD** 來設定 IPD 的 SQL_DESC_NAME 欄位。 使用具名引數時，程序呼叫中參數的順序並不重要，而且會忽略參數的記錄號碼。  
  
 未具名引數和具名引數之間的差異在於描述項的記錄號碼與程式中參數編號之間的關聯性。 使用未命名的參數時，第一個參數標記會與參數描述項中的第一筆記錄相關，而後者則是在程序呼叫中) 建立順序 (的第一個參數。 使用具名引數時，第一個參數標記仍會與參數描述項的第一筆記錄相關，但描述項的記錄號碼與程式中的參數編號之間的關聯性則不再存在。 具名引數不會使用描述項記錄號碼與程式參數位置的對應;相反地，描述項記錄名稱會對應至程式參數名稱。  
  
> [!NOTE]  
>  如果自動填入 IPD，驅動程式將會填入描述項，使描述項記錄的順序符合程序定義中參數的順序，即使使用了具名引數也是如此。  
  
 如果使用了具名引數，所有參數都必須是具名引數。 如果有任何參數不是具名引數，則沒有任何參數命名為參數。 如果有混合的具名引數和未命名的參數，行為會與驅動程式相依。  
  
 作為具名引數的範例，假設已定義 SQL Server 預存程式，如下所示：  
  
```  
CREATE PROCEDURE test @title_id int = 1, @quote char(30) AS <blah>  
```  
  
 在此程式中，第一個參數的 @title_id 預設值為1。 應用程式可以使用下列程式碼來叫用此程式，使其只指定一個動態參數。 此參數是名為 "quote" 的具名引數 \@ 。  
  
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
