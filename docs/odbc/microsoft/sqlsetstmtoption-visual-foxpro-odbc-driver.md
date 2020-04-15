---
title: SQLSetStmtOption(可視化狐狸Pro ODBC驅動程式) |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cb9677a9ccf307be847089c657964d96904eb20b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299398"
---
# <a name="sqlsetstmtoption-visual-foxpro-odbc-driver"></a>SQLSetStmtOption (Visual FoxPro ODBC Driver)
> [!NOTE]  
>  本主題包含 Visual FoxPro ODBC 特定於驅動程式的資訊。 有關此功能的一般資訊,請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的相應主題。  
  
 支援: 完整  
  
 ODBC API 符合性:1 級  
  
 設置與語句句柄*hstmt*相關的選項。  
  
|*fOption*|允許的值|註解|  
|---------------|--------------------|--------------|  
|SQL_ASYNC_ENABLE|SQL_ASYNC_ENABLE_OFF|如果嘗試設定此*fOption,* 驅動程式將傳回錯誤:「驅動程式無法。 Visual FoxPro 不支援非同步執行。|  
|SQL_BIND_TYPE|SQL_BIND_BY_COLUMN或 32 位值表示將結果列綁定到的結構或緩衝區實例的長度。||  
|SQL_CONCURRENCY|SQL_CONCUR_READ_ONLY<br /><br /> SQL_CONCUR_LOCK<br /><br /> SQL_CONCUR_VALUES|驅動程式不允許SQL_CONCUR_ROWVER,因為 Visual FoxPro 沒有基於時間戳的行版本控制。|  
|SQL_CURSOR_TYPE|SQL_CURSOR_FORWARD_ONLY<br /><br /> SQL_CURSOR_STATIC|驅動程序不允許SQL_CURSOR_KEYSET_DRIVEN或SQL_CURSOR_DYNAMIC;關於詳細資訊[,請參閱 SQLSetScroll 選項](../../odbc/microsoft/sqlsetscrolloptions-visual-foxpro-odbc-driver.md)。|  
|SQL_KEYSET_SIZE|錯誤:"驅動程序無法使用"|Visual FoxPro 不支援鍵集游標模型。|  
|SQL_MAX_LENGTH|0|如果嘗試設定此*fOption*值,驅動程式將返回錯誤"驅動程式無法。|  
|SQL_MAX_ROWS|0|如果嘗試設定此*fOption*值,驅動程式將返回錯誤"驅動程式無法。|  
|SQL_NOSCAN|SQL_NOSCAN_OFF||  
|SQL_QUERY_TIMEOUT|0|如果嘗試設定此*fOption*值,驅動程式將返回錯誤"驅動程式無法。|  
|SQL_RETRIEVE_DATA|SQL_RD_OFFSQL_RD_ON||  
|SQL_ROWSET_SIZE|1 到 4,294,967,296||  
|SQL_SIMULATE_CURSOR|錯誤:"驅動程序無法使用"||  
|SQL_USE_BOOKMARKS|SQL_UB_OFF<br /><br /> SQL_UB_ON||  
  
 有關詳細資訊,請參閱*ODBC 程式師參考*中的[SQLSetStmtOption。](../../odbc/reference/syntax/sqlsetstmtoption-function.md)
