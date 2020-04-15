---
title: 延遲緩衝區 |微軟文件
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
ms.openlocfilehash: f34c6d3d886a0a75c309dc4f5c71f5c7ba3df447
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305979"
---
# <a name="deferred-buffers"></a>延遲的緩衝區
*延遲緩衝區*是其值在函數調用中指定*後*某個時間使用該緩衝區的緩衝區。 例如 **,SQLBind 參數**用於將資料緩衝區與 SQL 語句中的參數關聯或*繫結*。 應用程式指定參數的編號,並傳遞緩衝區的位址、位元組長度和類型。 驅動程式保存此資訊,但不檢查緩衝區的內容。 稍後,當應用程式執行語句時,驅動程式檢索資訊並使用它檢索參數數據並將其發送到數據源。 因此,將延遲緩衝區中數據的輸入。 由於延遲緩衝區在一個函數中指定,在另一個函數中使用,因此在驅動程式仍希望它存在時釋放延遲緩衝區是應用程式程式設計錯誤;有關詳細資訊,請參閱本節後面的[分配和釋放緩衝區](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)。  
  
 輸入緩衝區和輸出緩衝區都可以延遲。 下表總結了延遲緩衝區的使用。 請注意,綁定到結果集列的延遲緩衝區是使用**SQLBindCol**指定的,而綁定到 SQL 語句參數的延遲緩衝區則使用**SQLBind 參數**指定。  
  
|緩衝區使用|類型|使用|使用對象|  
|----------------|----------|--------------------|-------------|  
|傳送輸入參數的資料|延遲輸入|**SQLBindParameter**|**SQLExecute**<br /> **SQLExecDirect**|  
|傳送資料以更新或插入結果集中的列|延遲輸入|**SQLBindCol**|**SQLSetPos**|  
|傳回輸出與輸入/輸出參數的資料|延遲輸出|**SQLBindParameter**|**SQLExecute**<br /> **SQLExecDirect**|  
|傳回結果集資料|延遲輸出|**SQLBindCol**|**SQLFetch**<br /> **SQLFetchScroll SQLSetPos**|
