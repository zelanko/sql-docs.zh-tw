---
title: SQLSetDescField 和 SQLSetDescRec （資料指標程式庫） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetDescField function [ODBC], Cursor Library
- SQLSetDescRec function [ODBC], Cursor Library
ms.assetid: 4ccff067-85cd-4bfa-a6cd-7f28051fb5b9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4cb723e7325454e6ff60e05d28a6321fd4d167e2
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2019
ms.locfileid: "67792827"
---
# <a name="sqlsetdescfield-and-sqlsetdescrec-cursor-library"></a>SQLSetDescField 和 SQLSetDescRec (資料指標程式庫)
> [!IMPORTANT]  
>  Windows 的未來版本將移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 本主題討論使用**SQLSetDescField**並**SQLSetDescRec**資料指標程式庫中的函式。 如需這些函式的一般資訊，請參閱[SQLSetDescField 函式](../../../odbc/reference/syntax/sqlsetdescfield-function.md)並[SQLSetDescRec 函式](../../../odbc/reference/syntax/sqlsetdescrec-function.md)。  
  
 資料指標程式庫執行**SQLSetDescField**時呼叫它來傳回欄位的值設定為書籤資料行：  
  
 SQL_DESC_DATA_PTR  
  
 SQL_DESC_INDICATOR_PTR  
  
 SQL_DESC_OCTET_LENGTH_PTR  
  
 SQL_DESC_LENGTH  
  
 SQL_DESC_OCTET_LENGTH  
  
 SQL_DESC_DATETIME_INTERVAL_CODE  
  
 SQL_DESC_SCALE  
  
 SQL_DESC_PRECISION  
  
 SQL_DESC_TYPE  
  
 SQL_DESC_NAME  
  
 SQL_DESC_UNNAMED  
  
 SQL_DESC_NULLABLE  
  
 資料指標程式庫執行呼叫**SQLSetDescRec**書籤資料行。  
  
 使用 ODBC 時*2.x*驅動程式，資料指標程式庫會傳回 SQLSTATE HY090 （無效的字串或緩衝區長度） 時**SQLSetDescField**或是**SQLSetDescRec**稱為若要設定的 SQL_DESC_OCTET_LENGTH 欄位 ARD 的書籤記錄的值不等於 4。 使用 ODBC 時*3.x*驅動程式，資料指標程式庫可讓任何大小的緩衝區。  
  
 資料指標程式庫執行**SQLSetDescField**時呼叫它來傳回 SQL_DESC_BIND_OFFSET_PTR、 SQL_DESC_BIND_TYPE、 SQL_DESC_ROW_ARRAY_SIZE，還是 SQL_DESC_ROW_STATUS_PTR 欄位的值。 這些欄位可能傳回的任何資料列，而不只是書籤資料列。  
  
 資料指標程式庫不會執行**SQLSetDescField**變更先前所述欄位以外的任何描述項欄位。 如果應用程式呼叫**SQLSetDescField**若要載入的資料指標程式庫時，請設定任何其他欄位，該呼叫會傳遞至驅動程式。  
  
 資料指標程式庫支援以動態方式變更應用程式的資料列描述項的任何資料列的 SQL_DESC_DATA_PTR、 SQL_DESC_INDICATOR_PTR 和 SQL_DESC_OCTET_LENGTH_PTR 欄位 (在呼叫之後**SQLExtendedFetch**， **SQLFetch**，或**SQLFetchScroll**)。 可以變更 SQL_DESC_OCTET_LENGTH_PTR 欄位，才能解除繫結資料行長度的緩衝區為 null 指標。  
  
 資料指標程式庫不支援資料指標開啟時，變更在 APD 或 ARD SQL_DESC_BIND_TYPE 欄位。 只會關閉資料指標之後，新的資料指標開啟之前，您可以變更 SQL_DESC_BIND_TYPE 欄位。 資料指標程式庫支援的資料指標開啟時變更的唯一描述項欄位是 SQL_DESC_ARRAY_STATUS_PTR、 SQL_DESC_BIND_OFFSET_PTR、 SQL_DESC_DATA_PTR、 SQL_DESC_INDICATOR_PTR、 SQL_DESC_OCTET_LENGTH_PTR 和 SQL_DESC_ROWS_PROCESSED_PTR。  
  
 資料指標程式庫不支援修改之後 ARD SQL_DESC_COUNT 欄位**SQLExtendedFetch**或是**SQLFetchScroll**已呼叫，並在關閉資料指標之前。
