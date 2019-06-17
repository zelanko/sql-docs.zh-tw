---
title: 設定描述項欄位 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], retrieving or setting field values
ms.assetid: d735dc64-370f-48ab-a59f-6cef9bc4e1e8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 14724a5cc863074344cfbb02615f0ccff228f04c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62447666"
---
# <a name="setting-descriptor-fields"></a>設定描述項欄位
若要修改的欄位描述元，應用程式可以呼叫**SQLSetDescField**。 某些欄位是唯讀的而且無法設定。 (請參閱[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)函式描述。)  
  
 描述項記錄的欄位會設定與資料錄數目 (*RecNumber*) 1 或更高版本，while 的描述項標頭欄位會設定使用記錄數字 0。 若要設定書籤的欄位，依照慣例，書籤會包含在資料行 0 也會記錄數字 0。 這可能會導致書籤欄位都包含在描述項標頭，但這不是大小寫的印象。 書籤的欄位是標頭欄位有所區別。  
  
 當個別設定欄位時，應用程式應遵循中定義的順序[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)。 設定某些欄位會導致驅動程式來設定其他欄位。 這可確保的描述元一律可供使用後具有指定的資料類型的應用程式。 當應用程式設定的 SQL_DESC_TYPE 欄位時，驅動程式會檢查指定類型的其他欄位有效且一致。  
  
 如果設定描述項欄位的函式呼叫失敗，描述項欄位的內容失敗函式呼叫之後為未定義。
