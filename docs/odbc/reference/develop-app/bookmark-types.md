---
title: "書籤類型 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- result sets [ODBC], bookmarks
- variable-length bookmarks [ODBC]
- bookmarks [ODBC]
- fixed-length bookmarks [ODBC]
ms.assetid: cb2e7443-0260-4d1a-930f-0154db447979
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 14ab851bb7878ec94f8044a4f7ef340754eff46c
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="bookmark-types"></a>書籤的型別
在 ODBC 3 的所有書籤*.x*可變長度的書籤。 這可讓主索引鍵或唯一索引相關聯的資料表來作為書籤。 書籤也可以是 32 位元值，所使用的 ODBC 2。*x*。 若要指定書籤使用與資料指標，而 ODBC 3*.x*應用程式設定 SQL_UB_VARIABLE SQL_ATTR_USE_BOOKMARK 陳述式屬性。 會自動使用可變長度的書籤。  
  
 應用程式可以呼叫**SQLColAttribute**與*FieldIdentifier*引數設定為 SQL_DESC_OCTET_LENGTH 以取得的書籤的長度。 可變長度的書籤可以是 long 值，因為應用程式應繫結至資料行 0 除非它會使用許多資料列集中的資料列的書籤。  
  
 僅為回溯相容性支援固定長度的書籤。 如果 ODBC 2。*x*應用程式使用 ODBC 3*.x*驅動程式呼叫**SQLSetStmtOption** SQL_USE_BOOKMARKS 設 SQL_UB_ON，它會對應至 SQL_UB_VARIABLE 中驅動程式管理員. 使用可變長度的書籤，即使只有 32 位元就會填入。 如果驅動程式支援固定長度的書籤，則會支援可變長度的書籤。 如果 ODBC 3*.x*應用程式使用 ODBC 2。*x*驅動程式呼叫**SQLSetStmtAttr** SQL_ATTR_USE_BOOKMARKS 設 SQL_UB_VARIABLE，它會對應至 SQL_UB_ON 中驅動程式管理員和 32 位元固定長度書籤。 SQL_ATTR_FETCH_BOOKMARK_PTR 陳述式屬性然後必須指向 32 位元書籤。 如果書籤使用超過 32 位元，例如資料指標時主索引鍵會當做書籤使用，必須對應到 32 位元值的實際值。 它可以比方說，來建置它們的雜湊資料表。 當 ODBC 3*.x*應用程式使用 ODBC 2。*x*驅動程式將繫結的書籤，緩衝區長度必須是 4。
