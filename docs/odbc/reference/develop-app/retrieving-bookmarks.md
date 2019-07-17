---
title: 擷取書籤 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- retrieving bookmarks [ODBC]
- result sets [ODBC], bookmarks
- bookmarks [ODBC]
ms.assetid: a34c8f09-b786-4835-a44b-b7294c970aff
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f18b87adf31f19d2a93bb3af3e14c265ae3940af
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68020570"
---
# <a name="retrieving-bookmarks"></a>擷取書籤
如果應用程式會使用書籤，它必須設 SQL_UB_VARIABLE 之前準備或執行陳述式來 SQL_ATTR_USE_BOOKMARKS 陳述式屬性。 這是必要的因為建置和維護的書籤可以昂貴的作業，因此只有在應用程式可以進行良好時，才應該啟用書籤使用它們。  
  
 書籤會傳回為結果集的資料行 0。 有三種方式，應用程式可以擷取這些資訊：  
  
-   繫結結果集的資料行 0。 **SQLFetch**或是**SQLFetchScroll**傳回書籤的資料行的資料列以及其他資料集中的每個資料列繫結。  
  
-   呼叫**SQLSetPos**中的資料列集的資料列的位置，然後呼叫**SQLGetData**資料行 0。 如果驅動程式支援書籤，它必須一律支援，以及呼叫**SQLGetData**資料行 0，即使它不允許應用程式呼叫**SQLGetData**之前最後一個繫結的其他資料行資料行。  
  
-   呼叫**SQLBulkOperations**具有*作業*設 SQL_ADD，引數和繫結資料行 0。 資料指標插入的資料列，並傳回繫結緩衝區中的資料列的書籤。
