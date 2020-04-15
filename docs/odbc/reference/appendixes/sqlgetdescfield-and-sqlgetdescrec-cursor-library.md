---
title: SQLGetDescField 和 SQLGetDescRec(游標庫) |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 49ceea6b6180e1b51f2f103f74412c3e2b4cbe02
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307829"
---
# <a name="sqlgetdescfield-and-sqlgetdescrec-cursor-library"></a>SQLGetDescField 和 SQLGetDescRec (資料指標程式庫)
> [!IMPORTANT]  
>  此功能將在將來版本的 Windows 中刪除。 避免在新的開發工作中使用此功能,並計劃修改當前使用此功能的應用程式。 Microsoft 建議使用驅動程式的游標功能。  
  
 本主題討論在游標庫中使用**SQLGetDescField**和**SQLGetDescRec**函數。 有關這些函數的一般資訊,請參閱[SQLGetDescField 函數](../../../odbc/reference/syntax/sqlgetdescfield-function.md)與[SQLGetDescRec 函數](../../../odbc/reference/syntax/sqlgetdescrec-function.md)。  
  
 游標庫執行**SQLGetDescRec**以返回書籤列的元數據。 游標庫執行**SQLGetDescField**傳回**SQLGetDescRec**傳回的相同欄位,這些字段SQL_DESC_NAME、SQL_DESC_TYPE、SQL_DESC_DATETIME_INTERVAL_CODE、SQL_DESC_OCTET_LENGTH、SQL_DESC_PRECISION、SQL_DESC_SCALE和SQL_DESC_NULLABLE。 為保持一致性 **,SQLGetDescField**還會返回SQL_DESC_UNNAMED。  
  
 游標庫在調用**SQLGetDescField 時執行 SQLGetDescField**以返回為綁定書簽列設置的以下欄位的值:SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR、SQL_DESC_OCTET_LENGTH_PTR和SQL_DESC_LENGTH。  
  
 在調用游標庫以返回SQL_DESC_BIND_OFFSET_PTR、SQL_DESC_BIND_TYPE、SQL_DESC_ROW_ARRAY_SIZE或SQL_DESC_ROW_STATUS_PTR欄位的值時,游標庫將執行**SQLGetDescField。** 可以為任何行返回這些欄位,而不僅僅是書籤行。  
  
 如果應用程式調用**SQLGetDescField**傳回上述欄位以外的任何欄位的值,則游標庫將調用傳遞給驅動程式。
