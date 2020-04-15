---
title: 使用 SQLBindCol |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294628"
---
# <a name="using-sqlbindcol"></a>使用 SQLBindCol
應用程式通過調用**SQLBindCol**來綁定列。 此函數一次綁定一列。 使用它,應用程式指定以下內容:  
  
-   資料行編號。 列 0 是書籤列;此列不包括在某些結果集中。 所有其他列都以數位 1 開頭編號。 綁定編號較高的列比結果集中的列綁定錯誤;在創建結果集之前無法檢測到此錯誤,因此**SQLFetch**而不是**SQLBindCol**會返回此錯誤。  
  
-   綁定到列的變數的 C 資料類型、位址和位元組長度。 指定無法轉換為列的 SQL 資料類型的 C 資料類型是錯誤的;在創建結果集之前可能無法檢測到此錯誤,因此**SQLFetch**而不是**SQLBindCol**會返回此錯誤。 有關支援的轉化清單,請參閱附錄 D:資料類型中[將資料從 SQL 轉換為 C 資料類型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。 有關位元組長度的資訊,請參閱[資料緩衝區長度](../../../odbc/reference/develop-app/data-buffer-length.md)。  
  
-   長度/指示器緩衝區的位址。 長度/指示器緩衝區是可選的。 它用於返回二進位或字元資料的位元組長度,或者如果資料為 NULL,則返回SQL_NULL_DATA。 關於詳細資訊,請參閱[使用長度/指標值](../../../odbc/reference/develop-app/using-length-and-indicator-values.md)。  
  
 調用**SQLBindCol**時,驅動程式將此資訊與語句關聯。 獲取每行數據時,它使用資訊將每列的數據放在綁定的應用程序變數中。  
  
 例如,以下代碼將變數綁定到 SalesPerson 和 CustID 列。 列的數據將在*SalesPerson*和*CustID 中*返回。 由於*SalesPerson*是一個字元緩衝區,因此應用程式指定其位元組長度 (11),以便驅動程式可以確定是否截截數據。 返回的標題的位元組長度或是否為 NULL 將在*SalesPersonLenOrInd 中*返回。  
  
 由於*CustID*是一個整數變數,並且具有固定長度,因此無需指定其位元組長度;驅動程式假定它是**大小**(SQLUINTEGER)。** ** 返回的客戶 ID 資料的位元組長度或是否為 NULL 將在*CustIDInd*中傳回。 請注意,應用程式只對工資是否為 NULL 感興趣,因為位元組長度始終**大小**(SQLUINTEGER)。** **  
  
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
  
 以下代碼執行使用者輸入的**SELECT**語句,並在結果集中列印每行數據。 由於應用程式無法預測由**SELECT**語句創建的結果集的形狀,因此無法像前面的示例中那樣將硬編碼變數綁定到結果集。 相反,應用程式分配一個緩衝區,該緩衝區保存該行中每一列的數據和長度/指示器緩衝區。 對於每列,它計算列記憶體開始的偏移量,並調整此偏移量,以便列的數據和長度/指示器緩衝區從對齊邊界開始。 然後,它將從偏移量開始的記憶體綁定到列。 從驅動程式的角度來看,此記憶體的位址與上述示例中綁定的變數的位址無法區分。 有關對齊的詳細資訊,請參閱[對齊](../../../odbc/reference/develop-app/alignment.md)。  
  
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
