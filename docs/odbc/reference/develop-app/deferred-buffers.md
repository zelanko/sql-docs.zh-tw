---
title: 延後緩衝區 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- buffers [ODBC], deferred
- deferred buffers [ODBC]
ms.assetid: 02c9a75c-2103-4f68-a1db-e31f7e0f1f03
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 14c1514759765699826c48a0cfb68e0eeba7a583
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32910033"
---
# <a name="deferred-buffers"></a>延後的緩衝區
A*延後的緩衝區*是在稍後使用其值的其中一個*之後*函式呼叫中指定。 例如， **SQLBindParameter**來建立關聯，或*繫結，* 資料緩衝區中的 SQL 陳述式搭配參數。 應用程式指定的參數數目，並傳遞位址、 位元組長度和類型的緩衝區。 驅動程式會將此資訊儲存，但不會檢查緩衝區的內容。 稍後，當應用程式執行陳述式時，驅動程式擷取的資訊並使用它來擷取參數資料，並將它傳送至資料來源。 因此，會延後的輸入緩衝區中的資料。 因為延後的緩衝區是一個函式中指定，而且在另一個使用，所以應用程式的程式設計錯誤時，驅動程式仍需要它存在; 釋放延後的緩衝區如需詳細資訊，請參閱[Allocating 和釋放緩衝區](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)稍後這一節。  
  
 輸入和輸出緩衝區，就會延遲。 下表摘要說明使用延後的緩衝區。 請注意延遲的緩衝區繫結至結果集資料行所指定的**SQLBindCol**，並延後的緩衝區繫結至 SQL 陳述式參數所指定的**SQLBindParameter**。  
  
|緩衝區使用|型別|使用指定|使用|  
|----------------|----------|--------------------|-------------|  
|傳送資料的輸入參數|延後的輸入|**SQLBindParameter**|**SQLExecute**<br /> **SQLExecDirect**|  
|若要更新或插入資料列中，將結果傳送資料集|延後的輸入|**SQLBindCol**|**SQLSetPos**|  
|輸出和輸入/輸出參數傳回資料|延後的輸出|**SQLBindParameter**|**SQLExecute**<br /> **SQLExecDirect**|  
|傳回結果集資料|延後的輸出|**SQLBindCol**|**SQLFetch**<br /> **SQLFetchScroll SQLSetPos**|
