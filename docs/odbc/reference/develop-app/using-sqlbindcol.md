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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: da49ad4db80b93d02534a0c4ecacdc2621c9cf8d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81294628"
---
# <a name="using-sqlbindcol"></a>使用 SQLBindCol
應用程式會藉由呼叫**SQLBindCol**來系結資料行。 此函式會一次系結一個資料行。 使用它，應用程式會指定下列各項：  
  
-   資料行編號。 [資料行 0] 是書簽資料行;某些結果集不包含這個資料行。 所有其他資料行都是從數位1開始編號。 系結較高編號的資料行，而不是結果集中的資料行，這是一項錯誤。在建立結果集之前，無法偵測到此錯誤，因此它是由**SQLFetch**傳回，而不是**SQLBindCol**。  
  
-   系結至資料行之變數的 C 資料類型、位址和位元組長度。 若要指定 C 資料類型，而無法轉換資料行的 SQL 資料類型，就會發生錯誤。在建立結果集之前，可能不會偵測到此錯誤，因此它是由**SQLFetch**傳回，而不是**SQLBindCol**。 如需支援的轉換清單，請參閱附錄 D：資料類型中的[將資料從 SQL 轉換成 C 資料類型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。 如需位元組長度的相關資訊，請參閱[資料緩衝區長度](../../../odbc/reference/develop-app/data-buffer-length.md)。  
  
-   長度/指標緩衝區的位址。 長度/指標緩衝區是選擇性的。 它可用來傳回二進位或字元資料的位元組長度，或在資料為 Null 時傳回 SQL_Null_DATA。 如需詳細資訊，請參閱[使用長度/指標值](../../../odbc/reference/develop-app/using-length-and-indicator-values.md)。  
  
 呼叫**SQLBindCol**時，驅動程式會將此資訊與語句產生關聯。 提取每個資料列時，它會使用此資訊，將每個資料行的資料放在系結的應用程式變數中。  
  
 例如，下列程式碼會將變數系結至 [銷售人員] 和 [CustID] 資料行。 資料行將在*銷售人員*和*CustID*中傳回。 由於*銷售人員*是字元緩衝區，因此應用程式會指定其位元組長度（11），以便讓驅動程式判斷是否要截斷資料。 傳回之標題的位元組長度，或其是否為 Null，將會在*SalesPersonLenOrInd*中傳回。  
  
 因為*CustID*是整數變數而且具有固定長度，所以不需要指定它的位元組長度。驅動程式假設它是**sizeof （** SQLUINTEGER **）**。 傳回的客戶識別碼資料的位元組長度，或其是否為 Null，將會在*CustIDInd*中傳回。 請注意，應用程式只對薪資是否為 Null 感興趣，因為位元組長度一律為**sizeof （** SQLUINTEGER **）**。  
  
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
  
 下列程式碼會執行使用者所輸入的**SELECT**語句，並列印結果集中的每個資料列。 因為應用程式無法預測**SELECT**語句所建立之結果集的形狀，所以它無法將硬式編碼的變數系結至結果集，如先前範例所示。 相反地，應用程式會配置一個緩衝區，以保存該資料列中每個資料行的資料和長度/指標緩衝區。 針對每個資料行，它會計算資料行記憶體起始處的位移，並調整此位移，以便在對齊界限開始時，資料行的資料和長度/指標緩衝區。 然後，它會將從位移開始的記憶體系結至資料行。 從驅動程式的觀點來看，這個記憶體的位址與上述範例中系結之變數的位址是不區分的。 如需對齊的詳細資訊，請參閱[對齊](../../../odbc/reference/develop-app/alignment.md)。  
  
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
