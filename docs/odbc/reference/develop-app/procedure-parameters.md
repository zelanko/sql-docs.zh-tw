---
description: 程序參數
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b21780cc4a6670c76e60daa69cf7933b4182b44e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465720"
---
# <a name="procedure-parameters"></a>程序參數
程序呼叫中的參數可以是輸入、輸入/輸出或輸出參數。 這不同于所有其他 SQL 語句中的參數，這些語句一律是輸入參數。  
  
 輸入參數是用來將值傳送至程式。 例如，假設 Part 資料表有 PartID、Description 和 Price 資料行。 針對資料表中的每個資料行，InsertPart 程式可能會有輸入參數。 例如：  
  
```  
{call InsertPart(?, ?, ?)}  
```  
  
 在 **SQLExecDirect** 或 **SQLExecute** 傳回 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、SQL_INVALID_HANDLE 或 SQL_NO_DATA 之前，驅動程式不應修改輸入緩衝區的內容。 當 **SQLExecDirect** 或 **SQLExecute** 傳回 SQL_NEED_DATA 或 SQL_STILL_EXECUTING 時，不應修改輸入緩衝區的內容。  
  
 輸入/輸出參數會用來將值傳送至程式，並從程式中取得值。 使用與輸入和輸出參數相同的參數通常會造成混淆，應予以避免。 例如，假設某個程式接受訂單識別碼，並傳回客戶的識別碼。 您可以使用單一輸入/輸出參數來定義此參數：  
  
```  
{call GetCustID(?)}  
```  
  
 使用兩個參數可能比較好：訂單識別碼的輸入參數，以及客戶識別碼的輸出或輸入/輸出參數：  
  
```  
{call GetCustID(?, ?)}  
```  
  
 輸出參數是用來取出程式傳回值，並從程式引數中取出值;傳回值的程式有時稱為 *函數*。 例如，假設剛才提及的 **GetCustID** 程式傳回一個值，指出它是否能夠找到順序。 在下列呼叫中，第一個參數是用來取出程式傳回值的輸出參數，第二個參數是用來指定順序識別碼的輸入參數，而第三個參數是用來抓取客戶識別碼的輸出參數：  
  
```  
{? = call GetCustID(?, ?)}  
```  
  
 驅動程式在程式中處理輸入和輸入/輸出參數的值，與其他 SQL 語句中的輸入參數不同。 當語句執行時，會抓取系結至這些參數的變數值，並將它們傳送到資料來源。  
  
 執行語句之後，驅動程式會將輸入/輸出和輸出參數的傳回值儲存在系結至這些參數的變數中。 在提取程式傳回的所有結果，且 **SQLMoreResults** 傳回 SQL_NO_DATA 之後，才保證會設定這些傳回的值。 如果執行語句會導致錯誤，則輸入/輸出參數緩衝區或輸出參數緩衝區的內容會是未定義的。  
  
 應用程式會呼叫 **SQLProcedure** 來判斷程式是否有傳回值。 它會呼叫 **SQLProcedureColumns** ，以判斷每個程式參數 (傳回值、輸入、輸入/輸出或輸出) 的型別。
