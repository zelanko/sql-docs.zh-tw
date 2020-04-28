---
title: 資料行大小、小數位數、傳輸八位長度、顯示大小 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 55b8e9dd305764a89601e9ffd5a337e42a8d8db3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306569"
---
# <a name="column-size-decimal-digits-transfer-octet-length-and-display-size---odbc"></a>資料行大小、小數位數、傳輸八位長度和顯示大小-ODBC
資料類型的特性是以其資料行（或參數）大小、小數位數、長度和顯示大小為特色。 下列 ODBC 函數會針對 SQL 語句中的參數或資料來源上的 SQL 資料類型傳回這些屬性。 每個 ODBC 函數都會傳回一組不同的屬性，如下所示：  
  
-   **SQLDescribeCol**會傳回它所描述之資料行的資料行大小和小數位數。  
  
-   **SQLDescribeParam**會傳回其所描述參數的參數大小和小數位數。 **SQLBindParameter**會在 SQL 語句中設定參數的參數大小和十進位數。  
  
-   目錄函數會**SQLColumns**、 **SQLProcedureColumns**和**SQLGetTypeInfo**傳回資料表中資料行的屬性、結果集或程式參數，以及資料來源中的資料類型目錄屬性。 **SQLColumns**會傳回指定資料表中資料行的資料行大小、小數位數和長度（例如基表、視圖或系統資料表）。 **SQLProcedureColumns**會傳回程序中資料行的資料行大小、小數位數和長度。 **SQLGetTypeInfo**會傳回資料來源上 SQL 資料類型的最大資料行大小和最小和最大十進位數。  
  
 這些函數針對資料行或參數大小所傳回的值，會對應至 ODBC 2 中定義的「精確度」。*x*。 不過，這些值不一定會對應到 SQL_DESC_PRECISION 或任何其他描述項欄位中所傳回的值。 這也適用于十進位數，其對應于 ODBC 2 中定義的「調整」。*x*。 這不一定會對應到 SQL_DESC_SCALE 或任何其他描述項欄位中所傳回的值，而是來自不同的描述項欄位，視資料類型而定。 如需詳細資訊，請參閱資料[行大小](../../../odbc/reference/appendixes/column-size.md)和[小數位數](../../../odbc/reference/appendixes/decimal-digits.md)。  
  
 同樣地，[傳輸八位長度] 的值不是來自 SQL_DESC_LENGTH。 它們來自所有字元和二進位類型之描述項的欄位 SQL_DESC_OCTET_LENGTH。 沒有任何描述元欄位可保存其他類型的這項資訊。  
  
 所有資料類型的顯示大小值都會對應至單一描述項欄位中的值，SQL_DESC_DISPLAY_SIZE。  
  
 描述項欄位說明結果集的特性。 描述項欄位在語句執行之前，不包含資料的有效值。 另一方面， **SQLColumns**、 **SQLProcedureColumns**和**SQLGetTypeInfo**所傳回之資料行大小、十進位數和顯示大小的值，會傳回存在於資料來源目錄中的資料庫物件（例如資料表資料行和資料類型）的特性。 同樣地，在其結果集內， **SQLColAttribute**會傳回資料來源的資料行大小、小數位數和傳輸八位長度。這些值不一定與 [SQL_DESC_PRECISION]、[SQL_DESC_SCALE] 和 [SQL_DESC_OCTET_LENGTH 描述項] 欄位中的值相同。  
  
 如需這些描述項欄位的詳細資訊，請參閱[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)。  
  
 相關主題：  
  
-   [資料行大小](../../../odbc/reference/appendixes/column-size.md)  
-   [小數位數](../../../odbc/reference/appendixes/decimal-digits.md)  
-   [傳輸八位元長度](../../../odbc/reference/appendixes/transfer-octet-length.md)  
-   [顯示大小](../../../odbc/reference/appendixes/display-size.md)
