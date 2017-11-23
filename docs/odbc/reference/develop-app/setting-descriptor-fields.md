---
title: "設定描述項欄位 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: descriptors [ODBC], retrieving or setting field values
ms.assetid: d735dc64-370f-48ab-a59f-6cef9bc4e1e8
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b618eb94f27015d807e1d8373108684ed77a2c7d
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="setting-descriptor-fields"></a>設定描述項欄位
若要修改的描述項欄位，應用程式可以呼叫**SQLSetDescField**。 某些欄位是唯讀而且無法設定。 (請參閱[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)函式描述。)  
  
 資料錄數目設定描述項記錄欄位 (*RecNumber*) 1 或更高，時間的描述項標頭欄位會設定使用 0 的記錄數目。 記錄數字 0 也用於設定書籤的欄位，根據書籤，會包含在資料行 0 的慣例。 這可能導致描述項標頭中包含書籤欄位，但這不是這樣的印象。 書籤欄位是不同的標頭欄位。  
  
 個別設定的欄位，當應用程式應該遵循中定義的順序[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)。 設定某些欄位會導致驅動程式來設定其他欄位。 這可確保描述元永遠可供使用後的應用程式指定的資料類型。 當應用程式設定的 SQL_DESC_TYPE 欄位時，驅動程式會檢查其他指定類型的欄位有效，而且一致。  
  
 如果函式呼叫會設定描述項欄位失敗，描述項欄位的內容是未定義的失敗函式呼叫之後。
