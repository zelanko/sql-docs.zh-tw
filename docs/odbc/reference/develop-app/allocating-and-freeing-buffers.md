---
description: 配置及釋放緩衝區
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
ms.openlocfilehash: 629c613e8c0aba4675b2b95c9c9ccd82fb7cdfb6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429470"
---
# <a name="allocating-and-freeing-buffers"></a>配置及釋放緩衝區
所有緩衝區都是由應用程式佈建及釋放。 如果緩衝區不會延後，它只需要存在於呼叫函式的持續時間。 例如， **SQLGetInfo** 會傳回與 *InfoValuePtr* 引數所指向之緩衝區中特定選項相關聯的值。 這個緩衝區可以在呼叫 **SQLGetInfo**之後立即釋放，如下列程式碼範例所示：  
  
```  
SQLSMALLINT   InfoValueLen;  
SQLCHAR *     InfoValuePtr = malloc(50);   // Allocate InfoValuePtr.  
  
SQLGetInfo(hdbc, SQL_DBMS_NAME, (SQLPOINTER)InfoValuePtr, 50,  
            &InfoValueLen);  
  
free(InfoValuePtr);                        // OK to free InfoValuePtr.  
```  
  
 因為延遲的緩衝區是在一個函式中指定，並且在另一個函式中使用，所以它是應用程式設計錯誤，可在驅動程式仍預期存在時釋放延遲的緩衝區。 例如， \* *ValuePtr*緩衝區的位址會傳遞至**SQLBindCol** ，以便稍後供**SQLFetch**使用。 在解除系結資料行之前，無法釋放這個緩衝區，例如呼叫 **SQLBindCol** 或 **SQLFreeStmt** ，如下列程式碼範例所示：  
  
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
  
 藉由在函式的本機宣告緩衝區，即可輕鬆地建立這類錯誤。當應用程式離開函式時，就會釋放緩衝區。 例如，下列程式碼會在驅動程式中導致未定義且可能有嚴重的行為：  
  
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
