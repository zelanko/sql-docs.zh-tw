---
title: SQLGetStmtAttr （資料指標程式庫） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetStmtAttr function [ODBC], Cursor Library
ms.assetid: 6c34e1ef-4273-4afb-a7d3-f9017ab69c5e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f9eef3ceba6fed1315d68038299640c772e92c9d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62751195"
---
# <a name="sqlgetstmtattr-cursor-library"></a>SQLGetStmtAttr (資料指標程式庫)
> [!IMPORTANT]  
>  Windows 的未來版本將移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 本主題討論使用**SQLGetStmtAttr**資料指標程式庫中的函式。 如需一般資訊**SQLGetStmtAttr**，請參閱[SQLGetStmtAttr 函式](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)。  
  
 資料指標程式庫支援下列陳述式屬性具有**SQLGetStmtAttr**:  
  
|||  
|-|-|  
|SQL_ATTR_CONCURRENCY|SQL_ATTR_ROW_BIND_OFFSET_PTR|  
|SQL_ATTR_CURSOR_TYPE|SQL_ATTR_ROW_BIND_TYPE|  
|SQL_ATTR_FETCH_BOOKMARK_PTR|SQL_ATTR_ROW_NUMBER|  
|SQL_ATTR_PARAM_BIND_OFFSET_PTR|SQL_ATTR_ROW_ARRAY_SIZE|  
|SQL_ATTR_PARAM_BIND_TYPE|SQL_ATTR_SIMULATE_CURSOR|
