---
title: SQLBindCol(游標庫) |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1c29909a96f147a0f5ebc2140a68072dfe544255
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305469"
---
# <a name="sqlbindcol-cursor-library"></a>SQLBindCol (資料指標程式庫)
> [!IMPORTANT]  
>  此功能將在將來版本的 Windows 中刪除。 避免在新的開發工作中使用此功能,並計劃修改當前使用此功能的應用程式。 Microsoft 建議使用驅動程式的游標功能。  
  
 本主題討論在遊標庫中使用**SQLBindCol**函數。 有關**SQLBindCol**的一般資訊,請參閱[SQLBindCol 函數](../../../odbc/reference/syntax/sqlbindcol-function.md)。  
  
 應用程式為游標庫分配一個或多個緩衝區以返回當前行集。 它調用**SQLBindCol**一次或多次將這些緩衝區綁定到結果集。  
  
 應用程式可以調用**SQLBindCol**在呼叫**SQL 擴充取得****、SQLFetch**或**SQLFetchScroll**後重新繫出結果集列,只要綁定列的 C 資料類型、列大小和十進位數位保持不變。 應用程式不需要關閉游標,將列重新綁定到不同的位址。  
  
 游標庫支援將SQL_ATTR_ROW_BIND_OFFSET_PTR語句屬性設置為使用綁定偏移量。 **(SQLBindCol**不必呼叫此重新綁定。如果游標庫與 ODBC *3.x*驅動程式一起使用,則在調用**SQLFetch**時不使用綁定偏移量。 如果當游標庫與 ODBC *2.x*驅動程式一起使用時呼叫**SQLFetch,** 則使用繫結偏移,因為**SQLFetch**隨後被映射到**SQLExtendedFetch**。  
  
 游標庫支援調用**SQLBindCol**來綁定書籤列。  
  
 使用 ODBC *2.x*驅動程式時,當調用**SQLBindCol**將書籤列的緩衝區長度設置為不等於 4 的值時,游標庫將返回 SQLSTATE HY090(無效字串或緩衝區長度)。 使用 ODBC *3.x*驅動程式時,游標庫允許緩衝區具有任何大小。
