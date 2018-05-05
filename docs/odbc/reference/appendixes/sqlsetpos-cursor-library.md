---
title: SQLSetPos （資料指標程式庫） |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLSetPos function [ODBC], Cursor Library
ms.assetid: 574399c3-2bb2-4d19-829c-7c77bd82858d
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b8a683d5b523205aa369769a612cf2b27cdb4800
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="sqlsetpos-cursor-library"></a>SQLSetPos （資料指標程式庫）
> [!IMPORTANT]  
>  將移除這項功能，在未來的版本的 Windows。 避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 本主題討論使用**SQLSetPos**資料指標程式庫中的函式。 如需一般資訊**SQLSetPos**，請參閱[SQLSetPos 函數](../../../odbc/reference/syntax/sqlsetpos-function.md)。  
  
 資料指標程式庫支援 SQL_POSITION 作業僅適用於*作業*引數中的**SQLSetPos**。 它支援僅適用於 SQL_LOCK_NO_CHANGE 值*LockType*引數。  
  
 如果驅動程式不支援大量作業，資料指標程式庫會傳回 SQLSTATE HYC00 （驅動程式不支援） 時**SQLSetPos**呼叫*RowNumber*等於 0。 不建議此驅動程式行為。  
  
 資料指標程式庫不支援的 SQL_UPDATE 和 SQL_DELETE 作業的呼叫中**SQLSetPos**。 定位更新或刪除 SQL 陳述式，藉由建立搜尋時，資料指標程式庫實作更新，或刪除陳述式搭配 WHERE 子句會列舉其每個繫結資料行的快取中儲存的值。 如需詳細資訊，請參閱[處理定位的更新和刪除陳述式](../../../odbc/reference/appendixes/processing-positioned-update-and-delete-statements.md)。  
  
 資料指標程式庫的應用程式的驅動程式不支援靜態資料指標，如果應該呼叫**SQLSetPos**只有在所提取的資料列集上**SQLExtendedFetch**或**SQLFetchScroll**、 不是由**SQLFetch**。 資料指標程式庫實作**SQLExtendedFetch**和**SQLFetchScroll**藉由重複的呼叫的**SQLFetch** （與資料列集大小為 1） 驅動程式中。 資料指標程式庫會傳遞至呼叫**SQLFetch**、 在其他交給，透過驅動程式。 如果**SQLSetPos**所提取的多重資料列資料列集上呼叫**SQLFetch**時驅動程式不支援靜態資料指標，呼叫會失敗，因為**SQLSetPos**無法運作以順向資料指標。 即使應用程式已成功呼叫，這會發生**SQLSetStmtAttr** SQL_ATTR_CURSOR_TYPE 設 SQL_CURSOR_STATIC，資料指標程式庫支援即使驅動程式不支援靜態資料指標。
