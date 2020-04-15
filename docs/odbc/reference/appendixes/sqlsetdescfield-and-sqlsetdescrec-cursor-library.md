---
title: SQLSetDescField 和 SQLSetDescRec(游標庫) |微軟文件
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
ms.openlocfilehash: b85eb84cdf48a1c2a441b8994076a9023d254f2d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300548"
---
# <a name="sqlsetdescfield-and-sqlsetdescrec-cursor-library"></a>SQLSetDescField 和 SQLSetDescRec (資料指標程式庫)
> [!IMPORTANT]  
>  此功能將在將來版本的 Windows 中刪除。 避免在新的開發工作中使用此功能,並計劃修改當前使用此功能的應用程式。 Microsoft 建議使用驅動程式的游標功能。  
  
 本主題討論在游標庫中使用**SQLSetDescField**和**SQLSetDescRec**函數。 有關這些函數的一般資訊,請參閱[SQLSetDescField 函數](../../../odbc/reference/syntax/sqlsetdescfield-function.md)與[SQLSetDescRec 函數](../../../odbc/reference/syntax/sqlsetdescrec-function.md)。  
  
 在呼叫游標庫以傳回為書籤列設定的欄位的值時,游標庫將執行**SQLSetDescField:**  
  
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
  
 游標庫執行對**SQLSetDesccRec**的書籤列的調用。  
  
 使用 ODBC *2.x*驅動程式時,當調用**SQLSetDescField**或**SQLSetDescRec**將 ARD 書籤記錄的SQL_DESC_OCTET_LENGTH欄位設置為不等於 4 的值時,游標庫將返回 SQLSTATE HY090(無效字串或緩衝區長度)。 使用 ODBC *3.x*驅動程式時,游標庫允許緩衝區具有任何大小。  
  
 在調用游標庫以返回SQL_DESC_BIND_OFFSET_PTR、SQL_DESC_BIND_TYPE、SQL_DESC_ROW_ARRAY_SIZE或SQL_DESC_ROW_STATUS_PTR欄位的值時,游標庫將執行**SQLSetDescField。** 可以為任何行返回這些欄位,而不僅僅是書籤行。  
  
 游標庫不執行**SQLSetDescField**來更改除前面提到的欄位之外的任何描述符欄位。 如果應用程式調用**SQLSetDescField**在載入游標庫時設置任何其他欄位,則調用將傳遞到驅動程式。  
  
 游標庫支援動態更改應用程式行描述符的任何行SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR和SQL_DESC_OCTET_LENGTH_PTR欄位(在呼叫**SQL 擴充取得****、SQLFetch**或**SQLFetchScroll**之後)。 SQL_DESC_OCTET_LENGTH_PTR欄位只能更改為空指標,以取消綁定列的長度緩衝區。  
  
 游標庫不支援在打開游標時更改 APD 或 ARD 中的SQL_DESC_BIND_TYPE欄位。 只有在關閉游標后和打開新遊標之前,才能更改SQL_DESC_BIND_TYPE欄位。 游標庫在打開游標時支援更改的唯一描述符欄位是SQL_DESC_ARRAY_STATUS_PTR、SQL_DESC_BIND_OFFSET_PTR、SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR、SQL_DESC_OCTET_LENGTH_PTR和SQL_DESC_ROWS_PROCESSED_PTR。  
  
 在調用**SQL 延長獲取**或**SQLFetchScroll**後以及游標關閉之前,遊標庫不支援修改 ARD 的SQL_DESC_COUNT欄位。
