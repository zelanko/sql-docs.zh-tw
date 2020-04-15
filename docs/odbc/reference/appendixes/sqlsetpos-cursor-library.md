---
title: SQLSetPos(游標庫) |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4c46ef88075a5adbd96138d7d1f03c26712f7ea1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300508"
---
# <a name="sqlsetpos-cursor-library"></a>SQLSetPos (資料指標程式庫)
> [!IMPORTANT]  
>  此功能將在將來版本的 Windows 中刪除。 避免在新的開發工作中使用此功能,並計劃修改當前使用此功能的應用程式。 Microsoft 建議使用驅動程式的游標功能。  
  
 本主題討論在遊標庫中使用**SQLSetPos**函數。 有關**SQLSetPos**的一般資訊,請參閱[SQLSetPos 函數](../../../odbc/reference/syntax/sqlsetpos-function.md)。  
  
 游標庫僅支援**SQLSetPos**中的*操作*參數的操作SQL_POSITION操作。 它僅支援*LockType*參數的SQL_LOCK_NO_CHANGE值。  
  
 如果驅動程式不支援批量操作,則當調用**SQLSetPos**時,*使用行號*等於 0 時,遊標庫將返回 SQLSTATE HYC00(驅動程式無法啟用)。 不建議使用此驅動程序行為。  
  
 游標庫不支援對**SQLSetPos**的調用中SQL_UPDATE和SQL_DELETE操作。 游標庫通過創建搜索的更新或刪除語句實現定位更新或刪除 SQL 語句,該語句具有 WHERE 子句,該語句枚舉存儲在其緩存中為每個綁定列的值。 有關詳細資訊,請參閱[處理定位更新與移除語句](../../../odbc/reference/appendixes/processing-positioned-update-and-delete-statements.md)。  
  
 如果驅動程式不支援靜態游標,則使用游標庫的應用程式應僅在**SQLExtendedFetch**或**SQLFetchScroll**取得的行集上調用**SQLSetPos,** 而不是**SQLFetch**呼叫 。 游標庫透過在驅動程式中重複呼叫**SQLFetch(** 行集大小為 1)實現**SQL 擴充取得**和**SQLFetchScroll。** 另一方面,游標庫將呼叫傳遞到**驅動程式**。 如果在驅動程式不支援靜態游標時**SQLFetch**獲取的多行行集上調用**SQLSetPos,** 則呼叫將失敗,因為**SQLSetPos**不適用於僅轉發游標。 即使應用程式已成功調用**SQLSetStmtAttr**將SQL_ATTR_CURSOR_TYPE設置為SQL_CURSOR_STATIC,即使驅動程式不支援靜態游標,也會發生這種情況。
