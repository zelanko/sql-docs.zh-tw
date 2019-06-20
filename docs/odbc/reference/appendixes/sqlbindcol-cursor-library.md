---
title: SQLBindCol （資料指標程式庫） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLAllocStmt function [ODBC], Cursor Library
ms.assetid: f4dd546a-0a6c-4397-8ee7-fafa6b9da543
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9e9e1018754977ee73ecdc21db30b3d8c2aae8b4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63199680"
---
# <a name="sqlbindcol-cursor-library"></a>SQLBindCol (資料指標程式庫)
> [!IMPORTANT]  
>  Windows 的未來版本將移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 本主題討論使用**SQLBindCol**資料指標程式庫中的函式。 如需一般資訊**SQLBindCol**，請參閱[SQLBindCol 函式](../../../odbc/reference/syntax/sqlbindcol-function.md)。  
  
 應用程式配置資料指標程式庫，來傳回在目前資料列集的一或多個緩衝區。 它會呼叫**SQLBindCol**一或多次，以將這些緩衝區繫結至結果集。  
  
 應用程式可以呼叫**SQLBindCol**重新繫結結果集資料行之後就叫做**SQLExtendedFetch**， **SQLFetch**，或**SQLFetchScroll**，只要 C 資料類型、 資料行大小和小數位數的繫結的資料行維持不變。 應用程式不需要關閉資料指標重新繫結至不同的地址的資料行。  
  
 資料指標程式庫支援 SQL_ATTR_ROW_BIND_OFFSET_PTR 陳述式將屬性設定為使用繫結的位移。 (**SQLBindCol**並沒有為此重新繫結進行呼叫。)如果資料指標程式庫會使用 ODBC 3 *.x*驅動程式繫結位移並不使用的時機**SQLFetch**呼叫。 如果，則會使用繫結位移**SQLFetch**稱為資料指標程式庫搭配 ODBC 2。*x*驅動程式因為**SQLFetch**會接著對應至**SQLExtendedFetch**。  
  
 資料指標程式庫支援呼叫**SQLBindCol**繫結的書籤資料行。  
  
 使用時的 ODBC 2。*x*驅動程式，資料指標程式庫會傳回 SQLSTATE HY090 （無效的字串或緩衝區長度） 時**SQLBindCol**呼叫以設定為值的書籤資料行緩衝區的長度不等於 4。 使用 ODBC 3 時 *.x*驅動程式，資料指標程式庫可讓任何大小的緩衝區。
