---
title: SQLSetStmtOption (Visual FoxPro ODBC Driver) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetStmtOption function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 76b813e3-c7dc-4bb2-a710-d2aa9dcfdc36
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a026922cb98fdb520c9eeab223c8b34a231a179e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67905334"
---
# <a name="sqlsetstmtoption-visual-foxpro-odbc-driver"></a>SQLSetStmtOption (Visual FoxPro ODBC Driver)
> [!NOTE]  
>  本主題包含 Visual FoxPro ODBC 驅動程式特有的資訊。 如需此函式的一般資訊，請參閱底下的適當主題[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 支援：完整  
  
 ODBC API 相容性：層級 1  
  
 設定與陳述式控制代碼相關的選項*hstmt*。  
  
|*fOption*|允許的值|註解|  
|---------------|--------------------|--------------|  
|SQL_ASYNC_ENABLE|SQL_ASYNC_ENABLE_OFF|如果您嘗試將此*fOption*，驅動程式會傳回錯誤：「 驅動程式不支援 」。 Visual FoxPro 不支援非同步執行。|  
|SQL_BIND_TYPE|SQL_BIND_BY_COLUMN 或 32 位元值，表示結構或緩衝區成的結果將會繫結資料行的執行個體的長度。||  
|SQL_CONCURRENCY|SQL_CONCUR_READ_ONLY<br /><br /> SQL_CONCUR_LOCK<br /><br /> SQL_CONCUR_VALUES|驅動程式不允許 SQL_CONCUR_ROWVER，因為 Visual FoxPro 並沒有時間戳記為基礎的資料列版本設定。|  
|SQL_CURSOR_TYPE|SQL_CURSOR_FORWARD_ONLY<br /><br /> SQL_CURSOR_STATIC|驅動程式不允許 SQL_CURSOR_KEYSET_DRIVEN 或 SQL_CURSOR_DYNAMIC;請參閱[SQLSetScrollOptions](../../odbc/microsoft/sqlsetscrolloptions-visual-foxpro-odbc-driver.md)如需詳細資訊。|  
|SQL_KEYSET_SIZE|錯誤：「 驅動程式不支援 」|Visual FoxPro 不支援索引鍵集資料指標模型。|  
|SQL_MAX_LENGTH|0|如果您嘗試將此*fOption*值，此驅動程式會傳回錯誤 「 驅動程式不支援 」。|  
|SQL_MAX_ROWS|0|如果您嘗試將此*fOption*值，此驅動程式會傳回錯誤 「 驅動程式不支援 」。|  
|SQL_NOSCAN|SQL_NOSCAN_OFF||  
|SQL_QUERY_TIMEOUT|0|如果您嘗試將此*fOption*值，此驅動程式會傳回錯誤 「 驅動程式不支援 」。|  
|SQL_RETRIEVE_DATA|SQL_RD_ON, SQL_RD_OFF||  
|SQL_ROWSET_SIZE|1 到 4294967296||  
|SQL_SIMULATE_CURSOR|錯誤：「 驅動程式不支援 」||  
|SQL_USE_BOOKMARKS|SQL_UB_OFF<br /><br /> SQL_UB_ON||  
  
 如需詳細資訊，請參閱 < [SQLSetStmtOption](../../odbc/reference/syntax/sqlsetstmtoption-function.md)中*ODBC 程式設計人員參考*。
