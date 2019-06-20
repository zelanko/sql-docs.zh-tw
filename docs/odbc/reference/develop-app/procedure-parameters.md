---
title: 程序參數 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- procedure parameters [ODBC]
ms.assetid: 54fd857e-d2cb-467d-bb72-121e67a8e88d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1cab0fea9c39e4946122698f2476668464e556c1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62861528"
---
# <a name="procedure-parameters"></a>程序參數
程序呼叫中的參數可以輸入、 輸入/輸出或輸出參數。 這是從所有其他 SQL 陳述式，其一律為輸入的參數中的參數不同。  
  
 輸入的參數用來將值傳送給程序。 例如，假設 Parts 資料表有 PartID、 描述和價格資料行。 InsertPart 程序可能會具有資料表中的每個資料行的輸入的參數。 例如：  
  
```  
{call InsertPart(?, ?, ?)}  
```  
  
 驅動程式不應該修改的輸入緩衝區，直到內容**SQLExecDirect**或是**SQLExecute**函數傳回 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR、 SQL_INVALID_HANDLE 或 sql_no_data 為止。 輸入緩衝區的內容不能修改時**SQLExecDirect**或是**SQLExecute**傳回 SQL_NEED_DATA 或 SQL_STILL_EXECUTING。  
  
 輸入/輸出參數會用來將值傳送給程序和擷取程序中的值。 做為輸入和輸出參數使用相同的參數通常會造成混淆，應予以避免。 例如，假設程序接受訂單 ID，並傳回客戶識別碼。 這可以定義具有單一輸入/輸出參數：  
  
```  
{call GetCustID(?)}  
```  
  
 最好是使用兩個參數： 訂單 ID 和輸出或客戶識別碼的輸入/輸出參數的輸入的參數：  
  
```  
{call GetCustID(?, ?)}  
```  
  
 輸出參數用來擷取程序傳回值，以及擷取程序引數; 的值傳回值的程序有時稱為*函式*。 例如，假設**GetCustID**剛剛提到的程序傳回值，這個值表示是否能夠找出訂單。 在下列呼叫中，第一個參數是用來擷取程序傳回值為輸出參數、 第二個參數是用來指定順序識別碼中，輸入的參數，和第三個參數是用來擷取客戶識別碼的輸出參數：  
  
```  
{? = call GetCustID(?, ?)}  
```  
  
 驅動程式處理輸入的值和輸入/輸出參數，程序中的不方式不同於其他 SQL 陳述式中的輸入參數。 當執行陳述式時，它們會擷取變數的值繫結到這些參數，並將它們傳送至資料來源。  
  
 在執行陳述式之後，驅動程式中繫結到這些參數的變數會儲存傳回的值的輸入/輸出和輸出參數。 這些傳回值並非保證值之後已經提取的程序所傳回的所有結果，直到設定並**SQLMoreResults**傳回 sql_no_data 為止。 如果執行陳述式會產生錯誤，是未定義的輸入/輸出參數緩衝區或輸出參數緩衝區的內容。  
  
 應用程式呼叫**SQLProcedure**判斷程序是否具有傳回值。 它會呼叫**SQLProcedureColumns**來判斷每個程序參數的型別 （傳回值、 輸入、 輸入/輸出或輸出）。
