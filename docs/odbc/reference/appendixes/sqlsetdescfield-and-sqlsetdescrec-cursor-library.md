---
description: SQLSetDescField 和 SQLSetDescRec (資料指標程式庫)
title: SQLSetDescField 和 SQLSetDescRec (資料指標程式庫) |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cef4967a81a78e08dee733072359459c864b9627
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476940"
---
# <a name="sqlsetdescfield-and-sqlsetdescrec-cursor-library"></a>SQLSetDescField 和 SQLSetDescRec (資料指標程式庫)
> [!IMPORTANT]  
>  未來的 Windows 版本將會移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 本主題討論如何在資料指標程式庫中使用 **SQLSetDescField** 和 **SQLSetDescRec** 函數。 如需這些函式的一般資訊，請參閱 [SQLSetDescField 函數](../../../odbc/reference/syntax/sqlsetdescfield-function.md) 和 [SQLSetDescRec 函數](../../../odbc/reference/syntax/sqlsetdescrec-function.md)。  
  
 資料指標程式庫會在呼叫時執行 **SQLSetDescField** ，以傳回針對書簽資料行所設定的欄位值：  
  
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
  
 資料指標程式庫會針對書簽資料行執行 **SQLSetDescRec** 的呼叫。  
  
 使用 *ODBC 2.x* 驅動程式時，資料指標程式庫會傳回 SQLSTATE HY090 (不正確字串或緩衝區長度) 當呼叫 **SQLSetDescField** 或 **SQLSetDescRec** 將 ARD 書簽記錄的 SQL_DESC_OCTET_LENGTH 欄位設定為不等於4的值時。 使用 *ODBC 3.x* 驅動程式時，資料指標程式庫允許緩衝區是任何大小。  
  
 當呼叫它來傳回 SQL_DESC_BIND_OFFSET_PTR、SQL_DESC_BIND_TYPE、SQL_DESC_ROW_ARRAY_SIZE 或 SQL_DESC_ROW_STATUS_PTR 欄位的值時，資料指標程式庫會執行 **SQLSetDescField** 。 這些欄位可以傳回任何資料列，而不只是書簽資料列。  
  
 資料指標程式庫不會執行 **SQLSetDescField** 來變更先前提及之欄位以外的任何描述項欄位。 如果應用程式在載入資料指標程式庫時呼叫 **SQLSetDescField** 來設定任何其他欄位，則會將呼叫傳遞至驅動程式。  
  
 資料指標程式庫支援在呼叫 **SQLExtendedFetch**、 **SQLFetch**或 **SQLFetchScroll**) 之後，以動態方式 (變更應用程式資料列描述項之任何資料列的 SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR 和 SQL_DESC_OCTET_LENGTH_PTR 欄位。 SQL_DESC_OCTET_LENGTH_PTR 欄位只能變更為 null 指標，以將資料行的長度緩衝區解除系結。  
  
 當資料指標開啟時，資料指標程式庫不支援變更 APD 或 ARD 中的 SQL_DESC_BIND_TYPE 欄位。 只有在資料指標關閉之後，以及開啟新的資料指標之前，才可以變更 SQL_DESC_BIND_TYPE 欄位。 當資料指標開啟時，資料指標程式庫支援變更的唯一描述項欄位為 SQL_DESC_ARRAY_STATUS_PTR、SQL_DESC_BIND_OFFSET_PTR、SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR、SQL_DESC_OCTET_LENGTH_PTR 和 SQL_DESC_ROWS_PROCESSED_PTR。  
  
 資料指標程式庫不支援在呼叫 **SQLExtendedFetch** 或 **SQLFetchScroll** 之後，以及資料指標關閉之前修改 ARD 的 SQL_DESC_COUNT 欄位。
