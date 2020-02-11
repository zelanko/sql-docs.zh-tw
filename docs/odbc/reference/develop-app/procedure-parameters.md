---
title: 程式參數 |Microsoft Docs
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
ms.openlocfilehash: f85512a1686df26cad739dc906e49cc5499f62e7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67912306"
---
# <a name="procedure-parameters"></a>程序參數
程序呼叫中的參數可以是輸入、輸入/輸出或輸出參數。 這與所有其他 SQL 語句中的參數不同，它們一律是輸入參數。  
  
 輸入參數是用來將值傳送至程式。 例如，假設 [元件] 資料表具有 [PartID]、[描述] 和 [價格] 資料行。 InsertPart 程式可能會有資料表中每個資料行的輸入參數。 例如：  
  
```  
{call InsertPart(?, ?, ?)}  
```  
  
 在**SQLExecDirect**或**SQLExecute**傳回 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、SQL_INVALID_HANDLE 或 SQL_NO_DATA 之前，驅動程式不應修改輸入緩衝區的內容。 當**SQLExecDirect**或**SQLExecute**傳回 SQL_NEED_DATA 或 SQL_STILL_EXECUTING 時，不應修改輸入緩衝區的內容。  
  
 輸入/輸出參數可用來將值傳送至程式，並從程式中抓取值。 使用與輸入和輸出參數相同的參數，通常會造成混淆，應予以避免。 例如，假設某個程式接受訂單識別碼，並傳回客戶的識別碼。 這可以使用單一輸入/輸出參數來定義：  
  
```  
{call GetCustID(?)}  
```  
  
 使用兩個參數可能較好：訂單識別碼的輸入參數，以及客戶識別碼的輸出或輸入/輸出參數：  
  
```  
{call GetCustID(?, ?)}  
```  
  
 輸出參數是用來抓取程式傳回值，並從程式引數抓取值;傳回值的程式有時也稱為*函數*。 例如，假設剛才提到的**GetCustID**程式傳回一個值，指出它是否能夠找到訂單。 在下列呼叫中，第一個參數是用來取出程式傳回值的輸出參數，第二個參數是用來指定訂單識別碼的輸入參數，而第三個參數是用來抓取客戶識別碼的輸出參數：  
  
```  
{? = call GetCustID(?, ?)}  
```  
  
 驅動程式會處理常式中輸入和輸入/輸出參數的值，與其他 SQL 語句中的輸入參數不同。 執行語句時，它們會抓取系結至這些參數的變數值，並將它們傳送至資料來源。  
  
 在執行語句之後，驅動程式會在系結至這些參數的變數中儲存輸入/輸出和輸出參數的傳回值。 在提取程式所傳回的所有結果並**SQLMoreResults**傳回 SQL_NO_DATA 之後，才保證不會設定這些傳回的值。 如果執行語句導致錯誤，則輸入/輸出參數緩衝區或輸出參數緩衝區的內容會是未定義的。  
  
 應用程式會呼叫**SQLProcedure**來判斷程式是否有傳回值。 它會呼叫**SQLProcedureColumns**來判斷每個程式參數的類型（傳回值、輸入、輸入/輸出或輸出）。
