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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e34c07cdd248d5da4efd9f66d7292bd6ab443e92
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300608"
---
# <a name="sqlgetstmtoption-cursor-library"></a>SQLGetStmtOption (資料指標程式庫)
> [!IMPORTANT]  
>  這項功能將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 本主題討論如何在資料指標程式庫中使用**SQLGetStmtOption**函數。 如需有關**SQLGetStmtOption**的一般資訊，請參閱[SQLGetStmtOption 函數](../../../odbc/reference/syntax/sqlgetstmtoption-function.md)。  
  
 資料指標程式庫支援下列使用**SQLGetStmtOption**的語句選項：  
  
|||  
|-|-|  
|SQL_BIND_TYPE|SQL_ROW_NUMBER|  
|SQL_CONCURRENCY|SQL_ROWSET_SIZE|  
|SQL_CURSOR_TYPE|SQL_SIMULATE_CURSOR|  
|SQL_GET_BOOKMARK||
