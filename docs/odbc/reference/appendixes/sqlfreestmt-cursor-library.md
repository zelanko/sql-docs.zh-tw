---
title: SQLFreeStmt （資料指標程式庫） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLFreeStmt function [ODBC], Cursor Library
ms.assetid: 47bfbd4d-9453-4609-958d-1e05794cb223
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d78075593926c15dbaeb1904603b08e990f64983
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81302019"
---
# <a name="sqlfreestmt-cursor-library"></a>SQLFreeStmt (資料指標程式庫)
> [!IMPORTANT]  
>  這項功能將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 本主題討論如何在資料指標程式庫中使用**SQLFreeStmt**函數。 如需有關**SQLFreeStmt**的一般資訊，請參閱[SQLFreeStmt 函數](../../../odbc/reference/syntax/sqlfreestmt-function.md)。  
  
 如果應用程式在呼叫**SQLExtendedFetch**、 **SQLFetch**或**SQLFetchScroll**之後，使用 SQL_UNBIND 選項呼叫**SQLFreeStmt** ，則資料指標程式庫會傳回錯誤。 應用程式必須使用 SQL_CLOSE 選項來呼叫**SQLCloseCursor**或**SQLFreeStmt** ，才能解除系結結果集資料行。
