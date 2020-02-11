---
title: 延遲的緩衝區 |Microsoft Docs
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
ms.openlocfilehash: 1f7c90dacc375877b4e449b8d59533ce75ff8a4e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68076829"
---
# <a name="deferred-buffers"></a>延遲的緩衝區
延後的*緩衝區*是在函式呼叫中指定的某個時間點*之後*，會使用其值的一個。 例如， **SQLBindParameter**是用來建立或系結資料緩衝區與 SQL 語句*中的參數*。 應用程式會指定參數的數目，並傳遞緩衝區的位址、位元組長度和類型。 驅動程式會儲存這項資訊，但不會檢查緩衝區的內容。 之後，當應用程式執行語句時，驅動程式會抓取資訊，並使用它來抓取參數資料，並將它傳送至資料來源。 因此，緩衝區中的資料輸入會延遲。 因為延遲的緩衝區是在一個函式中指定，並用於另一個函數中，所以它是應用程式設計錯誤，可在驅動程式仍預期它存在時釋放延遲的緩衝區;如需詳細資訊，請參閱本節稍後的配置[和釋放緩衝區](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)。  
  
 輸入和輸出緩衝區都可以延後。 下表摘要說明延遲緩衝區的用法。 請注意，系結至結果集資料行的延遲緩衝區會使用**SQLBindCol**來指定，而且系結至 SQL 語句參數的延遲緩衝區會使用**SQLBindParameter**來指定。  
  
|緩衝區使用|類型|指定方式|使用對象|  
|----------------|----------|--------------------|-------------|  
|傳送輸入參數的資料|延後輸入|**SQLBindParameter**|**SQLExecute**<br /> **SQLExecDirect**|  
|傳送資料以更新或插入結果集中的資料列|延後輸入|**SQLBindCol**|**SQLSetPos**|  
|傳回輸出和輸入/輸出參數的資料|延遲的輸出|**SQLBindParameter**|**SQLExecute**<br /> **SQLExecDirect**|  
|傳回結果集資料|延遲的輸出|**SQLBindCol**|**SQLFetch**<br /> **SQLFetchScroll SQLSetPos**|
