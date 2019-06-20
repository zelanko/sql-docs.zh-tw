---
title: 資料緩衝區類型 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], buffers
- data buffers [ODBC], types
- buffers [ODBC], data
- C data types [ODBC], buffers
ms.assetid: 58bea3e9-d552-447f-b3ad-ce1dab213b72
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7e02d42d6d63608ccb70dc984e05ae11578d3160
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63049964"
---
# <a name="data-buffer-type"></a>資料緩衝區類型
應用程式所指定之緩衝區的 C 資料類型。 使用單一的變數，這會發生於應用程式會將變數配置。 使用泛用的記憶體-也就是記憶體所指的類型 void 的指標。 發生這種情況時應用程式轉換成特定類型的記憶體。 驅動程式會探索此類型有兩種：  
  
-   **資料緩衝區型別引數。** 用來傳送參數值和結果集資料，例如與繫結之緩衝區的緩衝區*TargetValuePtr*中**SQLBindCol**，通常會有相關聯的類型引數，例如*TargetType*中的引數**SQLBindCol**。 這個引數，在應用程式會將對應的 C 類型識別項傳遞至緩衝區的型別。 例如，在下列呼叫來**SQLBindCol**，值 SQL_C_TYPE_DATE 表示驅動程式可*日期*緩衝區是 SQL_DATE_STRUCT:  
  
    ```  
    SQL_DATE_STRUCT Date;  
    SQLINTEGER  DateInd;  
    SQLBindCol(hstmt, 1, SQL_C_TYPE_DATE, &Date, 0, &DateInd);  
    ```  
  
     如需型別識別項的詳細資訊，請參閱[ODBC 中的資料型別](../../../odbc/reference/develop-app/data-types-in-odbc.md)區段中，本節稍後的。  
  
-   **預先定義的類型。** 用來傳送和擷取選項或屬性，例如緩衝區的緩衝區所指向*InfoValuePtr*中的引數**SQLGetInfo**，具有固定的型別取決於指定的選項。 驅動程式會假設資料緩衝區是這種;是配置的緩衝區，此類型的應用程式的責任。 例如，在下列呼叫來**SQLGetInfo**，驅動程式會假設緩衝區是 32 位元整數，因為這是 SQL_STRING_FUNCTIONS 選項的要求：  
  
    ```  
    SQLUINTEGER StringFuncs;  
    SQLGetInfo(hdbc, SQL_STRING_FUNCTIONS, (SQLPOINTER) &StringFuncs, 0,  
                NULL);  
    ```  
  
 驅動程式會使用的 C 資料類型，來解譯緩衝區中的資料。
