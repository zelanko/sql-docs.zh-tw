---
description: SQLGetDescField 和 SQLGetDescRec (資料指標程式庫)
title: SQLGetDescField 和 SQLGetDescRec (資料指標程式庫) |Microsoft Docs
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
ms.openlocfilehash: f13b3ff5ed7e54a127089b74b5a45081900edf55
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494748"
---
# <a name="sqlgetdescfield-and-sqlgetdescrec-cursor-library"></a>SQLGetDescField 和 SQLGetDescRec (資料指標程式庫)
> [!IMPORTANT]  
>  未來的 Windows 版本將會移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 本主題討論如何在資料指標程式庫中使用 **SQLGetDescField** 和 **SQLGetDescRec** 函數。 如需這些函式的一般資訊，請參閱 [SQLGetDescField 函數](../../../odbc/reference/syntax/sqlgetdescfield-function.md) 和 [SQLGetDescRec 函數](../../../odbc/reference/syntax/sqlgetdescrec-function.md)。  
  
 資料指標程式庫會執行 **SQLGetDescRec** ，以傳回書簽資料行的中繼資料。 資料指標程式庫會執行 **SQLGetDescField** ，以傳回 **SQLGetDescRec**所傳回的相同欄位，這些欄位是 SQL_DESC_NAME、SQL_DESC_TYPE、SQL_DESC_DATETIME_INTERVAL_CODE、SQL_DESC_OCTET_LENGTH、SQL_DESC_PRECISION、SQL_DESC_SCALE 和 SQL_DESC_NullABLE。 為了保持一致性， **SQLGetDescField** 也會傳回 SQL_DESC_UNNAMED。  
  
 資料指標程式庫會在呼叫時執行 **SQLGetDescField** ，以傳回下列為系結書簽資料行所設定的欄位值： SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR、SQL_DESC_OCTET_LENGTH_PTR 和 SQL_DESC_LENGTH。  
  
 當呼叫它來傳回 SQL_DESC_BIND_OFFSET_PTR、SQL_DESC_BIND_TYPE、SQL_DESC_ROW_ARRAY_SIZE 或 SQL_DESC_ROW_STATUS_PTR 欄位的值時，資料指標程式庫會執行 **SQLGetDescField** 。 這些欄位可以傳回任何資料列，而不只是書簽資料列。  
  
 如果應用程式呼叫 **SQLGetDescField** 來傳回先前所述以外的任何欄位值，則資料指標程式庫會將呼叫傳遞給驅動程式。
