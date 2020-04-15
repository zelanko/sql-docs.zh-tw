---
title: 過程參數 |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 35d43ca7cf6e603d7dabca9eacf1e026daa753b7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306952"
---
# <a name="procedure-parameters"></a>程序參數
過程呼叫中的參數可以是輸入、輸入/輸出或輸出參數。 這與所有其他 SQL 語句中的參數不同,後者始終是輸入參數。  
  
 輸入參數用於將值發送到過程。 例如,假設「零件」表具有「零件ID」、「說明」和「價格」列。 InsertPart 過程可能具有表中每列的輸入參數。 例如：  
  
```  
{call InsertPart(?, ?, ?)}  
```  
  
 在**SQLExecDirect**或**SQLExecute**返回SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、SQL_INVALID_HANDLE或SQL_NO_DATA之前,驅動程式不應修改輸入緩衝區的內容。 當**SQLExecDirect**或**SQLExecute**返回SQL_NEED_DATA或SQL_STILL_EXECUTING時,不應修改輸入緩衝區的內容。  
  
 輸入/輸出參數既用於將值發送到過程,又從過程檢索值。 使用與輸入和輸出參數相同的參數往往令人困惑,應避免使用。 例如,假設過程接受訂單 ID 並返回客戶的 ID。 這可以透過單一輸入/輸出參數進行定義:  
  
```  
{call GetCustID(?)}  
```  
  
 將使用兩個參數:訂單 ID 的輸入參數和客戶 ID 的輸出或輸入 / 輸出參數:  
  
```  
{call GetCustID(?, ?)}  
```  
  
 輸出參數用於檢索過程返回值並從過程參數中檢索值;傳回值的過程有時稱為*函數*。 例如,假設剛才提到的**GetCustID**過程返回一個值,指示它是否能夠找到訂單。 在以下調用中,第一個參數是用於檢索過程傳回值的輸出參數,第二個參數是用於指定訂單 ID 的輸入參數,第三個參數是用於檢索客戶 ID 的輸出參數:  
  
```  
{? = call GetCustID(?, ?)}  
```  
  
 驅動程式處理過程中輸入和輸入/輸出參數的值與其他 SQL 語句中的輸入參數不一樣。 執行語句時,它們會檢索綁定到這些參數的變數的值,並將它們發送到數據源。  
  
 執行語句後,驅動程式將輸入/輸出參數的返回值存儲在綁定到這些參數的變數中。 在提取過程返回的所有結果並返回**SQLMore 結果**SQL_NO_DATA之前,不保證對這些返回的值進行設置。 如果執行語句會導致錯誤,則輸入/輸出參數緩衝區或輸出參數緩衝區的內容將未定義。  
  
 應用程式呼叫**SQL 程式**以確定過程是否具有返回值。 它調用**SQL 過程列**以確定每個過程參數的類型(傳回值、輸入、輸入/輸出或輸出)。
