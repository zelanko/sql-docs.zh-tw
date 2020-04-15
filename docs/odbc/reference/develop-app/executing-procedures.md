---
title: 執行程式 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], procedures
- procedures [ODBC], executing
ms.assetid: a75e497a-4661-438a-a10e-f598c65f81be
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3a796c615d7dfdec11a9acb90ab4b5129cf69717
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305709"
---
# <a name="executing-procedures"></a>執行程序
ODBC 定義了執行過程的標準轉義序列。 有關此序列的語法和使用它的代碼範例,請參閱[過程呼叫](../../../odbc/reference/develop-app/procedure-calls.md)。  
  
 要執行過程,應用程式執行以下操作:  
  
1.  設置任何參數的值。 有關詳細資訊,請參閱本節後面的[語句參數](../../../odbc/reference/develop-app/statement-parameters.md)。  
  
2.  調用**SQLExecDirect**並傳遞一個字串,其中包含執行該過程的 SQL 語句。 此語句可以使用由 ODBC 或 DBMS 特定語法定義的轉義序列;使用特定於 DBMS 的語法的語句不可互通。  
  
3.  呼叫**SQLExecDirect**時,驅動程式:  
  
    -   檢索當前參數值並根據需要轉換它們。 有關詳細資訊,請參閱本節後面的[語句參數](../../../odbc/reference/develop-app/statement-parameters.md)。  
  
    -   呼叫資料來源中的過程,並向其發送轉換後的參數值。 驅動程式如何調用該過程是特定於驅動程式的。 例如,它可能會修改 SQL 語句以使用數據源的 SQL 語法並提交此語句以執行,或者可能直接使用 DBMS 的數據流協定中定義的遠端過程呼叫 (RPC) 機制呼叫該過程。  
  
    -   返回任何輸入/輸出或輸出參數的值或過程返回值,前提是該過程成功。 這些值可能直到處理過程生成的所有其他結果(行計數和結果集)後才可用。 如果該過程失敗,驅動程式將返回任何錯誤。
