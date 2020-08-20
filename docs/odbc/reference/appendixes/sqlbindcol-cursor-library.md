---
description: SQLBindCol (資料指標程式庫)
title: SQLBindCol (資料指標程式庫) |Microsoft Docs
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
ms.openlocfilehash: f3b3968687f1c9062457a16ec7c5bc11cb32d3a9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456477"
---
# <a name="sqlbindcol-cursor-library"></a>SQLBindCol (資料指標程式庫)
> [!IMPORTANT]  
>  未來的 Windows 版本將會移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 本主題討論如何在資料指標程式庫中使用 **SQLBindCol** 函數。 如需 **SQLBindCol**的一般資訊，請參閱 [SQLBindCol 函數](../../../odbc/reference/syntax/sqlbindcol-function.md)。  
  
 應用程式會為數據指標程式庫配置一或多個緩衝區，以傳回目前的資料列集。 它會呼叫 **SQLBindCol** 一次或多次，將這些緩衝區系結至結果集。  
  
 只要系結資料行的 C 資料類型、資料行大小和小數位數保持不變，應用程式就可以呼叫 **SQLBindCol** ，以便在呼叫 **SQLExtendedFetch**、 **SQLFetch**或 **SQLFetchScroll**之後，重新系結結果集資料行。 應用程式不需要關閉資料指標，即可將資料行重新系結至不同的位址。  
  
 資料指標程式庫支援將 SQL_ATTR_ROW_BIND_OFFSET_PTR 語句屬性設定為使用系結位移。 不需要呼叫 (**SQLBindCol** 就能進行此重新系結。 ) 如果資料指標程式庫 *與 ODBC 3.x* 驅動程式搭配使用，則在呼叫 **SQLFetch** 時，不會使用系結位移。 當資料指標程式庫*與 ODBC 2.x*驅動程式搭配使用時，如果呼叫**SQLFetch** ，就會使用系結位移，因為**SQLFetch**接著會對應到**SQLExtendedFetch**。  
  
 資料指標程式庫支援呼叫 **SQLBindCol** 來系結書簽資料行。  
  
 使用 *ODBC 2.x* 驅動程式時，資料指標程式庫會傳回 SQLSTATE HY090 (不正確字串或緩衝區長度) 當呼叫 **SQLBindCol** 將書簽資料行的緩衝區長度設定為不等於4的值時。 使用 *ODBC 3.x* 驅動程式時，資料指標程式庫允許緩衝區是任何大小。
