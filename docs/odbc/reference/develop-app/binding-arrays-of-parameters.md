---
title: 繫結參數陣列 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- binding parameter arrays [ODBC]
- arrays of parameter values [ODBC]
- parameter arrays [ODBC]
ms.assetid: 037afe23-052d-4f3a-8aa7-45302b199ad0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 76f756b96a62a174e329614f9ab1baf634937522
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47636867"
---
# <a name="binding-arrays-of-parameters"></a>繫結參數陣列
使用參數陣列的應用程式會將陣列中的 SQL 陳述式的參數繫結。 有兩種繫結樣式：  
  
-   將陣列繫結至每個參數。 每個資料結構 （陣列） 包含單一參數的所有資料。 這就叫做*資料行取向的繫結*因為它繫結的資料行的單一參數的值。  
  
-   定義結構，以保存參數資料的一整組的參數，並繫結這些結構的陣列。 每個資料結構會包含單一的 SQL 陳述式的資料。 這就叫做*資料列取向的繫結*因為它繫結參數的資料列。  
  
 因為當應用程式會將單一的變數繫結至參數，它會呼叫**SQLBindParameter**繫結至參數的陣列。 唯一的差別是傳遞的位址陣列位址，不會進行單一變數位址。 應用程式設定 SQL_ATTR_PARAM_BIND_TYPE 陳述式屬性來指定它是否使用資料行取向的 （預設值） 或資料列取向的繫結。 是否要使用資料行取向或資料列取向的繫結就是大部分的應用程式喜好設定。 取決於處理器存取記憶體的方式，資料列取向的繫結可能會比較快。 不過，差異很可能就可以忽略除了非常大量的資料列的參數。  
  
## <a name="column-wise-binding"></a>資料行取向的繫結  
 當使用資料行取向的繫結，應用程式繫結一或兩個陣列至提供資料的每個參數。 第一個陣列保存資料值，而第二個陣列包含長度/指標緩衝區。 每個陣列包含有參數值的項目數。  
  
 資料行取向繫結預設值。 應用程式也可以從變更資料列取向的繫結至資料行取向的繫結藉由設定 SQL_ATTR_PARAM_BIND_TYPE 陳述式屬性。 下圖顯示如何以資料行繫結的運作方式。  
  
 ![示範如何資料行&#45;明智繫結運作](../../../odbc/reference/develop-app/media/pr31.gif "pr31")  
  
 比方說，下列程式碼會將 10 個元素陣列繫結至 PartID、 描述和價格資料行的參數和執行陳述式來插入 10 個資料列。 它會使用資料行取向的繫結。  
  
```  
#define DESC_LEN 51  
#define ARRAY_SIZE 10  
  
SQLCHAR *      Statement = "INSERT INTO Parts (PartID, Description,  Price) "  
                                                "VALUES (?, ?, ?)";  
SQLUINTEGER    PartIDArray[ARRAY_SIZE];  
SQLCHAR        DescArray[ARRAY_SIZE][DESC_LEN];  
SQLREAL        PriceArray[ARRAY_SIZE];  
SQLINTEGER     PartIDIndArray[ARRAY_SIZE], DescLenOrIndArray[ARRAY_SIZE],  
               PriceIndArray[ARRAY_SIZE];  
SQLUSMALLINT   i, ParamStatusArray[ARRAY_SIZE];  
SQLULEN ParamsProcessed;  
  
memset(DescLenOrIndArray, 0, sizeof(DescLenOrIndArray));  
memset(PartIDIndArray, 0, sizeof(PartIDIndArray));  
memset(PriceIndArray, 0, sizeof(PriceIndArray));  
  
// Set the SQL_ATTR_PARAM_BIND_TYPE statement attribute to use  
// column-wise binding.  
SQLSetStmtAttr(hstmt, SQL_ATTR_PARAM_BIND_TYPE, SQL_PARAM_BIND_BY_COLUMN, 0);  
  
// Specify the number of elements in each parameter array.  
SQLSetStmtAttr(hstmt, SQL_ATTR_PARAMSET_SIZE, ARRAY_SIZE, 0);  
  
// Specify an array in which to return the status of each set of  
// parameters.  
SQLSetStmtAttr(hstmt, SQL_ATTR_PARAM_STATUS_PTR, ParamStatusArray, 0);  
  
// Specify an SQLUINTEGER value in which to return the number of sets of  
// parameters processed.  
SQLSetStmtAttr(hstmt, SQL_ATTR_PARAMS_PROCESSED_PTR, &ParamsProcessed, 0);  
  
// Bind the parameters in column-wise fashion.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_ULONG, SQL_INTEGER, 5, 0,  
                  PartIDArray, 0, PartIDIndArray);  
SQLBindParameter(hstmt, 2, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, DESC_LEN - 1, 0,  
                  DescArray, DESC_LEN, DescLenOrIndArray);  
SQLBindParameter(hstmt, 3, SQL_PARAM_INPUT, SQL_C_FLOAT, SQL_REAL, 7, 0,  
                  PriceArray, 0, PriceIndArray);  
  
// Set part ID, description, and price.  
for (i = 0; i < ARRAY_SIZE; i++) {  
   GetNewValues(&PartIDArray[i], DescArray[i], &PriceArray[i]);  
   PartIDIndArray[i] = 0;  
   DescLenOrIndArray[i] = SQL_NTS;  
   PriceIndArray[i] = 0;  
}  
  
// Execute the statement.  
SQLExecDirect(hstmt, Statement, SQL_NTS);  
  
// Check to see which sets of parameters were processed successfully.  
for (i = 0; i < ParamsProcessed; i++) {  
   printf("Parameter Set  Status\n");  
   printf("-------------  -------------\n");  
   switch (ParamStatusArray[i]) {  
      case SQL_PARAM_SUCCESS:  
      case SQL_PARAM_SUCCESS_WITH_INFO:  
         printf("%13d  Success\n", i);  
         break;  
  
      case SQL_PARAM_ERROR:  
         printf("%13d  Error\n", i);  
         break;  
  
      case SQL_PARAM_UNUSED:  
         printf("%13d  Not processed\n", i);  
         break;  
  
      case SQL_PARAM_DIAG_UNAVAILABLE:  
         printf("%13d  Unknown\n", i);  
         break;  
  
   }  
}  
```  
  
## <a name="row-wise-binding"></a>資料列取向的繫結  
 當使用資料列取向的繫結，應用程式會定義每個參數集的結構。 此結構包含一個或兩個項目，每個參數。 第一個項目會保存參數值，而第二個元素會保留長度/指標緩衝區。 接著，應用程式配置這些結構的陣列，其中包含每個參數的值的項目數。  
  
 應用程式會宣告為 SQL_ATTR_PARAM_BIND_TYPE 陳述式屬性與驅動程式結構的大小。 應用程式可以繫結參數的位址陣列的第一個結構。 因此，驅動程式可以在其中計算特定資料列和資料行做為資料的位址  
  
```  
Address = Bound Address + ((Row Number - 1) * Structure Size) + Offset  
```  
  
 其中的資料列編號 1 的參數集的大小。 位移值，如果有定義，是指向 SQL_ATTR_PARAM_BIND_OFFSET_PTR 陳述式屬性的值。 下圖顯示如何以資料列繫結的運作方式。 參數可以放在結構中，依任何順序，但為了清楚起見的循序順序顯示。  
  
 ![如何顯示資料列&#45;明智繫結運作](../../../odbc/reference/develop-app/media/pr32.gif "pr32")  
  
 下列程式碼會建立結構，與要 PartID、 描述和價格資料行中儲存之值的項目。 然後配置這些結構的 10 個元素陣列，並將它繫結至 PartID、 描述和價格資料行，使用資料列取向的繫結的參數。 然後，它會執行陳述式來插入 10 個資料列。  
  
```  
#define DESC_LEN 51  
#define ARRAY_SIZE 10  
  
typedef tagPartStruct {  
   SQLREAL       Price;  
   SQLUINTEGER   PartID;  
   SQLCHAR       Desc[DESC_LEN];  
   SQLINTEGER    PriceInd;  
   SQLINTEGER    PartIDInd;  
   SQLINTEGER    DescLenOrInd;  
} PartStruct;  
  
PartStruct PartArray[ARRAY_SIZE];  
SQLCHAR *      Statement = "INSERT INTO Parts (PartID, Description,  
                Price) "  
               "VALUES (?, ?, ?)";  
SQLUSMALLINT   i, ParamStatusArray[ARRAY_SIZE];  
SQLULEN ParamsProcessed;  
  
// Set the SQL_ATTR_PARAM_BIND_TYPE statement attribute to use  
// column-wise binding.  
SQLSetStmtAttr(hstmt, SQL_ATTR_PARAM_BIND_TYPE, sizeof(PartStruct), 0);  
  
// Specify the number of elements in each parameter array.  
SQLSetStmtAttr(hstmt, SQL_ATTR_PARAMSET_SIZE, ARRAY_SIZE, 0);  
  
// Specify an array in which to return the status of each set of  
// parameters.  
SQLSetStmtAttr(hstmt, SQL_ATTR_PARAM_STATUS_PTR, ParamStatusArray, 0);  
  
// Specify an SQLUINTEGER value in which to return the number of sets of  
// parameters processed.  
SQLSetStmtAttr(hstmt, SQL_ATTR_PARAMS_PROCESSED_PTR, &ParamsProcessed, 0);  
  
// Bind the parameters in row-wise fashion.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_ULONG, SQL_INTEGER, 5, 0,  
                  &PartArray[0].PartID, 0, &PartArray[0].PartIDInd);  
SQLBindParameter(hstmt, 2, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, DESC_LEN - 1, 0,  
                  PartArray[0].Desc, DESC_LEN, &PartArray[0].DescLenOrInd);  
SQLBindParameter(hstmt, 3, SQL_PARAM_INPUT, SQL_C_FLOAT, SQL_REAL, 7, 0,  
                  &PartArray[0].Price, 0, &PartArray[0].PriceInd);  
  
// Set part ID, description, and price.  
for (i = 0; i < ARRAY_SIZE; i++) {  
   GetNewValues(&PartArray[i].PartID, PartArray[i].Desc, &PartArray[i].Price);  
   PartArray[0].PartIDInd = 0;  
   PartArray[0].DescLenOrInd = SQL_NTS;  
   PartArray[0].PriceInd = 0;  
}  
  
// Execute the statement.  
SQLExecDirect(hstmt, Statement, SQL_NTS);  
  
// Check to see which sets of parameters were processed successfully.  
for (i = 0; i < ParamsProcessed; i++) {  
   printf("Parameter Set  Status\n");  
   printf("-------------  -------------\n");  
   switch (ParamStatusArray[i]) {  
      case SQL_PARAM_SUCCESS:  
      case SQL_PARAM_SUCCESS_WITH_INFO:  
         printf("%13d  Success\n", i);  
         break;  
  
      case SQL_PARAM_ERROR:  
         printf("%13d  Error\n", i);  
         break;  
  
      case SQL_PARAM_UNUSED:  
         printf("%13d  Not processed\n", i);  
         break;  
  
      case SQL_PARAM_DIAG_UNAVAILABLE:  
         printf("%13d  Unknown\n", i);  
         break;  
  
   }  
```
