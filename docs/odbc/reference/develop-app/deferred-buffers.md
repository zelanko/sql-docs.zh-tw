---
title: 延遲緩衝區 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- buffers [ODBC], deferred
- deferred buffers [ODBC]
ms.assetid: 02c9a75c-2103-4f68-a1db-e31f7e0f1f03
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b071494697d21a37f4420889a8f60cc35fe3d8b2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47797196"
---
# <a name="deferred-buffers"></a>延遲的緩衝區
A*延後的緩衝區*是其中一個使用其值的某個時間點*之後*函式呼叫中指定。 例如， **SQLBindParameter**用來建立關聯，或*繫結，* 資料緩衝區中，使用 SQL 陳述式中的參數。 應用程式指定的參數數目，並將傳遞地址、 位元組長度和類型的緩衝區。 驅動程式會將此資訊儲存，但不會檢查緩衝區的內容。 稍後，當應用程式執行的陳述式，驅動程式擷取的資訊，並使用它來擷取參數資料，並將它傳送至資料來源。 因此，會延後的輸入緩衝區中的資料。 延後的緩衝區會有一個函式中指定，並在另一個使用，因為它是應用程式的程式設計錯誤釋放延後的緩衝區時，驅動程式仍需要它的存在;如需詳細資訊，請參閱 < [Allocating 及釋放緩衝區](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)稍後這一節。  
  
 輸入和輸出緩衝區可以延後。 下表摘要說明使用延遲的緩衝區。 請注意延遲的緩衝區繫結至結果集資料行所指定的**SQLBindCol**，和延遲的緩衝區繫結至 SQL 陳述式參數所指定的**SQLBindParameter**。  
  
|緩衝區使用|類型|使用指定|使用|  
|----------------|----------|--------------------|-------------|  
|針對輸入參數傳送資料|延遲的輸入|**SQLBindParameter**|**SQLExecute**<br /> **SQLExecDirect**|  
|若要更新或插入資料列中，將結果傳送的資料集|延遲的輸入|**SQLBindCol**|**SQLSetPos**|  
|輸出和輸入/輸出參數傳回的資料|延後的輸出|**SQLBindParameter**|**SQLExecute**<br /> **SQLExecDirect**|  
|傳回結果集資料|延後的輸出|**SQLBindCol**|**SQLFetch**<br /> **SQLFetchScroll SQLSetPos**|
