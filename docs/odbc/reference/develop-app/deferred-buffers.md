---
description: 延遲的緩衝區
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 320271c39c735eafcfb1d59d26e7d0400eaa6e6c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424700"
---
# <a name="deferred-buffers"></a>延遲的緩衝區
*延遲的緩衝區*是在函式呼叫中指定值*之後*的某個時間使用值的緩衝區。 例如，您可以使用 **SQLBindParameter** ，在 SQL 語句中將資料緩衝區與參數建立 *關聯或系* 結。 應用程式會指定參數的數目，並傳遞緩衝區的位址、位元組長度和類型。 驅動程式會儲存此資訊，但不會檢查緩衝區的內容。 稍後，當應用程式執行語句時，驅動程式會抓取資訊並使用它來取出參數資料，並將其傳送至資料來源。 因此，緩衝區中資料的輸入會延後。 因為延遲的緩衝區是在一個函式中指定，並且在另一個函式中使用，所以在驅動程式仍預期它存在時，就會發生應用程式程式設計錯誤，以釋放延遲的緩衝區;如需詳細資訊，請參閱本節稍後的配置 [和釋放緩衝區](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)。  
  
 輸入和輸出緩衝區都可以延後。 下表摘要說明延遲緩衝區的使用。 請注意，系結至結果集資料行的延遲緩衝區會以 **SQLBindCol**指定，且系結至 SQL 語句參數的延遲緩衝區會以 **SQLBindParameter**指定。  
  
|緩衝區使用|類型|指定方式|使用對象|  
|----------------|----------|--------------------|-------------|  
|傳送輸入參數的資料|延後輸入|**SQLBindParameter**|**SQLExecute**<br /> **SQLExecDirect**|  
|傳送資料以更新或插入結果集中的資料列|延後輸入|**SQLBindCol**|**SQLSetPos**|  
|傳回輸出和輸入/輸出參數的資料|延遲的輸出|**SQLBindParameter**|**SQLExecute**<br /> **SQLExecDirect**|  
|傳回結果集資料|延遲的輸出|**SQLBindCol**|**SQLFetch**<br /> **SQLFetchScroll SQLSetPos**|
