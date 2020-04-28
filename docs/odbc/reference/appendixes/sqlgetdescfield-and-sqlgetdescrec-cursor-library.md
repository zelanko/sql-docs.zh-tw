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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 49ceea6b6180e1b51f2f103f74412c3e2b4cbe02
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307829"
---
# <a name="sqlgetdescfield-and-sqlgetdescrec-cursor-library"></a>SQLGetDescField 和 SQLGetDescRec (資料指標程式庫)
> [!IMPORTANT]  
>  這項功能將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 本主題討論如何在資料指標程式庫中使用**SQLGetDescField**和**SQLGetDescRec**函數。 如需這些函式的一般資訊，請參閱[SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md)函式和[SQLGetDescRec 函數](../../../odbc/reference/syntax/sqlgetdescrec-function.md)。  
  
 游標程式庫會執行**SQLGetDescRec** ，以傳回書簽資料行的中繼資料。 資料指標程式庫會執行**SQLGetDescField** ，以傳回**SQLGetDescRec**所傳回的相同欄位，也就是 SQL_DESC_NAME、SQL_DESC_TYPE、SQL_DESC_DATETIME_INTERVAL_CODE、SQL_DESC_OCTET_LENGTH、SQL_DESC_PRECISION、SQL_DESC_SCALE 和 SQL_DESC_NullABLE。 為求一致， **SQLGetDescField**也會傳回 SQL_DESC_UNNAMED。  
  
 呼叫資料指標程式庫時，會執行**SQLGetDescField** ，以傳回下欄欄位的值，這些欄位是針對系結書簽資料行所設定： SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR、SQL_DESC_OCTET_LENGTH_PTR 和 SQL_DESC_LENGTH。  
  
 呼叫資料指標程式庫時，會執行**SQLGetDescField** ，以傳回 SQL_DESC_BIND_OFFSET_PTR、SQL_DESC_BIND_TYPE、SQL_DESC_ROW_ARRAY_SIZE 或 SQL_DESC_ROW_STATUS_PTR 欄位的值。 這些欄位可以傳回任何資料列，而不只是書簽資料列。  
  
 如果應用程式呼叫**SQLGetDescField**來傳回先前所述之任何欄位以外的值，則資料指標程式庫會將呼叫傳遞給驅動程式。
