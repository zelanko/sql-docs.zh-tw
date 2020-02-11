---
title: 取得冗長的資料 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 49f0023f726dd4bb290ffba1018ce2608800dd90
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68216365"
---
# <a name="getting-long-data"></a>取得長資料
Dbms 會將*長資料*定義為任何一種大小的字元或二進位資料，例如255個字元。 這項資料可能夠小，可以儲存在單一緩衝區中，例如數千個字元的部分描述。 不過，儲存在記憶體中的時間可能太長，例如長文字檔或點陣圖。 因為這類資料不能儲存在單一緩衝區中，所以它會在提取資料列中的其他資料之後，從具有**SQLGetData**的元件中的驅動程式中取出。  
  
> [!NOTE]  
>  應用程式實際上可以使用**SQLGetData**（而不只是長資料）來抓取任何類型的資料，雖然只有字元和二進位資料可以在部分中取得。 不過，如果資料夠小而足以容納在單一緩衝區中，通常就沒有使用**SQLGetData**的理由。 將緩衝區系結至資料行，並讓驅動程式傳回緩衝區中的資料更為容易。  
  
 若要從資料行取出長資料，應用程式會先呼叫**SQLFetchScroll**或**SQLFetch**來移至資料列，並提取系結資料行的資料。 然後，應用程式會呼叫**SQLGetData**。 **SQLGetData**具有與**SQLBindCol**相同的引數：語句控制碼;資料行編號;應用程式變數的 C 資料類型、位址和位元組長度;以及長度/指標緩衝區的位址。 這兩個函式都有相同的引數，因為它們基本上執行相同的工作：它們會將應用程式變數描述到驅動程式，並指定應該在該變數中傳回特定資料行的資料。 主要的差異在於**SQLGetData**是在提取資料列之後呼叫（這有時候也稱為*晚期繫結*），而且**SQLGetData**所指定的系結只會在呼叫期間持續。  
  
 就單一資料行而言， **SQLGetData**的行為就像**SQLFetch**：它會抓取資料行的資料，將它轉換成應用程式變數的型別，然後在該變數中傳回它。 它也會傳回長度/指標緩衝區中的資料位元組長度。 如需**SQLFetch**如何傳回資料的詳細資訊，請參閱[提取資料列](../../../odbc/reference/develop-app/fetching-a-row-of-data.md)。  
  
 **SQLGetData**與**SQLFetch**的差異在於一個重要的考慮。 如果針對相同的資料行連續呼叫多次，則每個呼叫都會傳回連續的資料部分。 除了最後一個呼叫以外的每個呼叫都會傳回 SQL_SUCCESS_WITH_INFO 和 SQLSTATE 01004 （字串資料，右邊已截斷）;最後一次呼叫會傳回 SQL_SUCCESS。 這是**SQLGetData**用來在元件中取出長資料的方式。 當沒有其他要傳回的資料時， **SQLGetData**會傳回 SQL_NO_DATA。 應用程式會負責將長資料放在一起，這可能表示串連資料的各個部分。 每個部分都是以 null 結束;如果串連元件，應用程式必須移除 null 終止字元。 您可以針對可變長度的書簽以及其他長資料，來取得元件中的資料。 在長度/指標緩衝區中傳回的值會隨著前一個呼叫中所傳回的位元組數而減少每次呼叫，不過，驅動程式通常無法探索可用資料量並傳回 SQL_NO_TOTAL 的位元組長度。 例如：  
  
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
  
 使用**SQLGetData**有幾項限制。 一般來說，使用**SQLGetData**存取的資料行：  
  
-   必須以增加的資料行編號順序來存取（因為結果集的資料行是從資料來源讀取的方式）。 例如，呼叫資料行5的**SQLGetData**是錯誤的，然後對資料行4呼叫它。  
  
-   無法系結。  
  
-   必須具有比最後一個系結資料行更高的資料行編號。 例如，如果最後一個系結的資料行是資料行3，則呼叫資料行2的**SQLGetData**是錯誤的。 基於這個理由，應用程式應該確保將長資料行放在選取清單的結尾。  
  
-   如果呼叫**SQLFetch**或**SQLFetchScroll**來抓取一個以上的資料列，就無法使用。 如需詳細資訊，請參閱[使用區塊資料指標](../../../odbc/reference/develop-app/using-block-cursors.md)。  
  
 某些驅動程式不會強制執行這些限制。 互通的應用程式應該假設它們存在，或使用 SQL_GETDATA_EXTENSIONS 選項呼叫**SQLGetInfo**來判斷不會強制執行的限制。  
  
 如果應用程式不需要字元或二進位資料行中的所有資料，可以在執行語句之前設定 SQL_ATTR_MAX_LENGTH 語句屬性，藉以減少以 DBMS 為基礎的驅動程式中的網路流量。 這會限制將針對任何字元或二進位資料行傳回的位元組數目。 例如，假設資料行包含長文字檔。 流覽包含此資料行之資料表的應用程式，可能只需要顯示每份檔的第一頁。 雖然此語句屬性可以在驅動程式中模擬，但是沒有理由這麼做。 特別是，如果應用程式想要截斷字元或二進位資料，它應該使用**SQLBindCol**將小型緩衝區系結至資料行，並讓驅動程式截斷資料。
