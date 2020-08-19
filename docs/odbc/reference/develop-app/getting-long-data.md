---
description: 取得長資料
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c3a40bc3f4f65f747776d747d79868340de06f53
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429280"
---
# <a name="getting-long-data"></a>取得長資料
Dbms 將 *長資料* 定義為特定大小的任何字元或二進位資料，例如255個字元。 這項資料可能小到足以儲存在單一緩衝區中，例如數千個字元的部分描述。 不過，儲存在記憶體中的時間可能太長，例如長文字檔或點陣圖。 由於這類資料無法儲存在單一緩衝區中，因此在提取資料列中的其他資料之後，會從具有 **SQLGetData** 元件的驅動程式取出。  
  
> [!NOTE]  
>  應用程式實際上可以使用 **SQLGetData**（而不只是 long 資料）抓取任何類型的資料，雖然只有字元和二進位資料可以在部分中取得。 但是，如果資料夠小而足以容納在單一緩衝區中，則通常沒有理由使用 **SQLGetData**。 將緩衝區系結至資料行更容易，並讓驅動程式傳回緩衝區中的資料。  
  
 若要從資料行取出較長的資料，應用程式會先呼叫 **SQLFetchScroll** 或 **SQLFetch** 來移至資料列，並提取系結資料行的資料。 然後，應用程式會呼叫 **SQLGetData**。 **SQLGetData** 具有與 **SQLBindCol**相同的引數：語句控制碼;資料行編號;應用程式變數的 C 資料類型、位址和位元組長度;以及長度/指標緩衝區的位址。 這兩個函式都有相同的引數，因為它們基本上會執行相同的工作：它們都會描述驅動程式的應用程式變數，並指定應該在該變數中傳回特定資料行的資料。 主要的差異在於， **SQLGetData** 會在提取資料列之後呼叫 (而且有時也稱為 *晚期繫結* ，因為這是) ，而且 **SQLGetData** 指定的系結只會在呼叫期間持續。  
  
 關於單一資料行， **SQLGetData** 的行為類似 **SQLFetch**：它會抓取資料行的資料、將資料轉換為應用程式變數的類型，並將它傳回至該變數。 它也會傳回長度/指標緩衝區中資料的位元組長度。 如需 **SQLFetch** 如何傳回資料的詳細資訊，請參閱 [提取資料列](../../../odbc/reference/develop-app/fetching-a-row-of-data.md)。  
  
 **SQLGetData** 與 **SQLFetch** 在一個重要方面不同。 如果針對相同的資料行連續呼叫一次以上，每個呼叫都會傳回資料的連續部分。 除了最後一個呼叫之外，每個呼叫都會傳回 SQL_SUCCESS_WITH_INFO 和 SQLSTATE 01004 (字串資料，右邊的截斷) ;最後一個呼叫會傳回 SQL_SUCCESS。 這是使用 **SQLGetData** 來取出元件中長資料的方式。 當不再有要傳回的資料時， **SQLGetData** 會傳回 SQL_NO_DATA。 應用程式會負責將長的資料放在一起，這可能表示串連資料的部分。 每個元件都是以 null 結束;如果串連元件，應用程式必須移除 null 終止字元。 您可以針對可變長度的書簽以及其他長的資料，來取得元件中的資料。 在長度/指標緩衝區中傳回的值會在每次呼叫中減少前一個呼叫中傳回的位元組數目，但驅動程式通常會無法探索可用的資料量，並傳回 SQL_NO_TOTAL 的位元組長度。 例如：  
  
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
  
 使用 **SQLGetData**有幾項限制。 一般來說，使用 **SQLGetData**存取的資料行：  
  
-   因為結果集的資料行是從資料來源) 中讀取，所以必須以增加資料行編號 (的順序來存取。 例如，針對第5欄呼叫 **SQLGetData** 是錯誤的，然後對資料行4呼叫它。  
  
-   無法系結。  
  
-   的資料行數目必須大於最後一個系結資料行。 例如，如果最後一個系結資料行是資料行3，則呼叫資料行2的 **SQLGetData** 是錯誤的。 基於這個理由，應用程式應該要確定在選取清單的結尾放置長的資料行。  
  
-   如果呼叫 **SQLFetch** 或 **SQLFetchScroll** 來抓取一個以上的資料列，就無法使用。 如需詳細資訊，請參閱 [使用區塊資料指標](../../../odbc/reference/develop-app/using-block-cursors.md)。  
  
 某些驅動程式不會強制執行這些限制。 互通的應用程式應該假設它們存在，或透過 SQL_GETDATA_EXTENSIONS 選項呼叫 **SQLGetInfo** ，來判斷不會強制執行哪些限制。  
  
 如果應用程式不需要字元或二進位資料行中的所有資料，則可以在執行語句之前設定 SQL_ATTR_MAX_LENGTH 語句屬性，藉以減少 DBMS 驅動程式中的網路流量。 這會限制將針對任何字元或二進位資料行傳回的資料位元組數目。 例如，假設某個資料行包含長文字檔。 流覽包含此資料行之資料表的應用程式，可能必須只顯示每份檔的第一頁。 雖然此語句屬性可以在驅動程式中模擬，但沒有理由這麼做。 尤其是，如果應用程式想要截斷字元或二進位資料，則應該使用 **SQLBindCol** 將小型緩衝區系結至資料行，並讓驅動程式截斷資料。
