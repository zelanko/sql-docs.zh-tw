---
title: 按書籤滾動 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], bookmarks
- bookmarks [ODBC]
- scrolling rows [ODBC]
ms.assetid: 4862f098-41a4-4bd2-894e-f71bb97f9bc0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 454e29abdf848fdf4f4eaae090e7cc326f0048df
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304189"
---
# <a name="scrolling-by-bookmark"></a>依書籤捲動
使用**SQLFetchScroll**提取行時,應用程式可以使用書籤作為選擇起始行的基礎。 這是一個絕對位址的形式，因為它不相依於目前的資料指標位置。 要滾動到書籤行,應用程式調用**SQLFetchScroll,** 獲取*方向*為 SQL_FETCH_BOOKMARK。 此操作使用SQL_ATTR_FETCH_BOOKMARK_PTR語句屬性指向的書籤。 它會傳回資料列集，從該書籤識別的資料列開始。 應用程式可以在調用**SQLFetchScroll**的*FetchOffset*參數中指定此操作的偏移量。 指定偏移量時,通過將*FetchOffset*參數中的數位添加到書籤標識的行數來確定返回的行集的第一行。 與 ODBC 2 一起使用時,不支援使用*FetchOffset*參數。*x*驅動程式;當應用程式在 ODBC 2 中呼叫**SQLFetchScroll**時。*將**取取方向*設置為SQL_FETCH_BOOKMARK的 x 驅動程式必須將*FetchOffset*參數設置為 0。
