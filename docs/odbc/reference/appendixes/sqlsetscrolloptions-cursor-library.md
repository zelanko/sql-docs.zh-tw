---
title: SQLSetScrollOptions （資料指標程式庫） |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e1fe6765c0ff8a057aac8e86ea5ad4aa1ac388b4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63297492"
---
# <a name="sqlsetscrolloptions-cursor-library"></a>SQLSetScrollOptions (資料指標程式庫)
> [!IMPORTANT]  
>  Windows 的未來版本將移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 本主題討論使用**SQLSetScrollOptions**資料指標程式庫中的函式。 如需一般資訊**SQLSetScrollOptions**，請參閱[SQLSetScrollOptions 函式](../../../odbc/reference/syntax/sqlsetscrolloptions-function.md)。  
  
 資料指標程式庫支援**SQLSetScrollOptions**僅為回溯相容性; 應用程式應該改用 SQL_ATTR_CONCURRENCY、 SQL_ATTR_CURSOR_TYPE 和 SQL_ATTR_ROW_ARRAY_SIZE 陳述式屬性。
