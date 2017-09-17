---
title: "延後緩衝區 |Microsoft 文件"
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
- buffers [ODBC], deferred
- deferred buffers [ODBC]
ms.assetid: 02c9a75c-2103-4f68-a1db-e31f7e0f1f03
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 94d240284ce0273e0700bfbabfb38fd0a41884cf
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="deferred-buffers"></a>延後的緩衝區
A*延後的緩衝區*是在稍後使用其值的其中一個*之後*函式呼叫中指定。 例如， **SQLBindParameter**來建立關聯，或*繫結，*資料緩衝區中的 SQL 陳述式搭配參數。 應用程式指定的參數數目，並傳遞位址、 位元組長度和類型的緩衝區。 驅動程式會將此資訊儲存，但不會檢查緩衝區的內容。 稍後，當應用程式執行陳述式時，驅動程式擷取的資訊並使用它來擷取參數資料，並將它傳送至資料來源。 因此，會延後的輸入緩衝區中的資料。 因為延後的緩衝區是一個函式中指定，而且在另一個使用，所以應用程式的程式設計錯誤時，驅動程式仍需要它存在; 釋放延後的緩衝區如需詳細資訊，請參閱[Allocating 和釋放緩衝區](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)稍後這一節。  
  
 輸入和輸出緩衝區，就會延遲。 下表摘要說明使用延後的緩衝區。 請注意延遲的緩衝區繫結至結果集資料行所指定的**SQLBindCol**，並延後的緩衝區繫結至 SQL 陳述式參數所指定的**SQLBindParameter**。  
  
|緩衝區使用|類型|使用指定|使用|  
|----------------|----------|--------------------|-------------|  
|傳送資料的輸入參數|延後的輸入|**SQLBindParameter**|**SQLExecute**<br /> **SQLExecDirect**|  
|若要更新或插入資料列中，將結果傳送資料集|延後的輸入|**SQLBindCol**|**SQLSetPos**|  
|輸出和輸入/輸出參數傳回資料|延後的輸出|**SQLBindParameter**|**SQLExecute**<br /> **SQLExecDirect**|  
|傳回結果集資料|延後的輸出|**SQLBindCol**|**SQLFetch**<br /> **SQLFetchScroll SQLSetPos**|
