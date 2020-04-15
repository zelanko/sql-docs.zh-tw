---
title: SQLSetScroll選項(游標庫) |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetScrollOptions function [ODBC], Cursor Library
ms.assetid: c5c0ac6d-a6c1-4077-8186-1644df1944f8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0099ca5e9bcb3aefdd86e0132f52d110ab64e8a4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304909"
---
# <a name="sqlsetscrolloptions-cursor-library"></a>SQLSetScrollOptions (資料指標程式庫)
> [!IMPORTANT]  
>  此功能將在將來版本的 Windows 中刪除。 避免在新的開發工作中使用此功能,並計劃修改當前使用此功能的應用程式。 Microsoft 建議使用驅動程式的游標功能。  
  
 這個主題討論在游標庫中使用**SQLSetScrollOptions 函數**。 有關**SQLSetScroll 選項的**一般資訊,請參閱[SQLSetScrollOptions 函數](../../../odbc/reference/syntax/sqlsetscrolloptions-function.md)。  
  
 游標庫僅支援**SQLSetScroll 選項**,以便進行向後相容性;應用程式應改用SQL_ATTR_CONCURRENCY、SQL_ATTR_CURSOR_TYPE和SQL_ATTR_ROW_ARRAY_SIZE語句屬性。
