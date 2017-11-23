---
title: "SQLBindCol （資料指標程式庫） |Microsoft 文件"
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
helpviewer_keywords: SQLAllocStmt function [ODBC], Cursor Library
ms.assetid: f4dd546a-0a6c-4397-8ee7-fafa6b9da543
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bf80a3dfd02c2871267cfe57f1b95ae246094bc9
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="sqlbindcol-cursor-library"></a>SQLBindCol （資料指標程式庫）
> [!IMPORTANT]  
>  將移除這項功能，在未來的版本的 Windows。 避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 本主題討論使用**SQLBindCol**資料指標程式庫中的函式。 如需一般資訊**SQLBindCol**，請參閱[SQLBindCol 函數](../../../odbc/reference/syntax/sqlbindcol-function.md)。  
  
 應用程式配置一或多個緩衝區，以傳回目前資料列集資料指標程式庫。 它會呼叫**SQLBindCol**一或多次，以將這些緩衝區繫結至結果集。  
  
 應用程式可以呼叫**SQLBindCol**重新繫結結果集資料行之後又稱為**SQLExtendedFetch**， **SQLFetch**，或**SQLFetchScroll**，只要 C 資料類型、 資料行大小和小數位數的繫結的資料行維持不變。 應用程式不需要關閉資料指標重新繫結至不同位址的資料行。  
  
 資料指標程式庫支援的設定，若要使用繫結位移 SQL_ATTR_ROW_BIND_OFFSET_PTR 陳述式屬性。 (**SQLBindCol**並沒有發生重新繫結呼叫。)如果資料指標程式庫會使用 ODBC 3*.x*驅動程式，繫結位移不是使用當**SQLFetch**呼叫。 如果使用繫結位移**SQLFetch**稱為資料指標程式庫搭配 ODBC 2。*x*驅動程式因為**SQLFetch**接著會對應到**SQLExtendedFetch**。  
  
 資料指標程式庫支援呼叫**SQLBindCol**繫結的書籤資料行。  
  
 當使用的 ODBC 2。*x*驅動程式，資料指標程式庫會傳回 SQLSTATE HY090 （無效的字串或緩衝區長度） 時**SQLBindCol**呼叫以設定為值的書籤資料行的緩衝區長度不等於 4。 使用 ODBC 3 時*.x*驅動程式，資料指標程式庫會允許任何大小的緩衝區。
