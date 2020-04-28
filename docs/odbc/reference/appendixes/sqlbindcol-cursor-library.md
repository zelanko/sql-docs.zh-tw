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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1c29909a96f147a0f5ebc2140a68072dfe544255
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305469"
---
# <a name="sqlbindcol-cursor-library"></a>SQLBindCol (資料指標程式庫)
> [!IMPORTANT]  
>  這項功能將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 本主題討論如何在資料指標程式庫中使用**SQLBindCol**函數。 如需有關**SQLBindCol**的一般資訊，請參閱[SQLBindCol 函數](../../../odbc/reference/syntax/sqlbindcol-function.md)。  
  
 應用程式會為數據指標程式庫配置一個或多個緩衝區，以傳回中目前的資料列集。 它會呼叫**SQLBindCol**一次或多次，以將這些緩衝區系結至結果集。  
  
 應用程式可以呼叫**SQLBindCol** ，以便在呼叫**SQLExtendedFetch**、 **SQLFetch**或**SQLFetchScroll**之後重新系結結果集資料行，只要 C 資料類型、資料行大小和系結資料行的小數位數保持不變即可。 應用程式不需要關閉資料指標，即可將資料行重新系結至不同的位址。  
  
 資料指標程式庫支援將 SQL_ATTR_ROW_BIND_OFFSET_PTR 語句屬性設定為使用系結位移。 （不需要呼叫**SQLBindCol** ，就會發生此重新系結）。如果資料指標程式庫*與 ODBC 3.x*驅動程式搭配使用，則在呼叫**SQLFetch**時，不會使用系結位移。 當資料指標程式庫*與 ODBC 2.x*驅動程式搭配使用時，如果呼叫**SQLFetch** ，就會使用系結位移，因為**SQLFetch**會接著對應至**SQLExtendedFetch**。  
  
 資料指標程式庫支援呼叫**SQLBindCol**來系結書簽資料行。  
  
 使用*ODBC 2.x*驅動程式時，當呼叫**SQLBindCol**時，資料指標程式庫會傳回 SQLSTATE HY090 （不正確字串或緩衝區長度），以將書簽資料行的緩衝區長度設定為不等於4的值。 使用*ODBC 3.x*驅動程式時，資料指標程式庫可讓緩衝區成為任何大小。
