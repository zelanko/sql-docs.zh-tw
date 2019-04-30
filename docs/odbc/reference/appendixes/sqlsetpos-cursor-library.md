---
title: SQLSetPos （資料指標程式庫） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetPos function [ODBC], Cursor Library
ms.assetid: 574399c3-2bb2-4d19-829c-7c77bd82858d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b41fad0f609b16640bfa28ab36f29f364e067b73
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63297423"
---
# <a name="sqlsetpos-cursor-library"></a>SQLSetPos (資料指標程式庫)
> [!IMPORTANT]  
>  Windows 的未來版本將移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 本主題討論使用**SQLSetPos**資料指標程式庫中的函式。 如需一般資訊**SQLSetPos**，請參閱[SQLSetPos 函式](../../../odbc/reference/syntax/sqlsetpos-function.md)。  
  
 資料指標程式庫支援 SQL_POSITION 作業僅適用於*作業*中的引數**SQLSetPos**。 它支援僅適用於 SQL_LOCK_NO_CHANGE 值*LockType*引數。  
  
 如果驅動程式不支援大量作業，資料指標程式庫，將會傳回 SQLSTATE HYC00 （驅動程式不支援） 時**SQLSetPos**呼叫*RowNumber*等於 0。 不建議此驅動程式行為。  
  
 資料指標程式庫不支援的 SQL_UPDATE 和 SQL_DELETE 作業中呼叫**SQLSetPos**。 此資料指標程式庫會實作定位更新或刪除 SQL 陳述式，藉由建立搜尋更新，或刪除陳述式搭配 WHERE 子句，以列舉每個繫結的資料行快取中儲存的值。 如需詳細資訊，請參閱 <<c0> [ 處理定位的 Update 和刪除陳述式](../../../odbc/reference/appendixes/processing-positioned-update-and-delete-statements.md)。  
  
 如果驅動程式不支援靜態資料指標，使用資料指標程式庫的應用程式應該呼叫**SQLSetPos**只有在所擷取的資料列集上**SQLExtendedFetch**或**SQLFetchScroll**，而不**SQLFetch**。 資料指標程式庫會實作**SQLExtendedFetch**並**SQLFetchScroll**所進行的重複的呼叫**SQLFetch** （與資料列集大小為 1） 驅動程式中。 資料指標程式庫會傳遞至呼叫**SQLFetch**、 在其他交給，透過驅動程式。 如果**SQLSetPos**稱為多資料列的資料列集所擷取**SQLFetch**時，驅動程式不支援靜態資料指標，呼叫會失敗，因為**SQLSetPos**無法運作順向資料指標。 即使應用程式已成功地呼叫，這會發生**SQLSetStmtAttr** SQL_ATTR_CURSOR_TYPE 設 SQL_CURSOR_STATIC，資料指標程式庫支援，即使此驅動程式不支援靜態資料指標。
