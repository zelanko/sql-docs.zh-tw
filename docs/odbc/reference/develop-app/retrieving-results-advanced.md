---
title: 檢索結果(高級) |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- offsets [ODBC]
- result sets [ODBC], about result sets
- bind offsets [ODBC]
ms.assetid: bc00c379-71a7-407a-975c-898243f39bb6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ca02b4ff911c8edff06b38d5341eeaa288cc194c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294638"
---
# <a name="retrieving-results-advanced"></a>擷取結果 (進階)
應用程式可以指定在調用**SQLBulk 操作****、SQLFetch、SQLFetchScroll**或**SQLSetPos**時,將偏移**SQLFetchScroll**量添加到綁定的數據 緩衝區位址和相應的長度/指示器緩衝區位址。 這些添加的結果確定這些操作中使用的位址。  
  
 綁定偏移允許應用程式更改綁定,而無需為以前綁定的列調用**SQLBindCol。** 調用**SQLBindCol**以重新綁定數據會更改緩衝區位址和長度/ 指示器指標。 另一方面,使用偏移重新綁定只需向現有綁定數據緩衝區位址和長度/指示器緩衝區位址添加偏移。 使用偏移時,綁定是應用程式緩衝區佈局方式的"範本",應用程式可以通過更改偏移量將此"範本"移動到不同的記憶體區域。 可以隨時指定新的偏移量,並且始終添加到最初綁定的值。  
  
 要指定綁定偏移量,應用程式將SQL_ATTR_ROW_BIND_OFFSET_PTR語句屬性設置到 SQLINTEGER 緩衝區的位址。 在應用程式呼叫使用綁定的函數(如**SQLBulk 操作****、SQLFetch、SQLFetchScroll**或**SQLSetPos)** 之前,它會在此緩衝區中的位元組中放置偏移量,只要數據緩衝區位址和長度/ 指示器緩衝區位址都不是 0,**SQLFetchScroll**只要綁定列位於結果集中。 位址和偏移量的總和必須為有效位址。 (這意味著偏移量和添加到偏移的位址都無效,只要其總和是有效的位址。SQL_ATTR_ROW_BIND_OFFSET_PTR語句屬性是一個指標,因此偏移值可以應用於多組綁定數據,所有這些數據都可以通過更改一個偏移值來更改。 應用程式必須確保指標保持有效,直到游標關閉。  
  
> [!NOTE]  
>  ODBC 2 不支援綁定偏移。*x*驅動程式。  
  
 此章節包含下列主題。  
  
-   [區塊資料指標](../../../odbc/reference/develop-app/block-cursors.md)  
  
-   [可捲軸游標](../../../odbc/reference/develop-app/scrollable-cursors.md)  
  
-   [ODBC 資料指標程式庫](../../../odbc/reference/develop-app/the-odbc-cursor-library.md)  
  
-   [多個結果](../../../odbc/reference/develop-app/multiple-results.md)
