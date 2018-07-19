---
title: SQLSetDescField 和 SQLSetDescRec （資料指標程式庫） |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLSetDescField function [ODBC], Cursor Library
- SQLSetDescRec function [ODBC], Cursor Library
ms.assetid: 4ccff067-85cd-4bfa-a6cd-7f28051fb5b9
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 04c3fd1c3c64140b7669cdeeb35937498249ac66
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32910273"
---
# <a name="sqlsetdescfield-and-sqlsetdescrec-cursor-library"></a>SQLSetDescField 和 SQLSetDescRec （資料指標程式庫）
> [!IMPORTANT]  
>  將移除這項功能，在未來的版本的 Windows。 避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 本主題討論使用**SQLSetDescField**和**SQLSetDescRec**資料指標程式庫中的函式。 如需這些函式的一般資訊，請參閱[SQLSetDescField 函數](../../../odbc/reference/syntax/sqlsetdescfield-function.md)和[SQLSetDescRec 函數](../../../odbc/reference/syntax/sqlsetdescrec-function.md)。  
  
 資料指標程式庫執行**SQLSetDescField**呼叫傳回之欄位的值時設定為書籤資料行：  
  
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
  
 當使用的 ODBC 2。*x*驅動程式，資料指標程式庫會傳回 SQLSTATE HY090 （無效的字串或緩衝區長度） 時**SQLSetDescField**或**SQLSetDescRec**呼叫以設定 SQL_DESC_OCTET_值不等於 4 ARD 的書籤記錄的長度欄位。 使用 ODBC 3 時 *.x*驅動程式，資料指標程式庫會允許任何大小的緩衝區。  
  
 資料指標程式庫執行**SQLSetDescField**當呼叫它來傳回 SQL_DESC_BIND_OFFSET_PTR、 SQL_DESC_BIND_TYPE、 SQL_DESC_ROW_ARRAY_SIZE 或 SQL_DESC_ROW_STATUS_PTR 欄位的值。 這些欄位可傳回的任何資料列，而不只是書籤的資料列。  
  
 資料指標程式庫不會執行**SQLSetDescField**變更先前所述的欄位以外的任何描述項欄位。 如果應用程式呼叫**SQLSetDescField**設定任何其他欄位載入資料指標程式庫時，呼叫會傳遞至驅動程式。  
  
 資料指標程式庫支援動態變更的應用程式的資料列描述項的任何資料列的 SQL_DESC_DATA_PTR、 SQL_DESC_INDICATOR_PTR 和 SQL_DESC_OCTET_LENGTH_PTR 欄位 (呼叫後**SQLExtendedFetch**， **SQLFetch**，或**SQLFetchScroll**)。 可以變更 SQL_DESC_OCTET_LENGTH_PTR 欄位的 null 指標只有解除繫結資料行長度的緩衝區。  
  
 資料指標程式庫不支援資料指標開啟時，變更在 APD 或 ARD SQL_DESC_BIND_TYPE 欄位。 只會關閉資料指標之後，新的資料指標開啟之前，可以變更 SQL_DESC_BIND_TYPE 欄位。 資料指標程式庫支援的資料指標開啟時變更的唯一描述項欄位是 SQL_DESC_ARRAY_STATUS_PTR、 SQL_DESC_BIND_OFFSET_PTR、 SQL_DESC_DATA_PTR、 SQL_DESC_INDICATOR_PTR、 SQL_DESC_OCTET_LENGTH_PTR 和 SQL_DESC_ROWS_PROCESSED_PTR。  
  
 資料指標程式庫不支援修改之後 ARD SQL_DESC_COUNT 欄位**SQLExtendedFetch**或**SQLFetchScroll**已經呼叫，並在關閉資料指標之前。
