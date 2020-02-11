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
ms.openlocfilehash: 5a21af2a2067498a3ec495013554b70d6a86455a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68125568"
---
# <a name="sqlsetdescfield-and-sqlsetdescrec-cursor-library"></a>SQLSetDescField 和 SQLSetDescRec (資料指標程式庫)
> [!IMPORTANT]  
>  這項功能將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 本主題討論如何在資料指標程式庫中使用**SQLSetDescField**和**SQLSetDescRec**函數。 如需這些函式的一般資訊，請參閱[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)函式和[SQLSetDescRec 函數](../../../odbc/reference/syntax/sqlsetdescrec-function.md)。  
  
 呼叫資料指標程式庫時，會執行**SQLSetDescField** ，以傳回針對書簽資料行所設定的欄位值：  
  
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
  
 資料指標程式庫會針對書簽資料行執行**SQLSetDescRec**的呼叫。  
  
 使用*ODBC 2.x*驅動程式時，當呼叫**SQLSetDescField**或**SQLSetDescRec**將 ARD 之書簽記錄的 SQL_DESC_OCTET_LENGTH 欄位設定為不等於4的值時，資料指標程式庫會傳回 SQLSTATE HY090 （不正確字串或緩衝區長度）。 使用*ODBC 3.x*驅動程式時，資料指標程式庫可讓緩衝區成為任何大小。  
  
 呼叫資料指標程式庫時，會執行**SQLSetDescField** ，以傳回 SQL_DESC_BIND_OFFSET_PTR、SQL_DESC_BIND_TYPE、SQL_DESC_ROW_ARRAY_SIZE 或 SQL_DESC_ROW_STATUS_PTR 欄位的值。 這些欄位可以傳回任何資料列，而不只是書簽資料列。  
  
 資料指標程式庫不會執行**SQLSetDescField**來變更先前所述欄位以外的任何描述項欄位。 如果應用程式在載入資料指標程式庫時呼叫**SQLSetDescField**來設定其他任何欄位，則會將呼叫傳遞至驅動程式。  
  
 資料指標程式庫支援動態變更應用程式資料列描述元之任何資料列的 SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR 和 SQL_DESC_OCTET_LENGTH_PTR 欄位（在呼叫**SQLExtendedFetch**、 **SQLFetch**或**SQLFetchScroll**之後）。 只有在將資料行的長度緩衝區解除系結時，才能將 [SQL_DESC_OCTET_LENGTH_PTR] 欄位變更為 null 指標。  
  
 當資料指標開啟時，資料指標程式庫不支援變更 APD 或 ARD 中的 SQL_DESC_BIND_TYPE 欄位。 只有在資料指標關閉之後，以及新的資料指標開啟之前，才可以變更 [SQL_DESC_BIND_TYPE] 欄位。 資料指標開啟時，資料指標程式庫支援變更的唯一描述項欄位是 SQL_DESC_ARRAY_STATUS_PTR、SQL_DESC_BIND_OFFSET_PTR、SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR、SQL_DESC_OCTET_LENGTH_PTR 和 SQL_DESC_ROWS_PROCESSED_指標.  
  
 資料指標程式庫不支援在呼叫**SQLExtendedFetch**或**SQLFetchScroll**之後，以及在關閉資料指標之前，修改 ARD 的 SQL_DESC_COUNT 欄位。
