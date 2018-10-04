---
title: 取得長資料 |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: d61f6e2d5c2999a1ff7cea86d497eb4f0fb13244
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47849436"
---
# <a name="getting-long-data"></a>取得長資料
定義 Dbms*長資料*為任何字元或二進位資料超過特定大小，例如 255 個字元。 這項資料可能夠小，無法儲存在單一緩衝區，例如數個數千個字元的部分描述。 不過，它可能會太長而無法儲存在記憶體中，例如長文字文件或點陣圖。 因為這類資料無法儲存在單一緩衝區中，它會從使用組件中的驅動程式**SQLGetData**已經提取資料列中的其他資料之後。  
  
> [!NOTE]  
>  應用程式可以實際擷取資料的任何型別**SQLGetData**，不只是 long 資料，雖然組件中，則可以擷取只字元和二進位資料。 不過，如果資料夠小，無法放入單一緩衝區中，有通常是使用沒有理由**SQLGetData**。 就能輕鬆將緩衝區繫結至資料行，並讓傳回的資料緩衝區中的驅動程式。  
  
 若要從資料行擷取 long 資料，應用程式第一次呼叫**SQLFetchScroll**或是**SQLFetch**來移至資料列，並提取的資料繫結資料行。 接著，應用程式會呼叫**SQLGetData**。 **SQLGetData**具有相同的引數**SQLBindCol**： 陳述式控制代碼; 資料行編號; 應用程式變數; 的 C 資料類型、 位址和位元組長度和長度/指標緩衝區的位址。 這兩個函式會具有相同的引數，因為它們執行基本上相同的工作： 它們同時會描述應用程式變數到驅動程式並指定特定的資料行的資料應該會傳回該變數。 主要差異是， **SQLGetData**擷取的資料列之後，會呼叫 (和有時稱為*晚期繫結*基於這個理由) 及所指定的繫結**SQLGetData**生命週期僅限於在呼叫期間。  
  
 關於單一資料行**SQLGetData**行為都像是**SQLFetch**： 擷取資料行的資料、 將它轉換成變數的型別應用程式，並傳回該變數中。 它也會傳回長度/指標緩衝區中的資料的位元組長度。 如需有關如何**SQLFetch**傳回的資料，請參閱[擷取資料的資料列](../../../odbc/reference/develop-app/fetching-a-row-of-data.md)。  
  
 **SQLGetData**有別**SQLFetch**中重要的一點。 如果呼叫一次以上連續在相同的資料行，則每次呼叫會傳回連續資料的一部分。 除了最後一次呼叫的每個呼叫會傳回 SQL_SUCCESS_WITH_INFO 和 SQLSTATE 01004 （字串資料，右邊已截斷）;最後一次呼叫都會傳回 SQL_SUCCESS。 這是如何**SQLGetData**用來擷取部分的 long 資料。 若要傳回，沒有更多資料時**SQLGetData**傳回 sql_no_data 為止。 應用程式會負責將長資料放在一起，這可能表示串連的組件的資料。 每個部分是以 null 終止;應用程式必須移除 null 終止的字元，如果串連的組件。 擷取組件中的資料可以在進行可變長度的書籤也與其他的 long 資料。 雖然很常見的驅動程式無法探索可用的資料數量，並傳回 SQL_NO_TOTAL 位元組長度，長度/指標緩衝區會減少，每個呼叫中傳回的在前一個呼叫中，傳回的位元組數的值。 例如：  
  
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
  
 有幾項限制，使用**SQLGetData**。 一般而言，以存取資料行**SQLGetData**:  
  
-   必須遞增資料行數目 （因為從資料來源讀取的結果集資料行的方式） 的順序存取。 比方說，它會呼叫錯誤**SQLGetData** 5 的資料行，然後呼叫它的資料行 4。  
  
-   無法繫結。  
  
-   必須有較高的資料行數目，比最後一個繫結的資料行。 比方說，如果最後一個繫結的資料行是資料行 3，它會呼叫錯誤**SQLGetData**資料行 2。 基於這個理由，應用程式應該確定將長資料行放在選取清單的結尾。  
  
-   如果無法使用**SQLFetch**或是**SQLFetchScroll**呼叫來擷取多個資料列。 如需詳細資訊，請參閱 <<c0> [ 使用區塊資料指標](../../../odbc/reference/develop-app/using-block-cursors.md)。  
  
 有些驅動程式不會強制執行這些限制。 它們存在，或判斷不會藉由呼叫會強制執行的限制，互通的應用程式應該是假設**SQLGetInfo** SQL_GETDATA_EXTENSIONS 選項。  
  
 如果應用程式不需要在字元或二進位資料行中的所有資料，它可以減少網路流量，以 DBMS 為基礎的驅動程式中執行陳述式前，請先設定 SQL_ATTR_MAX_LENGTH 陳述式屬性。 這會限制的任何字元或二進位資料行就會傳回的資料位元組數目。 例如，假設資料行包含長文字文件。 瀏覽包含此資料行的資料表的應用程式可能需要顯示每份文件的第一頁。 雖然這個陳述式屬性可以模擬驅動程式中，沒有理由要執行這項操作。 特別是，如果應用程式想要截斷字元或二進位資料，所以應該繫結小型緩衝區的資料行**SQLBindCol** ，讓驅動程式會截斷資料。
