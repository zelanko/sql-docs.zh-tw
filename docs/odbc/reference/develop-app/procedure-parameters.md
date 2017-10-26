---
title: "程序參數 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- procedure parameters [ODBC]
ms.assetid: 54fd857e-d2cb-467d-bb72-121e67a8e88d
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 4cf4aa29c376ac600842804eb4b7e3b935fb049b
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="procedure-parameters"></a>程序參數
程序呼叫中的參數可以輸入、 輸入/輸出或輸出參數。 這是從所有其他 SQL 陳述式中，永遠是輸入的參數的參數不同。  
  
 輸入的參數用來將值傳送給程序。 例如，假設 Parts 資料表有 PartID、 描述和價格的資料行。 InsertPart 程序可能會在資料表中有每個資料行的輸入的參數。 例如：  
  
```  
{call InsertPart(?, ?, ?)}  
```  
  
 驅動程式不應修改的輸入緩衝區，直到內容**SQLExecDirect**或**SQLExecute**傳回 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR、 SQL_INVALID_HANDLE 或 sql_no_data 為止。 輸入緩衝區的內容不能修改時**SQLExecDirect**或**SQLExecute**傳回 SQL_NEED_DATA 或 SQL_STILL_EXECUTING。  
  
 輸入/輸出參數會用來將值傳送給程序，並從程序中擷取值。 做為輸入和輸出參數使用相同的參數通常會造成混淆，且應予以避免。 例如，假設程序接受訂單 ID，並傳回之客戶的 ID。 這可以使用單一輸入/輸出參數，定義：  
  
```  
{call GetCustID(?)}  
```  
  
 可能是較好的方式使用兩個參數： 訂單 ID 和輸出或輸入/輸出參數 客戶 id 的輸入的參數：  
  
```  
{call GetCustID(?, ?)}  
```  
  
 輸出參數會用來擷取程序傳回值，以及擷取程序引數; 的值傳回值的程序有時又稱為*函式*。 例如，假設**GetCustID**剛才所提到的程序會傳回值，指出是否能夠找出訂單。 在下列呼叫中，第一個參數是輸出參數用來擷取程序傳回值，第二個參數是用來指定順序識別碼中，輸入的參數，並第三個參數是輸出參數用來擷取客戶 ID:  
  
```  
{? = call GetCustID(?, ?)}  
```  
  
 驅動程式處理值的輸入和輸入/輸出參數，程序中的不方式不同於其他 SQL 陳述式中的輸入參數。 當執行陳述式時，它們會擷取變數的值繫結至這些參數，並將它們傳送到資料來源。  
  
 在執行陳述式之後，驅動程式中繫結至這些參數的變數會儲存傳回的值的輸入/輸出和輸出參數。 這些傳回之後已經提取的程序傳回的所有結果，直到設定，則不保證值和**SQLMoreResults**傳回 sql_no_data 為止。 如果執行陳述式會導致錯誤，則緩衝區輸入/輸出參數或輸出參數緩衝區的內容會是未定義。  
  
 應用程式呼叫**SQLProcedure**判斷程序是否有傳回值。 它會呼叫**SQLProcedureColumns**來判斷每個程序參數的型別 （傳回值、 輸入、 輸入/輸出或輸出）。

