---
title: 列大小、十進位元、傳輸八點長度、顯示大小 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306569"
---
# <a name="column-size-decimal-digits-transfer-octet-length-and-display-size---odbc"></a>列大小、十進位數字、傳輸八點長度和顯示大小 - ODBC
數據類型的特徵是其列(或參數)大小、小數位數、長度和顯示大小。 以下 ODBC 函數傳回 SQL 語句中的參數或數據來源上的 SQL 資料類型的這些屬性。 每個 ODBC 函數傳回一組不同的這些屬性,如下所示:  
  
-   **SQLDescribeCol**傳回它描述的欄位大小和十進位數字。  
  
-   **SQLDescribeParam**傳回它描述的參數的參數大小和十進位數位。 **SQLBind參數**在 SQL 語句中設置參數的參數大小和十進位數位。  
  
-   目錄函數**SQLColumn、SQL****過程列**和**SQLGetTypeInfo**傳回表中列、結果集或過程參數和資料來源中資料類型的目錄屬性的屬性。 **SQLColumn**傳回指定表中(如基表、檢視或系統表)中的列大小、小數位數和長度。 **SQL程式列**返回過程中列的大小、小數位數和長度。 **SQLGetTypeInfo**傳回資料來源上 SQL 資料類型的最大列大小以及最小和最大十進位數字。  
  
 這些函數為列或參數大小返回的值對應於 ODBC 2 中定義的「精度」。*x*. . 但是,這些值不一定對應於SQL_DESC_PRECISION或任何其他描述符欄位中返回的值。 十進位數位也是如此,對應於 ODBC 2 中定義的「刻度」。*x*. . 它不一定對應於SQL_DESC_SCALE或任何其他描述符欄位中返回的值,但來自不同的描述符欄位,具體取決於數據類型。 有關詳細資訊,請參閱[列大小](../../../odbc/reference/appendixes/column-size.md)和[十進位數字](../../../odbc/reference/appendixes/decimal-digits.md)。  
  
 同樣,傳輸八位位元節長度的值不來自SQL_DESC_LENGTH。 它們來自所有字元和二進位類型的描述符欄位的SQL_DESC_OCTET_LENGTH。 沒有用於其他類型的此資訊的描述符位。  
  
 所有資料類型的顯示大小值對應於單個描述符欄位中的值,SQL_DESC_DISPLAY_SIZE。  
  
 描述字段描述結果集的特徵。 描述符欄位在語句執行之前不包含有關數據的有效值。 另一方面 **,SQLColumn、SQL****程式列**和**SQLGetTypeInfo**傳回的欄大小、小數位數和顯示大小的值返回資料來源目錄中存在的資料庫物件的特徵,如表列和資料類型。 同樣,在其結果集中 **,SQLColAttribute**返回數據源中的列大小、小數位數和傳輸八位位元組長度的列;這些值不一定與SQL_DESC_PRECISION、SQL_DESC_SCALE和SQL_DESC_OCTET_LENGTH描述符欄位中的值相同。  
  
 有關這些描述符位的詳細資訊,請參閱[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)。  
  
 相關主題：  
  
-   [資料行大小](../../../odbc/reference/appendixes/column-size.md)  
-   [小數位數](../../../odbc/reference/appendixes/decimal-digits.md)  
-   [傳輸八位元長度](../../../odbc/reference/appendixes/transfer-octet-length.md)  
-   [顯示大小](../../../odbc/reference/appendixes/display-size.md)
