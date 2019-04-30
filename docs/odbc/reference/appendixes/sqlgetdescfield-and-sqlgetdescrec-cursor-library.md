---
title: SQLGetDescField 和 SQLGetDescRec （資料指標程式庫） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetDescField function [ODBC], Cursor Library
- SQLGetDescRec function [ODBC], Cursor Library
ms.assetid: 1a801f22-6fea-48aa-a723-3187a2ad852b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 66361572427c3264a1b25fe1c851685a07b2e029
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63188763"
---
# <a name="sqlgetdescfield-and-sqlgetdescrec-cursor-library"></a>SQLGetDescField 和 SQLGetDescRec (資料指標程式庫)
> [!IMPORTANT]  
>  Windows 的未來版本將移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 本主題討論使用**SQLGetDescField**並**SQLGetDescRec**資料指標程式庫中的函式。 如需這些函式的一般資訊，請參閱[SQLGetDescField 函式](../../../odbc/reference/syntax/sqlgetdescfield-function.md)並[SQLGetDescRec 函式](../../../odbc/reference/syntax/sqlgetdescrec-function.md)。  
  
 資料指標程式庫執行**SQLGetDescRec**傳回書籤資料行的中繼資料。 資料指標程式庫執行**SQLGetDescField**傳回所傳回的相同欄位**SQLGetDescRec**，這是與 SQL_DESC_NAME、 SQL_DESC_TYPE、 SQL_DESC_DATETIME_INTERVAL_CODE、 SQL_DESC_OCTET_長度、 SQL_DESC_PRECISION、 SQL_DESC_SCALE 和 SQL_DESC_NULLABLE。 為求一致， **SQLGetDescField**也會將 SQL_DESC_UNNAMED 傳回。  
  
 資料指標程式庫執行**SQLGetDescField**時呼叫它來傳回下列值欄位，已為書籤資料行繫結：SQL_DESC_DATA_PTR、 SQL_DESC_INDICATOR_PTR、 SQL_DESC_OCTET_LENGTH_PTR 和 SQL_DESC_LENGTH。  
  
 資料指標程式庫執行**SQLGetDescField**時呼叫它來傳回 SQL_DESC_BIND_OFFSET_PTR、 SQL_DESC_BIND_TYPE、 SQL_DESC_ROW_ARRAY_SIZE，還是 SQL_DESC_ROW_STATUS_PTR 欄位的值。 這些欄位可能傳回的任何資料列，而不只是書籤資料列。  
  
 如果應用程式呼叫**SQLGetDescField**傳回以外先前所述的任何欄位的值，資料指標程式庫會傳遞至驅動程式呼叫。
