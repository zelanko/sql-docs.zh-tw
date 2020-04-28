---
title: 系結參數陣列 |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 73cfcde89e89edb87a4955cf0854c66a01d81e6f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81283418"
---
# <a name="binding-arrays-of-parameters"></a>繫結參數陣列
使用參數陣列的應用程式會將陣列系結至 SQL 語句中的參數。 有兩種系結樣式：  
  
-   將陣列系結至每個參數。 每個資料結構（陣列）都會包含單一參數的所有資料。 這稱為「資料*行*取向系結」，因為它會系結單一參數值的資料行。  
  
-   定義結構來保存整個參數集的參數資料，並系結這些結構的陣列。 每個資料結構都會包含單一 SQL 語句的資料。 這稱為「資料*列*取向系結」，因為它會系結一列參數。  
  
 當應用程式將單一變數系結至參數時，它會呼叫**SQLBindParameter**來將陣列系結至參數。 唯一的差別在於傳遞的位址是陣列位址，而不是單一變數位址。 應用程式會設定 SQL_ATTR_PARAM_BIND_TYPE 語句屬性，以指定它使用的是資料行取向（預設值）還是資料列取向的系結。 是否要使用資料行取向或資料列取向的系結，主要是考慮應用程式的喜好設定。 視處理器存取記憶體的方式而定，資料列取向的系結可能會更快。 不過，除了非常大量的參數資料列之外，差異也可能是可忽略的。  
  
## <a name="column-wise-binding"></a>資料行取向的繫結  
 使用資料行取向系結時，應用程式會將一或兩個數組系結至要提供資料的每個參數。 第一個陣列會保存資料值，而第二個數組則保留長度/指標緩衝區。 每個陣列包含的元素數目與參數的值相同。  
  
 資料行取向系結是預設值。 應用程式也可以藉由設定 SQL_ATTR_PARAM_BIND_TYPE 語句屬性，從資料列取向的系結變更為資料行取向系結。 下圖顯示資料行取向系結的運作方式。  
  
 ![顯示資料行&#45;取向系結的運作方式](../../../odbc/reference/develop-app/media/pr31.gif "pr31")  
  
 例如，下列程式碼會將10個元素的陣列系結至 PartID、Description 和 Price 資料行的參數，並執行語句來插入10個數據列。 它會使用資料行取向的系結。  
  
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
 使用資料列取向的系結時，應用程式會為每個參數集定義一個結構。 結構會針對每個參數包含一或兩個元素。 第一個專案會保存參數值，而第二個元素會保存長度/指標緩衝區。 然後，應用程式會配置這些結構的陣列，其中包含的元素數目會與每個參數的值相同。  
  
 應用程式會使用 SQL_ATTR_PARAM_BIND_TYPE 語句屬性來宣告驅動程式的結構大小。 應用程式會將參數的位址系結到陣列的第一個結構。 因此，此驅動程式可以將特定資料列和資料行的資料位址計算為  
  
```  
Address = Bound Address + ((Row Number - 1) * Structure Size) + Offset  
```  
  
 其中，資料列的編號是從1到參數集的大小。 若已定義，則位移是 SQL_ATTR_PARAM_BIND_OFFSET_PTR 語句屬性所指向的值。 下圖顯示資料列取向系結的運作方式。 這些參數可以依任何順序放置在結構中，但會以順序顯示以供清楚。  
  
 ![顯示資料列&#45;取向系結的運作方式](../../../odbc/reference/develop-app/media/pr32.gif "pr32")  
  
 下列程式碼會針對要儲存在 PartID、Description 和 Price 資料行中的值，建立具有元素的結構。 然後，它會配置這些結構的10個元素陣列，並使用資料列取向的系結，將其系結至 PartID、Description 和 Price 資料行的參數。 然後，它會執行語句來插入10個數據列。  
  
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
