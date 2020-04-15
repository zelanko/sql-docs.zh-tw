---
title: 取得長數據 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- long data [ODBC]
- fetches [ODBC], long data
- result sets [ODBC], fetching
- SQLGetData function [ODBC], getting long data
- retrieving long data [ODBC]
ms.assetid: 6ccb44bc-8695-4bad-91af-363ef22bdb85
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: da901c22eb26af063397b4af184179ebe5c75924
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298988"
---
# <a name="getting-long-data"></a>取得長資料
DBMS 將*長數據*定義為特定大小的任何字元或二進位數據,例如 255 個字元。 此數據可能足夠小,可以存儲在單個緩衝區中,例如幾千個字元的部件描述。 但是,存儲在記憶體中可能太長,例如長文本文檔或位圖。 由於此類數據不能存儲在單個緩衝區中,因此在提取行中的其他數據后,將從具有**SQLGetData**的部件中的驅動程式中檢索這些數據。  
  
> [!NOTE]  
>  應用程序實際上可以使用**SQLGetData**檢索任何類型的數據,而不僅僅是長數據,儘管只能分批檢索字元和二進位數據。 但是,如果數據足夠小,可以容納單個緩衝區,則通常沒有理由使用**SQLGetData**。 將緩衝區綁定到列並讓驅動程式返回緩衝區中的數據要容易得多。  
  
 若要從列檢索長數據,應用程式首先調用**SQLFetchScroll**或**SQLFetch**移至行並取得綁定欄資料。 然後,應用程式呼叫**SQLGetData**。 **SQLGetData**的參數與**SQLBindCol**相同:語句句柄;列號;應用程式變數的 C 資料類型、位址和位元組長度;和長度/指示器緩衝區的位址。 這兩個函數具有相同的參數,因為它們執行的任務基本相同:它們既向驅動程式描述應用程式變數,又指定應返回該變數中特定列的數據。 主要區別是 **,SQLGetData**是在獲取行後調用的(由於此原因有時稱為*後期綁定*),並且**SQLGetData**指定的綁定僅在調用期間持續。  
  
 對於單個列 **,SQLGetData**的行像**SQLFetch:** 它檢索列的數據,將其轉換為應用程式變數的類型,並在該變數中返回它。 它還返回長度/指示器緩衝區中數據的位元組長度。 有關**SQLFetch**如何傳回資料的詳細資訊,請參閱[取得一行資料](../../../odbc/reference/develop-app/fetching-a-row-of-data.md)。  
  
 **SQLGetData**在一個重要的方面與**SQLFetch**不同。 如果對同一列連續調用該列多次,則每個調用返回數據的連續部分。 除上次調用外,每個調用返回SQL_SUCCESS_WITH_INFO和 SQLSTATE 01004(字串數據,右截斷);最後一次調用返回SQL_SUCCESS。 這是**SQLGetData**用於檢索部分長數據的方式。 當沒有更多的數據返回時 **,SQLGetData**會返回SQL_NO_DATA。 應用程式負責將長數據放在一起,這可能意味著將數據部分串聯。 每個部件都是 null 終止的;因此,每個部件都為 null 終止。如果串聯零件,應用程式必須刪除 null 終止字元。 可以為可變長度書籤和其他長數據檢索零件中的數據。 長度/指示器緩衝區中返回的值按上一次調用中返回的位元組數減小,儘管驅動程式通常無法發現可用資料量並返回 SQL_NO_TOTAL位元長度。 例如：  
  
```  
// Declare a binary buffer to retrieve 5000 bytes of data at a time.  
SQLCHAR       BinaryPtr[5000];  
SQLUINTEGER   PartID;  
SQLINTEGER    PartIDInd, BinaryLenOrInd, NumBytes;  
SQLRETURN     rc;   
SQLHSTMT      hstmt;  
  
// Create a result set containing the ID and picture of each part.  
SQLExecDirect(hstmt, "SELECT PartID, Picture FROM Pictures", SQL_NTS);  
  
// Bind PartID to the PartID column.  
SQLBindCol(hstmt, 1, SQL_C_ULONG, &PartID, 0, &PartIDInd);  
  
// Retrieve and display each row of data.  
while ((rc = SQLFetch(hstmt)) != SQL_NO_DATA) {  
   // Display the part ID and initialize the picture.  
   DisplayID(PartID, PartIDInd);  
   InitPicture();  
  
   // Retrieve the picture data in parts. Send each part and the number   
   // of bytes in each part to a function that displays it. The number   
   // of bytes is always 5000 if there were more than 5000 bytes   
   // available to return (cbBinaryBuffer > 5000). Code to check if   
   // rc equals SQL_ERROR or SQL_SUCCESS_WITH_INFO not shown.  
   while ((rc = SQLGetData(hstmt, 2, SQL_C_BINARY, BinaryPtr, sizeof(BinaryPtr),  
                           &BinaryLenOrInd)) != SQL_NO_DATA) {  
      NumBytes = (BinaryLenOrInd > 5000) || (BinaryLenOrInd == SQL_NO_TOTAL) ?  
                  5000 : BinaryLenOrInd;  
      DisplayNextPictPart(BinaryPtr, NumBytes);  
   }  
}  
  
// Close the cursor.  
SQLCloseCursor(hstmt);  
```  
  
 使用**SQLGetData**有幾個限制。 通常,使用**SQLGetData**存取的欄:  
  
-   必須按增加列數的順序進行訪問(因為從數據源讀取結果集的列的方式)。 例如,為第 5 列調用**SQLGetData,** 然後為列 4 調用它是一個錯誤。  
  
-   無法綁定。  
  
-   列號必須高於最後一個綁定列。 例如,如果最後一個綁定列是列 3,則為列 2 調用**SQLGetData**是錯誤的。 因此,應用程式應確保在選擇清單的末尾放置長數據列。  
  
-   如果調用**SQLFetch**或**SQLFetchScroll**來檢索多行,則無法使用。 有關詳細資訊,請參閱[使用區塊游標](../../../odbc/reference/develop-app/using-block-cursors.md)。  
  
 某些驅動程式不強制執行這些限制。 可互通的應用程式應假定它們存在,或者透過使用SQL_GETDATA_EXTENSIONS選項調用**SQLGetInfo**來確定不強制實施哪些限制。  
  
 如果應用程式不需要字元或二進位資料列中的所有資料,則可以在執行語句之前設置SQL_ATTR_MAX_LENGTH語句屬性,從而減少基於 DBMS 的驅動程式中的網路流量。 這將限制將返回任何字元或二進位數字的資料位元組數。 例如,假設一列包含長文本文檔。 瀏覽包含此列的表的應用程式可能必須僅顯示每個文檔的第一頁。 儘管可以在驅動程式中類比此語句屬性,但沒有理由執行此操作。 特別是,如果應用程式想要截截字元或二進位數據,它應該使用**SQLBindCol**將小緩衝區綁定到列,並讓驅動程式截截數據。
