---
title: 使用 SQLBindCol |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], binding columns
- binding columns [ODBC]
- SQLBindCol function [ODBC], using
ms.assetid: 17277ab3-33ad-44d3-a81c-a26b5e338512
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2c26aff8220d2ebaf4024a881e8b48f165999f8f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47776406"
---
# <a name="using-sqlbindcol"></a>使用 SQLBindCol
藉由呼叫應用程式繫結的資料行**SQLBindCol**。 此函式會將一個資料行繫結一次。 有了它，應用程式則指定下列項目：  
  
-   資料行編號。 資料行 0 是書籤資料行中;此資料行不會納入一些結果集。 所有其他資料行編號從數字 1 開始。 它會多於可用資料行的結果集; 繫結的編號較高的資料行發生錯誤此錯誤無法偵測到之前已建立結果集，因此它由**SQLFetch**，而非**SQLBindCol**。  
  
-   C 資料類型、 位址和位元組長度的變數繫結至資料行。 它會指定 C 資料類型的資料行的 SQL 資料類型無法轉換; 發生錯誤此錯誤可能無法偵測之前已建立結果集，因此它由**SQLFetch**，而非**SQLBindCol**。 如需支援的轉換，請參閱[轉換將資料從 SQL 到 C 資料類型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)附錄 d： 資料型別中。 如需位元組長度的資訊，請參閱[的資料緩衝區長度](../../../odbc/reference/develop-app/data-buffer-length.md)。  
  
-   長度/指標緩衝區的位址。 長度/指標緩衝區是選擇性的。 它用來傳回二進位或字元資料或傳回 SQL_NULL_DATA 的位元組長度，如果資料為 NULL。 如需詳細資訊，請參閱 <<c0> [ 使用長度/指標值](../../../odbc/reference/develop-app/using-length-and-indicator-values.md)。  
  
 當**SQLBindCol**是呼叫，此驅動程式將這項資訊與陳述式。 會擷取每個資料列，它會使用資訊來將每個資料行的資料放在繫結的應用程式變數中。  
  
 例如，下列程式碼會繫結變數的銷售人員和 CustID 資料行。 資料行的資料將會傳回*SalesPerson*並*CustID*。 因為*業務員*是字元的緩衝區中，應用程式指定的位元組長度 (11)，好讓驅動程式可以判斷是否要截斷的資料。 傳回的位元組長度的連結，或者是否為 NULL，將會傳回*SalesPersonLenOrInd*。  
  
 因為*CustID*是一個整數變數，並有固定的長度，則不需要指定它的位元組長度; 驅動程式會假設它是**sizeof (** SQLUINTEGER **)**。 傳回的客戶的位元組長度識別碼的資料，或是否為 NULL，將會傳回*CustIDInd*。 請注意，應用程式想要只薪資是否為 NULL，因為永遠是位元組長度**sizeof (** SQLUINTEGER **)**。  
  
```  
SQLCHAR       SalesPerson[11];  
SQLUINTEGER   CustID;  
SQLINTEGER    SalesPersonLenOrInd, CustIDInd;  
SQLRETURN     rc;  
SQLHSTMT      hstmt;  
  
// Bind SalesPerson to the SalesPerson column and CustID to the   
// CustID column.  
SQLBindCol(hstmt, 1, SQL_C_CHAR, SalesPerson, sizeof(SalesPerson),  
            &SalesPersonLenOrInd);  
SQLBindCol(hstmt, 2, SQL_C_ULONG, &CustID, 0, &CustIDInd);  
  
// Execute a statement to get the sales person/customer of all orders.  
SQLExecDirect(hstmt, "SELECT SalesPerson, CustID FROM Orders ORDER BY SalesPerson",  
               SQL_NTS);  
  
// Fetch and print the data. Print "NULL" if the data is NULL. Code to   
// check if rc equals SQL_ERROR or SQL_SUCCESS_WITH_INFO not shown.  
while ((rc = SQLFetch(hstmt)) != SQL_NO_DATA) {  
   if (SalesPersonLenOrInd == SQL_NULL_DATA)   
            printf("NULL                     ");  
   else   
            printf("%10s   ", SalesPerson);  
   if (CustIDInd == SQL_NULL_DATA)   
         printf("NULL\n");  
   else   
            printf("%d\n", CustID);  
}  
  
// Close the cursor.  
SQLCloseCursor(hstmt);  
```  
  
 下列程式碼執行**選取**使用者輸入陳述式，並列印每個結果集內的資料列。 因為應用程式無法預測結果的圖形設定所建立**選取**陳述式，所以無法繫結硬式編碼的變數至結果集，如上述範例所示。 相反地，應用程式會保存資料的緩衝區和長度/指標緩衝區配置該資料列中的每一個資料行。 每個資料行，它會計算資料行的記憶體開頭的位移，並調整此位移為對齊界限上的資料行的資料和長度/指標緩衝區啟動。 然後，它繫結至資料行位移開始的記憶體。 從驅動程式的觀點來看，這個記憶體位址是區別繫結在上述範例中，變數的位址。 如需對齊的詳細資訊，請參閱[對齊](../../../odbc/reference/develop-app/alignment.md)。  
  
```  
// This application allocates a buffer at run time. For each column, this   
// buffer contains memory for the column's data and length/indicator.   
// For example:  
//      column 1         column 2      column 3      column 4  
// <------------><---------------><-----><------------>  
//      db1   li1   db2   li2   db3   li3   db4   li4  
//      |      |      |      |      |      |      |         |  
//      _____V_____V________V_______V___V___V______V_____V_  
// |__________|__|_____________|__|___|__|__________|__|  
//  
// dbn = data buffer for column n  
// lin = length/indicator buffer for column n  
  
// Define a macro to increase the size of a buffer so that it is a   
// multiple of the alignment size. Thus, if a buffer starts on an   
// alignment boundary, it will end just before the next alignment   
// boundary. In this example, an alignment size of 4 is used because   
// this is the size of the largest data type used in the application's   
// buffer--the size of an SDWORD and of the largest default C data type   
// are both 4. If a larger data type (such as _int64) was used, it would   
// be necessary to align for that size.  
#define ALIGNSIZE 4  
#define ALIGNBUF(Length) Length % ALIGNSIZE ? \  
                  Length + ALIGNSIZE - (Length % ALIGNSIZE) : Length  
  
SQLCHAR        SelectStmt[100];  
SQLSMALLINT    NumCols, *CTypeArray, i;  
SQLINTEGER *   ColLenArray, *OffsetArray, SQLType, *DataPtr;  
SQLRETURN      rc;   
SQLHSTMT       hstmt;  
  
// Get a SELECT statement from the user and execute it.  
GetSelectStmt(SelectStmt, 100);  
SQLExecDirect(hstmt, SelectStmt, SQL_NTS);  
  
// Determine the number of result set columns. Allocate arrays to hold   
// the C type, byte length, and buffer offset to the data.  
SQLNumResultCols(hstmt, &NumCols);  
CTypeArray = (SQLSMALLINT *) malloc(NumCols * sizeof(SQLSMALLINT));  
ColLenArray = (SQLINTEGER *) malloc(NumCols * sizeof(SQLINTEGER));  
OffsetArray = (SQLINTEGER *) malloc(NumCols * sizeof(SQLINTEGER));  
  
OffsetArray[0] = 0;  
for (i = 0; i < NumCols; i++) {  
   // Determine the column's SQL type. GetDefaultCType contains a switch   
   // statement that returns the default C type for each SQL type.  
   SQLColAttribute(hstmt, ((SQLUSMALLINT) i) + 1, SQL_DESC_TYPE, NULL, 0, NULL, (SQLPOINTER) &SQLType);  
   CTypeArray[i] = GetDefaultCType(SQLType);  
  
   // Determine the column's byte length. Calculate the offset in the   
   // buffer to the data as the offset to the previous column, plus the   
   // byte length of the previous column, plus the byte length of the   
   // previous column's length/indicator buffer. Note that the byte   
   // length of the column and the length/indicator buffer are increased   
   // so that, assuming they start on an alignment boundary, they will  
   // end on the byte before the next alignment boundary. Although this   
   // might leave some holes in the buffer, it is a relatively   
   // inexpensive way to guarantee alignment.  
   SQLColAttribute(hstmt, ((SQLUSMALLINT) i)+1, SQL_DESC_OCTET_LENGTH, NULL, 0, NULL, &ColLenArray[i]);  
   ColLenArray[i] = ALIGNBUF(ColLenArray[i]);  
   if (i)  
      OffsetArray[i] = OffsetArray[i-1]+ColLenArray[i-1]+ALIGNBUF(sizeof(SQLINTEGER));  
}  
  
// Allocate the data buffer. The size of the buffer is equal to the   
// offset to the data buffer for the final column, plus the byte length   
// of the data buffer and length/indicator buffer for the last column.  
void *DataPtr = malloc(OffsetArray[NumCols - 1] +  
               ColLenArray[NumCols - 1] + ALIGNBUF(sizeof(SQLINTEGER)));  
  
// For each column, bind the address in the buffer at the start of the   
// memory allocated for that column's data and the address at the start   
// of the memory allocated for that column's length/indicator buffer.  
for (i = 0; i < NumCols; i++)  
   SQLBindCol(hstmt,  
            ((SQLUSMALLINT) i) + 1,  
            CTypeArray[i],  
            (SQLPOINTER)((SQLCHAR *)DataPtr + OffsetArray[i]),  
            ColLenArray[i],  
            (SQLINTEGER *)((SQLCHAR *)DataPtr + OffsetArray[i] + ColLenArray[i]));  
  
// Retrieve and print each row. PrintData accepts a pointer to the data,   
// its C type, and its byte length/indicator. It contains a switch   
// statement that casts and prints the data according to its type. Code   
// to check if rc equals SQL_ERROR or SQL_SUCCESS_WITH_INFO not shown.  
while ((rc = SQLFetch(hstmt)) != SQL_NO_DATA) {  
   for (i = 0; i < NumCols; i++) {  
      PrintData((SQLCHAR *)DataPtr[OffsetArray[i]], CTypeArray[i],  
               (SQLINTEGER *)((SQLCHAR *)DataPtr[OffsetArray[i] + ColLenArray[i]]));  
   }  
}  
  
// Close the cursor.  
SQLCloseCursor(hstmt);  
```
