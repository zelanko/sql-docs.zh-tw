---
title: 資料行大小、 十進位數字，傳輸八位元長度，顯示大小 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- display size of data types [ODBC]
- data types [ODBC], column size
- transfer octet length of data types [ODBC]
- size of data types [ODBC]
- data types [ODBC], display size
- decimal digits of data types [ODBC]
- data types [ODBC], decimal digits
- SQL data types [ODBC], column characteristics
- column size of data types [ODBC]
- data types [ODBC], transfer octet length
ms.assetid: 723107a1-be08-4ea3-a8c0-b2c45d38d1aa
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2ce63d73b21d7eee16d0b17100ff9c18cde265d6
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="column-size-decimal-digits-transfer-octet-length-and-display-size---odbc"></a>資料行大小、 十進位數字，傳送 8 位元長度和顯示大小-ODBC
資料類型的特性在於其資料行 （或參數） 的大小、 小數位數、 長度和顯示大小。 下列 ODBC 函數會傳回這些屬性中的 SQL 陳述式的參數或 SQL 資料型別上的資料來源。 每個 ODBC 函式會傳回一組不同的這些屬性，如下所示：  
  
-   **SQLDescribeCol**傳回的資料行描述的資料行的大小與小數位數。  
  
-   **SQLDescribeParam**傳回參數的參數，它會描述的大小與小數位數。 **SQLBindParameter** SQL 陳述式中設定參數的大小與小數位數的參數。  
  
-   目錄函數**SQLColumns**， **SQLProcedureColumns**，和**SQLGetTypeInfo**資料表、 結果集或程序參數中傳回資料行的屬性和資料來源中的資料類型類別目錄屬性。 **SQLColumns**傳回指定資料表 （例如基底資料表、 檢視或系統資料表） 中的資料行大小、 十進位數字和資料行長度。 **SQLProcedureColumns**程序中傳回的資料行大小、 十進位數字和資料行長度。 **SQLGetTypeInfo**傳回的資料來源上的最大資料行大小和 SQL 資料類型的最小和最大十進位數字。  
  
 資料行的這些函式傳回的值或參數的大小會對應至"precision"做為 ODBC 2 中定義。*x*。 不過，這些值這並不一定對應 SQL_DESC_PRECISION 或其他任何一個描述元欄位中傳回的值。 也適用於對應至"scale"做為 ODBC 2 中定義的十進位數字。*x*。 它不一定對應 SQL_DESC_SCALE 或其他任何一個描述元欄位，傳回的值，但來自不同的描述項欄位，依據該資料類型。 如需詳細資訊，請參閱[資料行大小](../../../odbc/reference/appendixes/column-size.md)和[十進位數字](../../../odbc/reference/appendixes/decimal-digits.md)。  
  
 同樣地，轉送八位元長度的值不是來自 SQL_DESC_LENGTH。 這些是來自的所有字元和二進位型別描述項欄位的 SQL_DESC_OCTET_LENGTH。 沒有任何保存這項資訊適用於其他類型的描述項欄位。  
  
 所有資料類型的顯示大小值對應至單一的描述項欄位，SQL_DESC_DISPLAY_SIZE 中的值。  
  
 描述項欄位描述結果集的特性。 描述項欄位不包含有效的值有關陳述式執行之前的資料。 資料行的值的大小，請十進位數字，並顯示所傳回的大小**SQLColumns**， **SQLProcedureColumns**，和**SQLGetTypeInfo**、 在其他另一方面，傳回在於資料來源的類別目錄的資料庫物件，例如資料表資料行和資料類型的特性。 同樣地，在結果集中， **SQLColAttribute**傳回的資料行大小、 十進位數字和傳輸八位元長度的資料行在資料來源; 這些值不一定是相同的 SQL_DESC_PRECISION SQL_ 中的值DESC_SCALE 和 SQL_DESC_OCTET_LENGTH 描述項欄位。  
  
 如需有關這些描述項欄位的詳細資訊，請參閱[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)。  
  
 相關主題：  
  
-   [資料行大小](../../../odbc/reference/appendixes/column-size.md)  
-   [小數位數](../../../odbc/reference/appendixes/decimal-digits.md)  
-   [傳輸八位元長度](../../../odbc/reference/appendixes/transfer-octet-length.md)  
-   [顯示大小](../../../odbc/reference/appendixes/display-size.md)
