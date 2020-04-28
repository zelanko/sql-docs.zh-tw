---
title: 配置和釋放緩衝區 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- buffers [ODBC], allocating and freeing
- allocating buffers [ODBC]
- freeing buffers [ODBC]
ms.assetid: 886bc9ed-39d4-43d2-82ff-aebc35b14d39
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e6aab888d24fcbc987b3db921436f14812618519
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81288398"
---
# <a name="allocating-and-freeing-buffers"></a>配置及釋放緩衝區
所有緩衝區都是由應用程式所配置和釋放。 如果緩衝區未延後，只需要在函式的呼叫期間存在。 例如， **SQLGetInfo**會傳回與*InfoValuePtr*引數所指向之緩衝區中特定選項相關聯的值。 這個緩衝區可以在呼叫**SQLGetInfo**之後立即釋放，如下列程式碼範例所示：  
  
```  
SQLSMALLINT   InfoValueLen;  
SQLCHAR *     InfoValuePtr = malloc(50);   // Allocate InfoValuePtr.  
  
SQLGetInfo(hdbc, SQL_DBMS_NAME, (SQLPOINTER)InfoValuePtr, 50,  
            &InfoValueLen);  
  
free(InfoValuePtr);                        // OK to free InfoValuePtr.  
```  
  
 因為延遲的緩衝區是在一個函式中指定，並用於另一個函數中，所以它是應用程式設計錯誤，可在驅動程式仍預期它存在時釋放延遲的緩衝區。 例如， \* *valueptr 是*緩衝區的位址會傳遞至**SQLBindCol** ，供**SQLFetch**稍後使用。 在資料行解除系結之前，無法釋放這個緩衝區，例如呼叫**SQLBindCol**或**SQLFreeStmt** ，如下列程式碼範例所示：  
  
```  
SQLRETURN    rc;  
SQLINTEGER   ValueLenOrInd;  
SQLHSTMT     hstmt;  
  
// Allocate ValuePtr  
SQLCHAR * ValuePtr = malloc(50);  
  
// Bind ValuePtr to column 1. It is an error to free ValuePtr here.  
SQLBindCol(hstmt, 1, SQL_C_CHAR, ValuePtr, 50, &ValueLenOrInd);  
  
// Fetch each row of data and place the value for column 1 in *ValuePtr.  
// Code to check if rc equals SQL_ERROR or SQL_SUCCESS_WITH_INFO   
// not shown.  
while ((rc = SQLFetch(hstmt)) != SQL_NO_DATA) {  
   // It is an error to free ValuePtr here.  
}  
  
// Unbind ValuePtr from column 1.  It is now OK to free ValuePtr.  
SQLFreeStmt(hstmt, SQL_UNBIND);  
free(ValuePtr);  
```  
  
 這類錯誤很容易透過在函式的本機宣告緩衝區來完成：當應用程式離開函數時，就會釋放緩衝區。 例如，下列程式碼會導致驅動程式中未定義且可能出現嚴重的行為：  
  
```  
SQLRETURN   rc;  
SQLHSTMT    hstmt;  
  
BindAColumn(hstmt);  
  
// Fetch each row of data and try to place the value for column 1 in  
// *ValuePtr. Because ValuePtr has been freed, the behavior is undefined  
// and probably fatal. Code to check if rc equals SQL_ERROR or   
// SQL_SUCCESS_WITH_INFO not shown.  
while ((rc = SQLFetch(hstmt)) != SQL_NO_DATA) {}  
  
   .  
   .  
   .  
  
void BindAColumn(SQLHSTMT hstmt)  // WARNING! This function won't work!  
{  
   // Declare ValuePtr locally.  
   SQLCHAR      ValuePtr[50];  
   SQLINTEGER   ValueLenOrInd;  
  
   // Bind rgbValue to column.  
   SQLBindCol(hstmt, 1, SQL_C_CHAR, ValuePtr, sizeof(ValuePtr),  
               &ValueLenOrInd);  
  
   // ValuePtr is freed when BindAColumn exits.  
}  
```
