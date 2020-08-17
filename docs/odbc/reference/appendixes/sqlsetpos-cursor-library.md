---
description: SQLSetPos (資料指標程式庫)
title: SQLSetPos (資料指標程式庫) |Microsoft Docs
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
ms.openlocfilehash: d35f1461f6a5da3ee894d9275c6ca112bfabab44
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88339234"
---
# <a name="sqlsetpos-cursor-library"></a>SQLSetPos (資料指標程式庫)
> [!IMPORTANT]  
>  未來的 Windows 版本將會移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 本主題討論如何在資料指標程式庫中使用 **SQLSetPos** 函數。 如需 **SQLSetPos**的一般資訊，請參閱 [SQLSetPos 函數](../../../odbc/reference/syntax/sqlsetpos-function.md)。  
  
 資料指標程式庫只支援**SQLSetPos**中的*operation*引數的 SQL_POSITION 作業。 它僅支援 *LockType* 引數的 SQL_LOCK_NO_CHANGE 值。  
  
 如果驅動程式不支援大量作業，當以*RowNumber*等於0呼叫**SQLSetPos**時，資料指標程式庫會傳回 SQLSTATE HYC00 (驅動程式無法) 。 不建議使用此驅動程式行為。  
  
 資料指標程式庫不支援呼叫 **SQLSetPos**時的 SQL_UPDATE 和 SQL_DELETE 作業。 資料指標程式庫會使用 WHERE 子句來建立搜尋的 update 或 delete 語句，以針對每個系結的資料行列舉其快取中儲存的值，以執行定點更新或刪除 SQL 語句。 如需詳細資訊，請參閱 [處理定點更新和刪除語句](../../../odbc/reference/appendixes/processing-positioned-update-and-delete-statements.md)。  
  
 如果驅動程式不支援靜態資料指標，使用資料指標程式庫的應用程式應該只在**SQLExtendedFetch**或**SQLFetchScroll**所提取的資料列集上呼叫**SQLSetPos** ，而不是**SQLFetch**。 資料指標程式庫會在驅動程式中對資料列集大小為 1) 的**SQLFetch** (進行重複呼叫，以執行**SQLExtendedFetch**和**SQLFetchScroll** 。 資料指標程式庫會將對 **SQLFetch**的呼叫傳遞至驅動程式。 當驅動程式不支援靜態資料指標時，如果在**SQLFetch**所提取的多資料列資料列集上呼叫**SQLSetPos** ，呼叫將會失敗，因為**SQLSetPos**無法使用順向資料指標。 即使應用程式已成功呼叫 **SQLSetStmtAttr** 將 SQL_ATTR_CURSOR_TYPE 設定為 SQL_CURSOR_STATIC （即使驅動程式不支援靜態資料指標，也會支援），這也會發生這種情況。
