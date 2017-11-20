---
title: "資料緩衝區類型 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data types [ODBC], buffers
- data buffers [ODBC], types
- buffers [ODBC], data
- C data types [ODBC], buffers
ms.assetid: 58bea3e9-d552-447f-b3ad-ce1dab213b72
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0c2ed3fb1d6a68737a894663e1b5c841d6cb1041
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="data-buffer-type"></a>資料緩衝區類型
應用程式所指定之緩衝區的 C 資料類型。 使用單一的變數，這發生在應用程式會將變數配置。 與一般記憶體 — 也就是記憶體所指向的類型 void 的指標，這發生在應用程式會轉換成特定類型的記憶體。 驅動程式會探索此類型有兩種：  
  
-   **資料緩衝區型別引數。** 用來傳送參數值和結果集資料，例如與繫結之緩衝區的緩衝區*TargetValuePtr*中**SQLBindCol**，通常會有相關聯的類型引數，例如*TargetType*引數中的**SQLBindCol**。 這個引數，應用程式會傳遞緩衝區的型別對應的 C 類型識別項。 例如，在下列呼叫**SQLBindCol**，值 SQL_C_TYPE_DATE 會告知驅動程式，在*日期*緩衝區是 SQL_DATE_STRUCT:  
  
    ```  
    SQL_DATE_STRUCT Date;  
    SQLINTEGER  DateInd;  
    SQLBindCol(hstmt, 1, SQL_C_TYPE_DATE, &Date, 0, &DateInd);  
    ```  
  
     如需類型識別項的詳細資訊，請參閱[ODBC 中的資料型別](../../../odbc/reference/develop-app/data-types-in-odbc.md)區段中的，於本節稍後。  
  
-   **預先定義的類型。** 用來傳送和擷取選項或屬性，例如緩衝區的緩衝區所指*InfoValuePtr*引數中的**SQLGetInfo**，具有固定的型別取決於指定的選項。 驅動程式會假設資料緩衝區是這種;負責應用程式的配置此類型的緩衝區。 例如，在下列呼叫**SQLGetInfo**，驅動程式會假設緩衝區是 32 位元整數，因為這是 SQL_STRING_FUNCTIONS 選項的需要：  
  
    ```  
    SQLUINTEGER StringFuncs;  
    SQLGetInfo(hdbc, SQL_STRING_FUNCTIONS, (SQLPOINTER) &StringFuncs, 0,  
                NULL);  
    ```  
  
 驅動程式使用的 C 資料類型，來解譯緩衝區中的資料。

