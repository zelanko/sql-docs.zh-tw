---
title: SQLGetStmtOption （資料指標程式庫） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetStmtOption function [ODBC], Cursor Library
ms.assetid: 986170b3-fba8-4323-9224-60b381c7effb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f4c7429bd4a3780caaf5bc7e0624d0e92ef4dd3f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62751171"
---
# <a name="sqlgetstmtoption-cursor-library"></a>SQLGetStmtOption (資料指標程式庫)
> [!IMPORTANT]  
>  Windows 的未來版本將移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 本主題討論使用**SQLGetStmtOption**資料指標程式庫中的函式。 如需一般資訊**SQLGetStmtOption**，請參閱[SQLGetStmtOption 函式](../../../odbc/reference/syntax/sqlgetstmtoption-function.md)。  
  
 資料指標程式庫支援下列陳述式選項搭配**SQLGetStmtOption**:  
  
|||  
|-|-|  
|SQL_BIND_TYPE|SQL_ROW_NUMBER|  
|SQL_CONCURRENCY|SQL_ROWSET_SIZE|  
|SQL_CURSOR_TYPE|SQL_SIMULATE_CURSOR|  
|SQL_GET_BOOKMARK||
